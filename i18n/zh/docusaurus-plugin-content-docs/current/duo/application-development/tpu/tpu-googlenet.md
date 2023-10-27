---
sidebar_label: '基于Googlenet的图像分类'
sidebar_position: 37
---

# 基于 Googlenet 的图像分类

## 1. 配置 Docker 开发环境

参考 [这里](https://milkv.io/zh/docs/duo/application-development/tpu/tpu-docker) 配置好 Docker 开发环境后，再回到这里继续下一步

## 2. 在 Docker 中准备工作目录

创建并进入 `googlenet` 工作目录，注意是与 `tpu-mlir_*` 同级的目录
```
# mkdir googlenet && cd googlenet
```

获取原始模型
```
wget https://github.com/onnx/models/raw/main/vision/classification/inception_and_googlenet/googlenet/model/googlenet-12.onnx
```

拷贝测试图片:
```
# cp -rf ${TPUC_ROOT}/regression/dataset/ILSVRC2012/ .
# cp -rf ${TPUC_ROOT}/regression/image/ .
```
这里的 `${TPUC_ROOT}` 是环境变量，对应 `tpu-mlir_*` 目录，是在前面配置 Docker 开发环境中 `source ./tpu-mlir_*/envsetup.sh` 这一步加载的

创建并进入 `work` 工作目录，用于存放编译生成的 MLIR、cvimodel 等文件
```
# mkdir work && cd work
```

## 3. ONNX 模型转换

:::tip
Duo 开发板搭载的是 CV1800B 芯片，该芯片支持 **ONNX 系列** 和 **Caffe 模型**，目前不支持 TFLite 模型。在量化数据类型方面，支持 **BF16 格式的量化** 和 **INT8 格式的非对称量化**
:::

### ONNX 模型转换成 MLIR

本例中的模型是 RGB 输入, `mean` 和 `scale` 分别为 `123.675`,`116.28`,`103.53` 和 `0.0171`,`0.0175`,`0.0174`，模型转换命令如下:
```
model_transform.py \
 --model_name googlenet \
 --model_def ../googlenet-12.onnx \
 --test_input ../image/cat.jpg \
 --input_shapes [[1,3,224,224]] \
 --resize_dims 256,256 \
 --mean 123.675,116.28,103.53 \
 --scale 0.0171,0.0175,0.0174 \
 --pixel_format rgb \
 --test_result googlenet_top_outputs.npz \
 --mlir googlenet.mlir
```

运行成功效果示例

![duo](/docs/duo/tpu/duo-tpu-googlenet_05.png)

转成 MLIR 模型后，会生成一个 `googlenet.mlir` 文件，该文件即为 MLIR 模型文件，还会生成一个 `googlenet_in_f32.npz` 文件和一个 `googlenet_top_outputs.npz` 文件，是后续转模型的输入文件

![duo](/docs/duo/tpu/duo-tpu-googlenet_06.png)

### MLIR 转 BF16 模型

将 MLIR 模型转换为 BF16 模型的命令如下:
```
model_deploy.py \
 --mlir googlenet.mlir \
 --quantize BF16 \
 --chip cv180x \
 --test_input googlenet_in_f32.npz \
 --test_reference googlenet_top_outputs.npz \
 --model googlenet_cv180x_bf16.cvimodel
```

运行成功效果示例

![duo](/docs/duo/tpu/duo-tpu-googlenet_07.png)

编译完成后，会生成 `googlenet_cv180x_bf16.cvimodel` 文件

![duo](/docs/duo/tpu/duo-tpu-googlenet_08.png)

### MLIR 转 INT8 模型

#### 生成量化需要的校准表

运行 `run_calibration.py` 得到校准表，输入数据的数量根据情况准备 100~1000 张左右。 这里用现有的 100 张来自 ILSVRC2012 的图片举例，执行 calibration 命令：
```
run_calibration.py googlenet.mlir \
 --dataset ../ILSVRC2012 \
 --input_num 100 \
 -o googlenet_cali_table
```

运行成功效果示例

![duo](/docs/duo/tpu/duo-tpu-googlenet_09.png)

运行完成后会生成名为 `googlenet_cali_table` 的文件, 该文件用于后续编译 INT8 模型的输入文件

![duo](/docs/duo/tpu/duo-tpu-googlenet_10.png)

#### MLIR 量化成 INT8 非对称 cvimodel

将 MLIR 模型转换为 INT8 模型的命令如下:
```
model_deploy.py \
 --mlir googlenet.mlir \
 --quantize INT8 \
 --calibration_table googlenet_cali_table \
 --chip cv180x \
 --test_input ../image/cat.jpg \
 --test_reference googlenet_top_outputs.npz \
 --compare_all \
 --fuse_preprocess \
 --model googlenet_cv180x_int8_fuse.cvimodel
```

运行成功效果示例

![duo](/docs/duo/tpu/duo-tpu-googlenet_11.png)

编译完成后, 会生成名为 `googlenet_cv180x_int8_fuse.cvimodel` 的文件

![duo](/docs/duo/tpu/duo-tpu-googlenet_12.png)

## 4. 在 Duo 开发板上进行验证

### 连接 Duo 开发板

根据前面的教程完成 Duo 开发板与电脑的连接，并使用 `mobaxterm` 或 `Xshell` 等工具开启终端操作 Duo 开发板

### 获取 cvitek_tpu_sdk

1. 从 MEGA 下载

   [下载地址](https://mega.nz/folder/yZghQA4R#aZkbTwJb7Ji5LvAWIuBtag)

   包名: `cvitek_tpu_sdk_cv180x_musl_riscv64_rvv.tar.gz`

2. 从 ftp 服务器下载

   ```
   sftp://218.17.249.213
   username: cvitek_mlir_2023
   password: 7&2Wd%cu5k
   ```
   如果文件未找到，可以到 backup 目录中找一下，可能更新版本后旧版本的包被放到 backup 目录

下载完成后，通过 Windows 终端拷贝到 Docker 中
```
docker cp C:\Users\Carbon\Duo-TPU\cvitek_tpu_sdk_cv180x_musl_riscv64_rvv.tar.gz  DuoTPU:/workspace/
```

并在 Docker 中进行解压
```
# cd /workspace
# tar -zxvf cvitek_tpu_sdk_cv180x_musl_riscv64_rvv.tar.gz
```

解压完成后会生成`cvitek_tpu_sdk`文件夹

### 将开发工具包和模型文件拷贝到开发板上

在 duo 开发板的终端中，新建文件目录 `/mnt/tpu/`
```
# mkdir -p /mnt/tpu && cd /mnt/tpu
```

在 Docker 的终端中，将开发工具包和前面生成的两个模型文件拷贝到开发板上
```
# scp -r /workspace/cvitek_tpu_sdk root@192.168.42.1:/mnt/tpu/
# scp /workspace/googlenet/work/googlenet_cv180x_bf16.cvimodel root@192.168.42.1:/mnt/tpu/cvitek_tpu_sdk/
# scp /workspace/googlenet/work/googlenet_cv180x_int8_fuse.cvimodel root@192.168.42.1:/mnt/tpu/cvitek_tpu_sdk/
```

### 设置环境变量

在 Duo 开发板的终端中，进行环境变量的设置
```
# cd /mnt/tpu/cvitek_tpu_sdk
# source ./envs_tpu_sdk.sh
```

### 进行图像分类测试

在 Duo 开发板上，对该图像进行分类

![duo](/docs/duo/tpu/duo-tpu-cat.jpg)

使用 `googlenet_cv180x_bf16.cvimodel` 模型进行图像分类
```
./samples/bin/cvi_sample_classifier_bf16 \
 ./googlenet_cv180x_bf16.cvimodel \
 ./samples/data/cat.jpg \
 ./samples/data/synset_words.txt
```

分类成功结果示例

![duo](/docs/duo/tpu/duo-tpu-googlenet_13.png)

使用 `googlenet_cv180x_int8_fuse.cvimodel` 模型进行图像分类
```
./samples/bin/cvi_sample_classifier_fused_preprocess \
 ./googlenet_cv180x_int8_fuse.cvimodel \
 ./samples/data/cat.jpg \
 ./samples/data/synset_words.txt
```

分类成功结果示例

![duo](/docs/duo/tpu/duo-tpu-googlenet_14.png)


## 5. 附录

正文涉及到的文件总结如下

- TPU-MLIR 模型转换工具：`tpu-mlir_v1.3.228-g19ca95e9-20230921.tar.gz`
- TPU SDK 开发工具包：`cvitek_tpu_sdk_cv180x_musl_riscv64_rvv.tar.gz`
- (附) Sample 测试例程源码：`cvitek_tpu_samples.tar.gz`
- (附) 转换好的 cvimodel 包：`cvimodel_samples_cv180x.tar.gz`

正文提到的 TPU 开发所需的包文件可在下面 sftp 站点获取，或者从 [MEGA](https://mega.nz/folder/yZghQA4R#aZkbTwJb7Ji5LvAWIuBtag) 下载
```
sftp://218.17.249.213
user: cvitek_mlir_2023
password: 7&2Wd%cu5k
```

使用 WinSCP 登陆 sftp 站点后的界面

![duo](/docs/duo/tpu/duo-tpu-sftp.png)

注意：
1. sample 目录下的 samples_extra 提供了更多 samples 脚本，但其中 cvimodel 名字已经硬编码在其中，如想使用脚本运行，需要自行修改 cvimodel 名字
2. 此小节介绍的是使用预编译好的 sample 程序对转换好的 cvimodel 进行部署测试，如果开发者有兴趣对 samples 源码进行编码和交叉编译，请参考官网 [TPU-MLIR文档](https://doc.sophgo.com/sdk-docs/v23.05.01/docs_latest_release/docs/tpu-mlir/quick_start/html/10_cv18xx_guide.html#runtime-sample) 中的第9章《CV18xx芯片使用指南》中的第3小节 "编译和运行runtime sample" 内容