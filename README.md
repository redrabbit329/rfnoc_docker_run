# RFNoC Docker Env. Run Command
---------------------

## RFNoC Docker Image Descriptions :
------------------
--- Ubuntu 18.04 LTS
--- uhd/gr-ettus/uhd-fpga/
--- sdk-cross-compiled version of 

in CentOS7, 기본 명령어

### 1. docker image List 확인 : 
$ docker images

### 2. 구동중인 Container 혹은 History확인 :
$ docker ps -a
  
### 3. 불필요한 Conatainer Stop 혹은 제거 :
$ docker stop <Container이름>
  
### 4. 불필요한 Container 제거 :
$ docker rm <Conatainer이름>
  
### 5. 구동할 도커 이미지로부터 컨테이너 생성하기
$ docker run <옵션> "이미지이름" "실행할 파일"
$ docker run -it --name Redrabbit_Nick_Name Original_Image_Name_and_TAG /bin/bash

### 6. 기 생성되어 있는 컨테이너 실행하기
$ docker exec Container_Nick_Name /bin/bash

(5-6) 그러나 이와 같이 컨테이너를 생성하면, 컨테이너 내에서 생성한 작업의 결과는 컨테이너 종료와 동시에 날라간다.
작업의 결과물을 User folder 내에 유지하기 위해, workspcae를 docker image내에 생성해 두고,
실제 시스템에서 작업공간으로 사용 할 폴더를 도커 컨테이너를 프로세스에 올리면서, 컨테이너의 Device Tree에도 함께 마운트 하면
도커 내에서 작업하는 동안 폴더 안에서 작업한 내용들은 모두 실제 시스템에 붙어있는 내용이므로, 도커가 종료 된 다음에도
작업 한 결과물이 남아서 다음 번에도 동일한 환경을 불러 왔을 때 연속적으로 작업하는 것이 가능하다.
이렇게 하기 위해서는 도커 이미지에서 컨테이너를 불러 올 때, User Work폴더를 컨테이너에 마운트 해줘야 하는데
명령이 좀 길어서...sh script를 사용한다.

작업하고자 하는 폴더를 시스템에 생성해놓고, docker_run.sh파일을 가져와서 (현재 폴더를 마운트하라는 명령이 sh script에 포함되어 있음

$ source docker_run.sh rfnoc:0.6 
$ source <script.sh> <docker image>:<TAG>
그럼 안 붙는다. 왜?

$ docker_run.sh <이미지이름>:<TAG>
  
### 7. Container 작업 종료하고 나가기
$ exit
  
### 8. 사용하지 않는 Docker Image 삭제하기
$ docker rmi <이미지이름>:<태그>


### 


```

~/Projects/RFNoC
source docker_run.sh rfnoc:0.6
// container의 workspace2에 rfnoc폴더가 mount됨
cd rfnoc/src

source /opt/Xilinx/Vivado/2017.4/settings64.sh
source uhd-fpga/usrp3/top/x300/setupenv.sh

 >> Environment successfully initialized.
----------------------------------------------------------------------- 
rfnocmodtool newmod test
cd rfnoc-test
rfnocmodtool add gain
N/ N/ 1111222233334444 / N/ N/ 
mkdir build
cd build
cmake -DUHD_FPGA_DIR=../../uhd-fpga/ ../

>> Performing Test HAVE_WNO_UNUSED_BUT_SET_VARIABLE - Success
>> Configuring done
>> Generating done
>> Build files have been written to : 

make test_tb
make noc_block_gain_tb

>> Checking /Environment
>> Builer Checking Tools..
>> Bibado Simulator 
>> Xsim completed. XSim simulation ran for 
>> BUILDER: Closing project
INFO: [Common 17-206] Exiting Vivado at Mon Apr 13 ~
Built target noc_block_gain_tb
-----------------------------------------------------------------------

```


