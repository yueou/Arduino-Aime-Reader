# Arduino-Aime-Reader
使用 Arduino + PN532 + WS2812B 制作的 Aime 读卡器。支持 Felica，banapassport，Aime（Mifare 卡模拟 Felica 是可选功能）。     
通信数据格式参考了 [Segatools]() 和实体读卡器抓包数据，可在 [Example.txt](doc/Example.txt) 和 [nfc.txt](doc/nfc.txt) 查看。   
替换 chunihook.dll 可在控制台输出通信数据，源码在 [sg-cmd.c](tools/sg-cmd.c)。   

#### 使用方法：  
按照 [PN532](https://github.com/elechouse/PN532) 的提示安装库；
Arduino 和 PN532 接好 VCC，GND，SDA，SCL；  
接上 WS2812B 灯条（可选）；  
上传 [ReaderTest](tools/ReaderTest.ino) 测试硬件是否工作正常；  
上传程序。  

打开设备管理器，设置 Arduino 的 COM 号，一些参考如下：  
- SDBT：COM12，支持读取 Felica 和 Aime  
- SDDT/SDEZ：COM1，支持读取 Felica 和 Aime  
- SBZV/SDDF：COM10，支持读取 Felica 和 Aime  
- SDEY：COM2，仅支持读取 Aime  
- SDHD：COM4，支持读取 Felica 和 Aime  

有使用 amdaemon 的，可以参考 config_common.json 内 aime > unit > port,high_baudrate 来确定 COM 号和波特率。  

某些 Arduino 可能需要在游戏主程序连接前给串口发送 DTR/RTS，需要先打开一次 Arduino 串口监视器再启动主程序。  
如果是 SDBT，可以在启动前运行一次 [DTR-RTS.exe](tools/DTR-RTS.exe) 以向 COM1 和 COM12 发送DTR/RTS。  
如果需要向其他端口发送，可以修改 [DTR-RTS.c](tools/DTR-RTS.c) 然后编译。

#### 已测试开发板：  
- SparkFun Pro Micro（ATmega32U4），需要发送 DTR/RTS  
- SparkFun SAMD21 Dev Breakout（ATSAMD21G18）  
- NodeMCU 1.0（ESP-12E + CP2102 & CH340），SDA=D2，SCL=D1  

#### 待办事项：  
- [X] 确认 SDDT 和 SDDF 读取 Felica 情况
- [X] 收集 banapassport 卡结构和读取数据
- [ ] 确认 NDA_06 和 NDA_08 数据结构

#### 引用库：  
- [驱动WS2812B FastLED.h](https://github.com/FastLED/FastLED)    
- [驱动PN532 PN532.h](https://github.com/elechouse/PN532)    
