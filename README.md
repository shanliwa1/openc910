# IP Readme

  Welcome to C910! Some key directories are shown below.
```
|--C910_RTL_FACTORY/
  |--gen_rtl/     ## Verilog source code of C910
  |--setup/       ## Script to set the environment variables
|--smart_run/     ## RTL simulation environment
  |--impl/        ## SDC file, scripts and file lists for implementation
  |--logical/     ## SoC demo and test bench to run the simulation
  |--setup/       ## GNU tool chain setting
  |--tests/       ## Test driver and test cases
  |--work/        ## Working directory for builds
  |--Makefile     ## Makefile for building and running sim targets
|--doc/           ## The user and integration manual of C910
```


## Toolchain Setup 

You can download the Xuantie GNU tool chain compiled by T-HEAD from the url below:
https://occ.t-head.cn/community/download?id=3948120165480468480

Download pre-built Xuantie-900-gcc-elf-newlib-Vxxxx.tar.gz 

unzip it and put it in /opt/xuantie/ directory.

(1) Clone this repo:
```
git clone git@192.168.100.205:wangy/openc910.git

git checkout verilator-sim 
```

(2) Set environment veriables:

CODE_BASE_PATH and TOOL_EXTENSION will be used in Makefile to build the RTL code and testcase code)

```
cd openc1910/C910_RTL_FACTORY

source ./setup/setup.sh
(This command will set CODE_BASE_PATH as C910_RTL_FACTORY directory)

cd ../smart_run

source ./setup/example_setup.sh
(This command will set TOOL_EXTENSION as /opt/xuantie/bin)

```

## Verilator Simulation Step-by-Step guide


In this step, we aussme you alreay have "Verilator", "GtkWave" and "Xuantie toolchain" intalled on your system.


(1) Compile Verilator, execute following command under ./smart_run directory: 
```
make compile SIM=verilator DUMP=on
```
(This command only need to execute once, unless you modified CPU design files, e.g RTL code.
If you want to dump vcd waveform use DUMP=on)



(2) Build Verilator 
```
make buildVerilator
```
(This command only need to execute once, unless you modified CPU design files, e.g RTL code)

      

(3) Build testcase 
```
make buildcase CASE=hello_world
```
(This command build a C or assembly program, use CASE=xxx to select which program you want to build, you can use make help to see what XXX can be)

      

(4) Run testcase on Verilator 
```
make runVerilator
```
(This command run a application on verilator simulation CPU)


(5) Check waveform file
After execution, there will be a `test.vcd` file under smart_run/work directory.
You can use gtkwave to open it. if there is test.vcd file, you need to rerun make compile
with DUMP=on. 

## Notes

```
The testbench supports Verilator(version is better newer than 4.215),iverilog, vcs and irun to run simulation and you can use Gtkwave or verdi
to open the waveform under ./smart_run/work/ directory.

You can get the debugger, IDE and SDK from the url:https://occ.t-head.cn/community/download?id=575997419775328256
```


## Discussion
    If you are interested in participating in discussions or improving the "openXuantie" cores, you can scan the DingDing QR code below to join the discussion group.
<img src="https://github.com/T-head-Semi/opene902/blob/main/doc/QR_code_openXuantie.png" />


/*Copyright 2019-2021 T-Head Semiconductor Co., Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

 http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

*/
