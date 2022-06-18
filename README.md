# 小麻雀处理器

### 介绍
小麻雀处理器(SparrowRV)是一款单核32位，支持RV32IM指令集的嵌入式处理器。它结构精简，RTL代码中有非常详细的注释，没有繁杂冗余的结构，代码整体的可读性强。小麻雀处理器是我学习的一个里程碑。  

**设计指标：**  
- 支持RV32IM指令集，未来可能会制作多核结构  
- 支持CSR，支持中断，仅支持机器模式  
- 哈佛结构，指令存储器映射至存储器空间  
- 支持C语言  
- 支持带有阻塞功能的总线  
- JTAG调试支持  
- 片外Flash启动支持  

### 设计进度
```
SoC RTL
 ├─内核
 │   ├─译码执行 (Debug 90%)
 │   ├─iram (OK)
 │   ├─CSR  (Debug 0%)
 │   ├─寄存器组 (OK)
 │   ├─总线接口 (Debug 60%)
 │   ├─中断控制 (10%)
 │   └─多周期指令控制 (Debug 80%)
 ├─外设 (未进行)
 └─调试 (未进行)

软件部分
 ├─指令仿真 (OK)
 └─BSP (未进行)

当前任务
- 设计中断控制器
```

### 开发工具
- 处理器RTL设计采用Verilog-2001。此版本代码密度更高，可读性更强，并且受到综合器的广泛支持。  
- 处理器RTL验证采用System Verilog-2005。此版本可以满足仿真需求，语法受到仿真器的广泛支持。   
- 数字逻辑仿真采用iverilog。开源免费的跨平台HDL仿真器。  
- 辅助脚本采用 Batchfile批处理(Win)/Makefile(Linux) + Python3。发挥各种脚本语言的优势，最大程度地简化操作。  
- 所有文本采用UTF-8编码，具备良好的多语言和跨平台支持。  

### 仿真
目前仅支持内核仿真，且只配置了Windows下的批处理脚本，makefile脚本待开发。需要安装iverilog、python3，环境配置可参考[大黄鸭处理器](https://gitee.com/xiaowuzxc/Yduck-processor/)  
双击`tb/run.bat`即可启动脚本，输入单个数字或符号即可执行对应项目。目前仅支持命令`1`和`c`  
执行ISA测试，可以对内核进行仿真，依次测试机器模式下RV32IM的指令，并收集测试结果。

### 杂谈:个人心路历程
本项目开坑，是我学习数字逻辑设计从量变到质变的又一个转折点。  
我以前搞嵌入式，全靠自己摸索，当时觉得单片机可有意思了，从STC到STM32，还有经典的ESP8266，可以自己做各种小玩意。不过，再有意思的东西，玩上好几年，新鲜感没了，也就腻了，觉得是时候跳出这个圈子了。  
我学习数字逻辑设计的起点是一个40包邮的ZYNQ7010矿板。这板子买不了吃亏买不了上当，又能玩PL/FPGA部分，也能玩PS/Cortex-A9硬核。后来随着技术力的提升，我开始参加竞赛，玩各个厂家的FPGA器件，尝试iverilog,VCS,AlpsMS等各种仿真器，学会了makefile、Python等脚本，一次次挑战自我。  
搞技术的就怕舒适圈。很多时候，调用现成的模块可以带来很大的便利，重复造轮子也确实没有意义，毕竟高复用性是开源的灵魂之一，不必将精力消耗在重复劳动上，~~IP连连看不爽吗~~。但是，会用现成的轮子，不代表不需要有造轮子的能力。要知道，轮子也是人造的，人人都想着调库，技术就难以发展。我的开源仓库里面就有很多轮子，比如说明很详细的异步FIFO、逐次逼近型ADC、CIC/FIR滤波器等。借鉴并复现成熟设计不丢人，毕竟只有吃透了成熟设计才有创新的能力；但是，只想借鉴不想创造，躺在舒适圈里，不是一个工程师该有的想法。借鉴并研究经典设计，在此基础上创造出新的知识或成果，成为后人所学习的”经典设计“，既象征着对技术的不懈追求，也是一种开源精神的传承。  
如果只是为了拿来用，tinyriscv、蜂鸟E203、PicoRV都是非常成熟且优秀的设计，做一个使用者，方便快捷。但是，我是一个不甘于一直做“使用者”的人，如果有可能，我想做开发者，能力不够也可以尝试去修改。我以前搞单片机，开发C语言程序，是“使用者”；我修改tinyriscv和蜂鸟E203的功能和外设，做出自己想要的东西，是“开发者”。同样，我在tinyriscv或蜂鸟E203的基础上进行开发，却是“使用者”；我尝试自己写一个RISC-V处理器，做出自己想要的东西，是“开发者”。  

### 致谢
本项目参考了tinyriscv的RTL设计和Python脚本：https://gitee.com/liangkangnan/tinyriscv  
感谢众多开源软件为我提供了很多好用的工具  
感谢导师对我的支持和理解  
大家的支持是我前进的动力  