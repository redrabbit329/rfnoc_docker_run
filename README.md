# rfnoc_docker_run
=====================
RFNoC Docker Env. Run Command
---------------------

## docker image run

in CentOS7,

1. docker image List 확인 : 
>$ docker images

2. 구동중인 Container 혹은 History확인 :
>$ docker ps -a
  
3. 불필요한 Conatainer Stop 혹은 제거 :
>$ docker stop <Container이름>
  
4. 불필요한 Container 제거 :
>$ docker rm <Conatainer이름>
  
5. 구동할 도커 이미지로부터 컨테이너 생성하기
>$ docker run <옵션> <이미지이름> <실행할 파일>
>$ docker run -it --name Redrabbit_Nick_Name Original_Image_Name_and_TAG /bin/bash

6. 기 생성되어 있는 컨테이너 실행하기
>$ docker exec Container_Nick_Name /bin/bash
  
7. 사용하지 않는 Docker Image 삭제하기
>$ docker rmi <이미지이름>:<태그>
