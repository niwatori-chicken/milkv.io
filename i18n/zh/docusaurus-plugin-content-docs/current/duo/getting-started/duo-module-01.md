---
sidebar_label: 'Duo Module 01 (SG2000)'
sidebar_position: 4
---

# Duo Module 01

<Image src='/docs/duo/dm01/size-view.webp' maxWidth='30%' align='center' />

Duo Module 01 是一款集成了 SG2000、WI-FI6/BTDM5.4 和 eMMC 的紧凑型模块。它支持 SMD 贴片。此外，它还能大大节省产品开发时间。它是制作产品的首选。

为了您在使用 Duo Module 01 设计产品时，能够快速进行产品初期的方案验证与调试，Duo Module 01 还提供一个评估板，该底板专为核心板设计，提供丰富的接口和功能。

<Image src='/docs/duo/dm01/dm01-eb.webp' maxWidth='70%' align='center' />

## SG2000 简介

SG2000 是一款高性能、低功耗芯片，专为智能监控 IP 摄像机、本地面部识别考勤机、智能家居设备等各种产品领域而设计。 它集成了 H.264/H.265 视频压缩解码和 ISP 能力。 支持 HDR 宽动态、3D 降噪、去雾、镜头畸变校正等多种图像增强和校正算法，为客户提供专业级的视频图像质量。

该芯片还集成了内部 TPU，在 INT8 运算下可提供约 0.5TOPS 的计算能力。专门设计的 TPU 调度引擎高效地为张量处理单元核心提供高带宽数据流。它还为用户提供了强大的深度学习模型编译器和软件 SDK 开发套件。 Caffe、Pytorch、ONNX、MXNet、TensorFlow（Lite）等主流深度学习框架都可以轻松移植到该平台。

## SG2000 数据手册

我们已将 SG2000 的数据手册和 TRM 开源到 GitHub。请 [查看](https://github.com/milkv-duo/duo-files/tree/main/duo-s/datasheet)。

## 购买

Milk-V 是 SG2000 芯片的全球授权经销商。您可以直接从我们的经销商 [Arace](https://arace.tech/products/sophon-cv1800b-5pcs) 购买 `Duo Module 01` 和 `SG2000` 芯片的样品。如需批量订购，请联系 [Milk-V 销售团队](mailto:sales@milkv.io) 获取报价。

## 上手指南

### 安装系统

:::tip
Duo Module 01 的软件与 DuoS 是通用的，请直接使用 DuoS 的固件。
:::

- 从 SD 卡启动
  
  请参考：[启动](https://milkv.io/zh/docs/duo/getting-started/boot) 章节。

- 从 eMMC 启动
  
  请参考：[eMMC 版本固件烧录](https://milkv.io/zh/docs/duo/getting-started/duos#emmc-%E7%89%88%E6%9C%AC%E5%9B%BA%E4%BB%B6%E7%83%A7%E5%BD%95) 章节。

### USB 网络的使用

请参考：[设置](https://milkv.io/zh/docs/duo/getting-started/setup) 章节。

## Duo Module 01 GPIO 引脚分配

### GPIO 引脚映射

<div className='gpio_style'>

| GROUP | ADDR          | PORT  | CHIP      | NUM     | NAME     | START             |
|:-----:|:-------------:|:-----:|:---------:|:-------:|:---------|:------------------|
| gpio0 | gpio@03020000 | porta | gpiochip0 | 480-511 | XGPIOA   | 480 - XGPIOA[0]   |
| gpio1 | gpio@03021000 | portb | gpiochip1 | 448-479 | XGPIOB   | 448 - XGPIOB[0]   |
| gpio2 | gpio@03022000 | portc | gpiochip2 | 416-447 | XGPIOC   | 416 - XGPIOC[0]   |
| gpio3 | gpio@03023000 | portd | gpiochip3 | 384-415 |          |                   |
| gpio4 | gpio@05021000 | porte | gpiochip4 | 352-383 | PWR_GPIO | 352 - PWR_GPIO[0] |

</div>

### GPIO 引脚定义

<div className='gpio_style' style={{ overflow :"auto"}} >

| PIN                             | NAME            | SG2000     | NUM |  MIPI DSI   |
|:-------------------------------:|:----------------|:-----------|:---:|:---------- |
| <div className='green'>1</div>  | MIPI_TX_2N      | XGPIOC[16] | 432 | MIPI_TX_CN |
| <div className='green'>2</div>  | MIPI_TX_2P      | XGPIOC[17] | 433 | MIPI_TX_CP |
| <div className='green'>3</div>  | MIPI_TX_1N      | XGPIOC[14] | 430 | MIPI_TX_1N |
| <div className='green'>4</div>  | MIPI_TX_1P      | XGPIOC[15] | 431 | MIPI_TX_1P |
| <div className='green'>5</div>  | MIPI_TX_0N      | XGPIOC[12] | 428 | MIPI_TX_0N |
| <div className='green'>6</div>  | MIPI_TX_0P      | XGPIOC[13] | 429 | MIPI_TX_0P |
| <div className='orange'>7</div> | 3V3             |            |     |            |
| <div className='orange'>8</div> | 3V3             |            |     |            |
| <div className='black'>9</div>  | GND             |            |     |            |
| <div className='green'>10</div> | SENSOR_HS0      | XGPIOA[1]  |     |            |
| <div className='green'>11</div> | SENSOR_CLK1     | XGPIOA[3]  |     |            |
| <div className='green'>12</div> | SENSOR_CLK0     | XGPIOA[0]  |     |            |
| <div className='green'>13</div> | I2C3_SENSOR0_SDA| XGPIOA[6]  |     |            |
| <div className='green'>14</div> | I2C3_SENSOR0_SCL| XGPIOA[5]  |     |            |
| <div className='green'>15</div> | SENSOR_RSTN1    | XGPIOA[4]  |     |            |
| <div className='green'>16</div> | SENSOR_RSTN0    | XGPIOA[2]  |     |            |
| <div className='green'>17</div> | AUDIO_OUT_L     |            |     |            |
| <div className='green'>18</div> | AUDIO_OUT_R     |            |     |            |
| <div className='green'>19</div> | AUDIO_IN_L      |            |     |            |
| <div className='green'>20</div> | AUDIO_IN_R      |            |     |            |
| <div className='green'>21</div> | SD_SD0_D1       | XGPIOA[10] |     |            |
| <div className='green'>22</div> | SD_SD0_CMD      | XGPIOA[8]  |     |            |


</div>

<div className='gpio_style' style={{ overflow :"auto"}} >

| PIN                             | NAME            | SG2000     | NUM | UART              | PWM  | JTAG    | MIPI DSI   | I2C      |
|:-------------------------------:|:----------------|:-----------|:---:|:----------------- |:-----|:--------|:---------- |:---------|
| <div className='green'>23</div> | SD_SD0_CD       | XGPIOA[13] |     |                   |      |         |            |          |
| <div className='green'>24</div> | SD_SD0_D0       | XGPIOA[9]  |     |                   |      |         |            |          |
| <div className='green'>25</div> | SD_SD0_CLK      | XGPIOA[7]  |     |                   |      |         |            |          |
| <div className='green'>26</div> | SD_SD0_D2       | XGPIOA[11] |     |                   |      |         |            |          |
| <div className='green'>27</div> | SD_SD0_D3       | XGPIOA[12] |     |                   |      |         |            |          |
| <div className='green'>28</div> | XGPIOB_22       | XGPIOB[22] | 470 | UART2_RX          |      |         |            |          |
| <div className='green'>29</div> | SD_PWR_EN       |            |     |                   |      |         |            |          |
| <div className='green'>30</div> | UART0_RX        | PWR_GPIO[0]| 352 | UART2_TX          | PWM8 |         | LCD_PWM    |          |
| <div className='green'>31</div> | UART0_TX        | XGPIOA[16] | 496 |UART0_TX/UART1_TX  | PWM4 |         |            |          |
| <div className='green'>32</div> | XGPIOA_18       | XGPIOA[18] | 498 |UART1_RX/UART1_CTS | PWM6 |JTAG_TCK |            |          |
| <div className='green'>33</div> | XGPIOA_19       | XGPIOA[19] | 499 |UART1_TX/UART1_RTS | PWM7 |JTAG_TMS |            |          |
| <div className='green'>34</div> | XGPIOA_30       | XGPIOA[30] |     |                   |      |         |            |          |
| <div className='green'>35</div> | PWR_VBAT_DET    |            |     |                   |      |         |            |          |
| <div className='green'>36</div> | LCD_RST         | PWR_GPIO[2]| 354 |                   | PWM10|         | LCD_RST    | I2C2_SDA |
| <div className='green'>37</div> | LCD_PWR_CT      |            |     |                   |      |         |            |          |
| <div className='green'>38</div> | LCD_PWM         |            |     |                   |      |         |            |          |
| <div className='green'>39</div> | I2C_SENSOR1_SDA |PWR_GPIO[13]|     |                   |      |         |            |          |
| <div className='green'>40</div> | I2C_SENSOR1_SCL |PWR_GPIO[12]|     |                   |      |         |            |          |
| <div className='green'>41</div> | XGPIOA_20       | XGPIOA[20] | 500 |                   |      |JTAG_TRST|            |          |
| <div className='green'>42</div> | XGPIOA_29       | XGPIOA[29] |     |                   |      |         |            |          |
| <div className='green'>43</div> | XGPIOA_28       | XGPIOA[28] | 508 | UART2_TX/UART1_TX |      |         |            |          |
| <div className='green'>44</div> | VDD_BAT         |            |     |                   |      |         |            |          |

</div>

<div className='gpio_style' style={{ overflow :"auto"}} >

| PIN                             | NAME            | SG2000     | NUM | UART              | PWM  | SPI     |    I2C     |
|:-------------------------------:|:----------------|:-----------|:---:|:----------------- |:-----|:--------|:-----------|
| <div className='green'>45</div> |  PWM0_BUCK      | XGPIOB[0]  |     |                   |      |         |            |
| <div className='green'>46</div> |  VBUS_EN        | XGPIOB[5]  |     |                   |      |         |            |
| <div className='green'>47</div> |  UPDATE         | XGPIOB[4]  |     |                   |      |         |            |
| <div className='green'>48</div> |  VBUS_DET       | XGPIOB[6]  |     |                   |      |         |            |
| <div className='green'>49</div> |  EPHY_LNK_LED   | PWR_GPIO[6]|     |                   |      |         |            |
| <div className='green'>50</div> |  EPHY_SPD_LED   | PWR_GPIO[8]|     |                   |      |         |            |
| <div className='green'>51</div> |  XGPIOB_12      | XGPIOB[12] | 460 |   UART2_RX        | PWM2 |         |   I2C1_SCL |
| <div className='green'>52</div> |  XGPIOB_11      | XGPIOB[11] | 459 |   UART2_TX        | PWM1 |         |   I2C1_SDA |
| <div className='green'>53</div> |XGPIOB_13/SPI3_SDO| XGPIOB[13]| 461 |                   | PWM3 |SPI3_SDO |   I2C2_SCL |
| <div className='green'>54</div> |XGPIOB_15/SPI3_SCK| XGPIOB[15]| 463 |   UART2_TX        |      |SPI3_SCK |            |
| <div className='green'>55</div> |XGPIOB_14/SPI3_SDI| XGPIOB[14]| 462 |                   |      |SPI3_SDI |   I2C2_SDA |
| <div className='green'>56</div> |XGPIOB_16/SPI3_CS | XGPIOB[16]| 464 |   UART2_RX        |      |SPI3_CS  |            |
| <div className='green'>57</div> |ADC1             | XGPIOB[3]  | 451 |                   |      |         |            |
| <div className='green'>58</div> |ADC2             | XGPIOB[2]  | 450 |   UART3_RX        |PWM13 |         |   I2C4_SDA |
| <div className='green'>59</div> |ADC3             | XGPIOB[1]  | 449 |   UART3_TX        |PWM12 |         |   I2C4_SCL |
| <div className='green'>60</div> |ARM_RISV_SWITCH  | XGPIOB[23] |     |                   |      |         |            |
| <div className='green'>61</div> |EPHY_RXP         | XGPIOB[24] |     |                   |      |         |            |
| <div className='green'>62</div> |EPHY_RXN         | XGPIOB[25] |     |                   |      |         |            |
| <div className='green'>63</div> |EPHY_TXP         | XGPIOB[26] |     |                   |      |         |            |
| <div className='green'>64</div> |EPHY_TXN         | XGPIOB[27] |     |                   |      |         |            |
| <div className='green'>65</div> |USB_DM           |            |     |                   |      |         |            |
| <div className='green'>66</div> |USB_DP           |            |     |                   |      |         |            |

</div>

<div className='gpio_style' style={{ overflow :"auto"}} >

| PIN                             | NAME              | SG2000     | NUM | UART              | PWM  | MIPI DSI   | I2C      |
|:-------------------------------:|:------------------|:-----------|:---:|:----------------- |:-----|:---------- |:---------|
| <div className='green'>67</div> |XGPIOB_17/I2C1_SDA | XGPIOB[17] |     |                   |      |            |          |
| <div className='green'>68</div> |XGPIOB_18/I2C1_SCL | XGPIOB[18] | 466 |                   |      |            | I2C1_SCL |
| <div className='green'>69</div> |XGPIOB_19          | XGPIOB[19] | 467 |  UART2_TX         | PWM2 |            |          |
| <div className='green'>70</div> |XGPIOB_20/I2C4_SCL | XGPIOB[20] | 468 |  UART2_TX         | PWM3 |            | I2C4_SCL |
| <div className='green'>71</div> |XGPIOB_21/I2C4_SDA | XGPIOB[21] | 469 |                   |      |            | I2C4_SDA |
| <div className='green'>72</div> |MIPI0_DN5          | XGPIOC[0]  |     |                   |      |            | I2C4_SDA |
| <div className='green'>73</div> |MIPI0_DP5          | XGPIOC[1]  |     |                   |      |            |          |
| <div className='green'>74</div> |MIPI0_DN4          | XGPIOC[2]  |     |                   |      |            |          |
| <div className='green'>75</div> |MIPI0_DP4          | XGPIOC[3]  |     |                   |      |            |          |
| <div className='green'>76</div> |MIPI0_DN3          | XGPIOC[4]  |     |                   |      |            |          |
| <div className='green'>77</div> |MIPI0_DP3          | XGPIOC[5]  |     |                   |      |            |          |
| <div className='green'>78</div> |MIPI0_DN0          | XGPIOC[10] |     |                   |      |            |          |
| <div className='green'>79</div> |MIPI0_DP0          | XGPIOC[11] |     |                   |      |            |          |
| <div className='green'>80</div> |MIPI0_DN1          | XGPIOC[8]  |     |                   |      |            |          |
| <div className='green'>81</div> |MIPI0_DP1          | XGPIOC[9]  |     |                   |      |            |          |
| <div className='green'>82</div> |MIPI0_DN2          | XGPIOC[6]  |     |                   |      |            |          |
| <div className='green'>83</div> |MIPI0_DP2          | XGPIOC[7]  |     |                   |      |            |          |
| <div className='black'>84</div> |GND                |            |     |                   |      |            |          |
| <div className='green'>85</div> |MIPI_TX_4N         | XGPIOC[18] | 434 |                   |      | MIPI_TX_3N |          |
| <div className='green'>86</div> |MIPI_TX_4P         | XGPIOC[19] | 435 |                   |      | MIPI_TX_3P |          |
| <div className='green'>87</div> |MIPI_TX_3N         | XGPIOC[20] | 436 |                   |      | MIPI_TX_2N |          |
| <div className='green'>88</div> |MIPI_TX_3P         | XGPIOC[21] | 437 |                   |      | MIPI_TX_2P |          |

</div>

## Duo Module 01 评估板引脚分配

<Image src='/docs/duo/dm01/dm01-evb-pinout.webp' maxWidth='70%' align='left' />

### 26 PIN 排针

`26 PIN 排针` 上的 GPIO 使用 3.3V 逻辑电平。

<div className='gpio_style' style={{ overflow :"auto"}} >

| SPI      | PWM  | I2C      | UART     | NUM | SG2000     | NAME  | PIN                              | PIN                             | NAME     | SG2000     | NUM | UART               | PWM  | SPI     | JTAG      |
|:---------|:-----|:---------|:---------|:---:|:-----------|------:|:--------------------------------:|:-------------------------------:|:---------|:-----------|:---:|:-------------------|:-----|:--------|:----------|
|          |      |          |          |     |            | 3V3   | <div className='orange'>1</div>  | <div className='red'>2</div>    | VSYS(5V) |            |     |                    |      |         |           |
|          | PWM3 | I2C4_SCL |          | 468 | XGPIOB[20] | B20   | <div className='green'>3</div>   | <div className='red'>4</div>    | VSYS(5V) |            |     |                    |      |         |           |
|          |      | I2C4_SDA |          | 469 | XGPIOB[21] | B21   | <div className='green'>5</div>   | <div className='black'>6</div>  | GND      |            |     |                    |      |         |           |
|          |      | I2C1_SCL |          | 466 | XGPIOB[18] | B18   | <div className='green'>7</div>   | <div className='green'>8</div>  | A16      | XGPIOA[16] | 496 | UART0_TX/UART1_TX  | PWM4 |         |           |
|          |      |          |          |     |            | GND   | <div className='black'>9</div>   | <div className='green'>10</div> | A17      | XGPIOA[17] | 497 | UART0_RX/UART1_RX  | PWM5 |         |           |
|          | PWM1 | I2C1_SDA | UART2_TX | 459 | XGPIOB[11] | B11   | <div className='green'>11</div>  | <div className='green'>12</div> | B19      | XGPIOB[19] | 467 | UART2_TX           | PWM2 |         |           |
|          | PWM2 | I2C1_SCL | UART2_RX | 460 | XGPIOB[12] | B12   | <div className='green'>13</div>  | <div className='black'>14</div> | GND      |            |     |                    |      |         |           |
|          |      |          | UART2_RX | 470 | XGPIOB[22] | B22   | <div className='green'>15</div>  | <div className='green'>16</div> | A20      | XGPIOA[20] | 500 |                    |      |         | JTAG_TRST |
|          |      |          |          |     |            | 3V3   | <div className='orange'>17</div> | <div className='green'>18</div> | A19      | XGPIOA[19] | 499 | UART1_TX/UART1_RTS | PWM7 |         | JTAG_TMS  |
| SPI3_SDO | PWM3 | I2C2_SCL |          | 461 | XGPIOB[13] | B13   | <div className='green'>19</div>  | <div className='black'>20</div> | GND      |            |     |                    |      |         |           |
| SPI3_SDI |      | I2C2_SDA |          | 462 | XGPIOB[14] | B14   | <div className='green'>21</div>  | <div className='green'>22</div> | A18      | XGPIOA[18] | 498 | UART1_RX/UART1_CTS | PWM6 |         | JTAG_TCK  |
| SPI3_SCK |      |          | UART2_TX | 463 | XGPIOB[15] | B15   | <div className='green'>23</div>  | <div className='green'>24</div> | B16      | XGPIOB[16] | 464 | UART2_RX           |      | SPI3_CS |           |
|          |      |          |          |     |            | GND   | <div className='black'>25</div>  | <div className='green'>26</div> | A28      | XGPIOA[28] | 508 | UART2_TX/UART1_TX  |      |         |           |

</div>

### 蓝色 LED 引脚

<div className='gpio_style'>

| NAME                            | SG2000     | NUM |
|:-------------------------------:|:----------:|:---:|
| <div className='blue'>LED</div> | XGPIOA[29] | 509 |

</div>

### 摄像头接口

Duo Module 01 评估板有两个 CSI 摄像头接连器：

- J8 是 16 PIN 间距为 0.5mm 与 Duo 和 Duo256M 摄像头兼容的连接器，可以直接使用 [CAM-GC2083](https://milkv.io/zh/docs/duo/camera/gc2083) 摄像头。
- J10 是 15 PIN 间距为 1.0mm 与树莓派摄像头接口兼容的连接器，目前可以支持在树莓派上使用的 OV5647 摄像头。

<Image src='/docs/duo/dm01/dm01-evb-csi.webp' maxWidth='70%' align='left' />

注意，J8 接口使用的 I2C 为 I2C3，J10 接口使用的 I2C 为 I2C2，使用时注意检查引脚复用配置。

#### J8 接口 FPC 线序

<div className='gpio_style'>

| J8 | Description         |
|:--:|:--------------------|
| 1  | GND                 |
| 2  | MIPI0_DN0           |
| 3  | MIPI0_DP0           |
| 4  | GND                 |
| 5  | MIPI0_DN1           |
| 6  | MIPI0_DP1           |
| 7  | GND                 |
| 8  | MIPI0_CKN           |
| 9  | MIPI0_CKP           |
| 10 | GND                 |
| 11 | SENSOR_RSTN0 (1.8V) |
| 12 | SENSOR_CLK0  (1.8V) |
| 13 | I2C3_SCL     (1.8V) |
| 14 | I2C3_SDA     (1.8V) |
| 15 |                     |
| 16 | 3V3                 |

</div>

#### J10 接口 FPC 线序

<div className='gpio_style'>

|J10 | Description          |
|:--:|:---------------------|
| 1  | 3V3                  |
| 2  | I2C2_SDA     (3.3V)  |
| 3  | I2C2_SCL     (3.3V)  |
| 4  | SENSOR_CLK1  (3.3V)  |
| 5  | SENSOR_RSTN1 (3.3V)  |
| 6  | GND                  |
| 7  | MIPI0_DP5 (CAM1_CP)  |
| 8  | MIPI0_DN5 (CAM1_CN)  |
| 9  | GND                  |
| 10 | MIPI0_DP4 (CAM1_DP1) |
| 11 | MIPI0_DN4 (CAM1_DN1) |
| 12 | GND                  |
| 13 | MIPI0_DP3 (CAM1_DP0) |
| 14 | MIPI0_DN3 (CAM1_DN0) |
| 15 | GND                  |

</div>

### POE 接口

<Image src='/docs/duo/dm01/dm01-evb-poe.webp' maxWidth='70%' align='left' />

<div className='gpio_style'>

| POE Pin | Description |
|:-------:|:-----------:|
| 1       | VA-         |
| 2       | VA+         |
| 3       | VB+         |
| 4       | VB-         |

</div>

### ADC 接口

<Image src='/docs/duo/dm01/dm01-evb-adc.webp' maxWidth='70%' align='left' />

<div className='gpio_style'>

| ADC Pin | Description |
|:-------:|:-----------:|
| 1       | GND         |
| 2       | 3V3         |
| 3       | 1V8         |
| 4       | ADC1        |
| 5       | ADC2        |
| 6       | ADC3        |

</div>

### MIPI DSI 屏幕接口

<Image src='/docs/duo/dm01/dm01-evb-lcd.webp' maxWidth='70%' align='left' />

<div className='gpio_style'>

| LCD Pin | Description  | Level |
|:-------:|:-------------|:------|
| 1       | VDD3V3       | 3.3V  |
| 2       | IOVCC1V8-3V3 | 1.8V  |
| 3       | SENSOR-INT   |       |
| 4       | RESET        | 1.8V  |
| 5       | NC           |       |
| 6       | GND1         |       |
| 7       | MIPI-0N      |       |
| 8       | MIPI-0P      |       |
| 9       | GND2         |       |
| 10      | MIPI-1N      |       |
| 11      | MIPI-1P      |       |
| 12      | GND3         |       |
| 13      | MIPI-CKN     |       |
| 14      | MIPI-CKP     |       |
| 15      | GND4         |       |
| 16      | MIPI-2N      |       |
| 17      | MIPI-2P      |       |
| 18      | GND5         |       |
| 19      | MIPI-3N      |       |
| 20      | MIPI-3P      |       |
| 21      | GND6         |       |
| 22      | GND7         |       |
| 23      | TP-RESET     | 3.3V  |
| 24      | TP-VCC       | 3.3V  |
| 25      | TP-INT       | 3.3V  |
| 26      | TP-SDA       | 3.3V  |
| 27      | TP-SCL       | 3.3V  |
| 28      | GND8         |       |
| 29      | GND9         |       |
| 30      | VCC3V31      | 3.3V  |
| 31      | VCC3v32      | 3.3V  |
| 32      | GND11        |       |
| 33      | GND12        |       |
| 34      | LED-1        |       |
| 35      | LED-         |       |
| 36      | NC           |       |
| 37      | NC           |       |
| 38      | LED+1        |       |
| 39      | LED+         |       |

</div>

### RTC 供电接口

<Image src='/docs/duo/dm01/dm01-evb-rtc.webp' maxWidth='70%' align='left' />

<div className='gpio_style'>

| ADC Pin | Description |
|:-------:|:-----------:|
| 1       | GND         |
| 2       | Vbat        |

</div>

### 音频接口

<Image src='/docs/duo/dm01/dm01-evb-audio.webp' maxWidth='70%' align='left' />

<div className='gpio_style'>

| MIC Pin | Description |
|:-------:|:-----------:|
| 1       | MIC IN      |
| 2       | GND         |

</div>

## Duo Module 01 评估板使用指引

### RISC-V 与 ARM 切换

Duo Module 01 的大核可以选择使用 RISC-V 或者 ARM，可以通过评估板上的切换开关来设置，如果您在使用中发现评估板不能正常启动，请先检查该切换开关和使用的固件是否一致。

<Image src='/docs/duo/dm01/dm01-evb-switch.webp' maxWidth='70%' align='left' />

如果连接了调试串口，可以在第一行开机日志中看到，以 `C` 开头时代表从 RISC-V 核启动，以 `B` 开头时代表从 ARM 核启动。

- RISC-V:
  ```
  C.SCS/0/0.C.SCS/0/0.WD.URPL.USBI.USBW
  ```
- ARM:
  ```
  B.SCS/0/0.WD.URPL.B.SCS/0/0.WD.URPL.USBI.USBW
  ```

### USB Type A 接口的使用

评估板的 USB 2.0 Type A 接口与 Type C 接口的 USB 功能是二选一的，不可以同时使用。默认固件配置的是 Type C 口的 USB 网口(USB-NCM)功能，如果需要切换为 Type A 口的 USB 2.0 HOST 口接 U 盘等设备使用，需要执行以下命令：

~~~
ln -sf /mnt/system/usb-host.sh /mnt/system/usb.sh
sync
~~~
然后执行 `reboot` 命令或重新上电使其生效。

比如 USB A 口接入 U 盘后，可以用 `ls /dev/sd*` 查看是否有检测到设备。

挂载到系统中查看 U 盘中的内容(以/dev/sda1为例)：
```
mkdir /mnt/udisk
mount /dev/sda1 /mnt/udisk
```
查看 `/mnt/udisk` 目录中的内容是否符合预期：
```
ls /mnt/udisk
```

卸载U盘的命令：
```
umount /mnt/udisk
```

想恢复 Type C 口 的 USB 网卡(USB-NCM)功能时，执行：
~~~
rm /mnt/system/usb.sh
ln -sf /mnt/system/usb-ncm.sh /mnt/system/usb.sh
sync
~~~
然后执行 `reboot` 命令或重新上电使其生效。

:::tip
Duo Module 01 评估板有板载以太网接口，所以 Type C 口的 USB 网口(USB-NCM)可以不用，一直保持切换为 A 口的 USB 2.0 Host 功能。
:::

### 固定网口 MAC 地址

Duo Module 01 评估板以太网口 MAC 地址是随机分配的，这可能会导致每次重启之后，路由器为网口分配的 IP 地址会变，为了解决这个问题，可以使用如下命令配置一个固定的 MAC 地址:

:::tip
**替换命令中的 MAC 地址为你想使用的地址，另外注意在同一网段中，不能出现重复的 MAC 地址**
:::

```
echo "pre-up ifconfig eth0 hw ether 78:01:B3:FC:E8:55" >> /etc/network/interfaces && sync
```
然后执行 reboot 命令或重新上电使其生效。

### UART 串口控制台

Duo Module 01 评估板上有预留 UART 调试串口，可以查看系统的启动日志，也可以在系统启动后登陆到控制台，执行一些终端命令。

#### USB-TTL 串口线

Duo 系列调试串口电平为 3.3V。

常见的 USB 转 TTL 串口线的引脚定义如下：

<Image src='/docs/common/usb2ttl.webp' maxWidth='100%' align='left' />

#### 连接串口

如下图所示，连接 USB 到 TTL 串口线，不要连接红线。

<div className='gpio_style'>

| Milk-V DouS | \<---> | USB 转 TTL 串口 |
| ----------- | ------ | -------------- |
| GND (pin 6) | \<---> | 黑色线          |
| TX (pin  8) | \<---> | 白色线          |
| RX (pin 10) | \<---> | 绿色线          |

</div>

<Image src='/docs/duo/dm01/dm01-evb-uart.webp' maxWidth='100%' align='left' />

默认的串口参数如下：

```
baudrate: 115200
data bit: 8
stop bit: 1
parity  : none
flow control: none
```

### WIFI 配置

#### 方法一

编辑如下文件，替换 `ssid` 和 `psk` 为要连接的 WIFI 账号和密码：

```python {6,7} title="/etc/wpa_supplicant.conf"
ctrl_interface=/var/run/wpa_supplicant
ap_scan=1
update_config=1

network={
  ssid="wifi_test"
  psk="12345678"
  key_mgmt=WPA-PSK
}
```

再执行如下命令：

```bash
wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant.conf
```
即可连接 WIFI，连接之后可以通过 `ifconfig` 或者 `ip a` 命令查看分配的 IP 地址。

如果需要开机自动连接 WIFI，可以把以下命令放到 `/mnt/system/auto.sh` 文件中。

```bash
interface="wlan0"
max_attempts=100
attempt=0
log_file="/var/log/auto.sh.log"

# Continuously attempt to detect if the interface exists, up to $max_attempts times
echo "start auto.sh" > "$log_file"
while [ $attempt -lt $max_attempts ]; do
    # Check if the wlan0 interface exists
    ip link show "$interface" > /dev/null 2>&1
    if [ $? -eq 0 ]; then
        echo "$(date +'%Y-%m-%d %H:%M:%S') $interface interface exists, starting wpa_supplicant..." >> "$log_file"
        wpa_supplicant -B -i "$interface" -c /etc/wpa_supplicant.conf >> "$log_file"
        break  # Exit the loop if the interface is found
    else
        echo "$(date +'%Y-%m-%d %H:%M:%S') $interface interface not found, waiting..." >> "$log_file"
        sleep 1  # Wait for 1 second before checking again
        attempt=$((attempt + 1))  # Increment the attempt counter
    fi
done

# If the maximum number of attempts is reached and the interface still not found, output an error message
if [ $attempt -eq $max_attempts ]; then
    echo "$(date +'%Y-%m-%d %H:%M:%S') Interface $interface not found after $max_attempts attempts" >> "$log_file"
fi
```

### 固定 WIFI MAC 地址

Duo Module 01 WIFI MAC 地址是随机分配的，这可能会导致每次重启之后，路由器为 WIFI 分配的 IP 地址会变，可以使用如下命令为 WIFI 配置一个固定的 MAC 地址：

:::tip
**替换命令中的 MAC 地址为你想使用的地址，另外注意在同一网段中，不能出现重复的 MAC 地址**
:::

```bash
echo "MAC_ADDR=11:22:33:44:55:66" > /mnt/system/firmware/aic8800/rwnx_settings.ini && sync
```

然后执行 reboot 命令或重新上电使其生效。

### eMMC 版本固件烧录

Duo Module 01 eMMC 版本出厂未烧录固件，需要使用 PC 通过 USB 接口烧录。

:::tip
使用 Windows 下的 USB 烧录工具支持 eMMC 固件版本为 [V1.1.2](https://github.com/milkv-duo/duo-buildroot-sdk/releases/tag/Duo-V1.1.2) 或[更新的版本](https://github.com/milkv-duo/duo-buildroot-sdk/releases)。
:::

#### Windows 环境下烧录

1. 安装驱动

   下载 USB 驱动安装工具：[CviUsbDownloadInstallDriver.zip](https://github.com/milkv-duo/duo-buildroot-sdk/releases/download/Duo-V1.1.0/CviUsbDownloadInstallDriver.zip)。下载后解压安装即可。

2. 下载烧录工具

   下载 Windows 下的命令行烧录工具 [CviBurn_v2.0_cli_windows.zip](https://github.com/milkv-duo/duo-buildroot-sdk/releases/download/Duo-V1.1.0/CviBurn_v2.0_cli_windows.zip)，下载后解压。

3. 下载固件

   Duo Module 01 的固件与 DuoS 的固件通用。下载 DuoS eMMC 最新版本的固件，当前是 [milkv-duos-emmc-v1.1.2-2024-0801.zip](https://github.com/milkv-duo/duo-buildroot-sdk/releases/download/Duo-V1.1.2/milkv-duos-emmc-v1.1.2-2024-0801.zip)，可以在烧录工具 `CviBurn_v2.0_cli_windows` 目录下新建 rom 文件夹，并将下载好的 eMMC 固件压缩包解压到 rom 目录下，此时烧录工具的目录结构如下：

   ```
   └───CviBurn_v2.0_cli_windows
    │   cv_dl_magic.bin
    │   usb_dl.exe
    └───rom
        │   boot.emmc
        │   fip.bin
        │   partition_emmc.xml
        │   rootfs_ext4.emmc
        |   ...
   ```

   在 Windows 的终端中，`CviBurn_v2.0_cli_windows` 目录下执行烧录命令：

   ```
   .\usb_dl.exe -s linux -c cv181x -i .\rom
   ```

   *也可以把固件放到其他目录，通过命令中的 -i 参数指定到对应的目录即可。*

   显示等待 USB 连接的信息：

   <Image src='/docs/duo/duos/duos-emmc-install-01.webp' maxWidth='100%' align='left' />

   用 **Type-C 数据线** 连接评估板 和 PC （注意，目前如果评估板有插 SD 卡，请先将 SD 卡取下），评估板会自动上电进入烧录模式，PC 端会实时显示烧录进度：

   ```
   [INFO] Waiting for USB device connection: ---
   [INFO] found usb device vid=0x3346 pid=0x1000
   [INFO] downloading file: .\rom\boot.emmc
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 3384664/213100824(1%)
   [INFO] downloading file: .\rom\rootfs_ext4.emmc
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 20161944/213100824(9%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 36939224/213100824(17%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 53716504/213100824(25%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 70493784/213100824(33%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 87271064/213100824(40%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 104048344/213100824(48%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 120825624/213100824(56%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 137602904/213100824(64%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 154380184/213100824(72%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 171157464/213100824(80%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 187934744/213100824(88%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 204712024/213100824(96%)
   [INFO] CVI_USB_PROGRAM
   [INFO] updated size: 213100696/213100824(99%)
   [INFO] USB download complete
   ```

   烧录完成后，评估板会自动重启，开机后看到评估板上的蓝色 LED 闪烁，说明系统已经正常启动，烧录成功。

### eMMC 擦除

如果需要将 eMMC 恢复到初始状态，请参考以下命令清除 eMMC 数据（请提前备份好eMMC中的重要文件）：

- 解除 readonly
  ```
  echo 0 > /sys/block/mmcblk0boot0/force_ro
  echo 0 > /sys/block/mmcblk0boot1/force_ro
  ```
- 擦除
  ```
  dd if=/dev/zero of=/dev/mmcblk0boot0 bs=1M count=4
  dd if=/dev/zero of=/dev/mmcblk0boot1 bs=1M count=4
  ```

## 硬件资料

### 其他

[https://github.com/milkv-duo/duo-files/tree/main/duo-module-01](https://github.com/milkv-duo/duo-files/tree/main/duo-module-01)
