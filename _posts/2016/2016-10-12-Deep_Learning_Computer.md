---
title: "연구실 딥러닝용 컴퓨터 설정"
layout: single
excerpt: "GTX1080 + Ubuntu 14.04"
sitemap: true
permalink: #/Deep_Learning_Computer.html
date: 2016-10-12 16:00:00
tags:
  - Deep Learning
---

### 연구실 컴퓨터 사양
![연구실 컴퓨터](/images/2016-10-12/Lab_computer.png)  
\+ GTX1080

### 주의 사항
- Ubuntu 14.04의 경우 Nvidia Cuda 설치 시 OpenGL이나 nouveau와 충돌하여 로그인 화면에서 무한반복되는 문제가 발생할 수 있다. ([링크](http://ejklike.github.io/2016/01/25/installing-ubuntu-with-nvidia-graphic-card.html))
  - 문제가 생길 경우 Ctrl + Alt + F1을 통해 text mode로 들어가서 그래픽카드 드라이버를 재설치 할 것.


### 설치 순서
1. Ubuntu 14.04 CD 넣고 재부팅 시 F11로 Boot 순서 선택하여 우분투 설치  
1.1 **English**, 키보드는 **Korean** 으로 설정함

2. 설치 후 랜카드 드라이버를 설치해야 인터넷을 설정할 수 있음
 ([출처](http://askubuntu.com/questions/755652/ethernet-not-working-on-ubuntu-14-04-lts))  
2.1 https://downloadcenter.intel.com/download/15817 에서 랜카드 드라이버 다운로드 (e1000e)  
2.2 USB 등을 이용해 적당한 폴더에 파일을 옮김  
2.3 ```tar zxf e1000e-<x.x.x>.tar.gz``` 명령을 이용해 압축을 풀고  
2.4 ```cd e1000e-<x.x.x>/src/``` 폴더로 이동  
2.5 ```sudo make install```을 통해 드라이버 설치  
2.6 ```sudo modprobe e1000e insmod e1000e```  
2.7 오른쪽 위를 잘 찾다보면 인터넷 설정하는 페이지가 나오므로 거기서 ip 맞춰서 설정  
2.8 가끔 apt-get 실행시 접속이 제대로 안 되는 경우가 있으니 우분투 apt-get list를 받아오는 서버를 수정하자. [링크](http://www.javaexpert.co.kr/entry/Ubuntu-%EC%97%90%EC%84%9C-apt-get-update-%EA%B0%80-%EC%95%88%EB%90%A0-%EB%95%8C)  
2.9  ```sudo apt-get update```, ```sudo apt-get upgrade```를 통해 패키지 업데이트를 실행

3. 그래픽카드 드라이버 설치 (현재 연결되어 있는 모니터는 주파수 문제로 드라이버 설치 전엔 안 나온다!)([출처](https://kusemanohar.wordpress.com/2016/07/29/gtx-1080-on-ubuntu-14-04-trusty/))  
3.1 http://www.nvidia.com/Download/index.aspx?lang=en-us 에서 GTX1080, Linux 64bit용 드라이버 다운로드  
3.2 ```sudo apt-get purge nvidia-*``` 명령을 통해 기존 드라이버 삭제 (아마 없음)  
3.3 그냥은 tty로 진입이 안 되므로 ```sudo vi /etc/default/grub``` 로 아래와 같이 수정 ([출처](http://blog.sanguneo.com/17))  
``` "GRUB_CMDLINE_LINUX_DEFAULT="quiet splash" ```  
``` → GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset" ```  
3.4 ```sudo update-grub```을 통해 업데이트를 반영시킴   
3.5 ```sudo reboot```을 통해 재부팅  
3.6 ```CTRL+ALT+F1```을 눌러 tty로 진입  
3.7 ```sudo init 3``` 을 통해 text only mode 설정  
3.8 ```sudo service lightgdm stop```을 통해 그래피컬 인터페이스 끔  
3.9 ```sudo sh ./NVIDIA-Linux-x86_64-367.35.run``` 을 통해 그래픽카드 설치  
( **Issue**: 왜 pre-distributed install이 없다고 뜨는가?)  
3.10 ```sudo reboot``` 을 통해 리붓  

4. Cuda 설치  
4.1 CUDA의 경우 위에서 서술했듯 opengl, nouveau 등과 충돌할 수 있기 때문에 먼저 해당 모듈을 끈다. 터미널에서 ```sudo vi /etc/modprobe.d/blacklist-nouveau.conf ``` 입력을 통해 파일을 만들고 아래 내용을 추가한 뒤 저장한다.
```blacklist nouveau```  
```blacklist lbm-nouveau```  
```options nouveau modeset=0```  
```alias nouveau off```  
```alias lbm-nouveau off```  
4.2 https://developer.nvidia.com/cuda-downloads 에서 CUDA 최신버전을 다운받는다  
4.3 **tty**로 진입해서 ```sudo service lightdm stop``` 으로 그래피컬 인터페이스 끔  
4.4 ```sudo sh cuda_<version>\_linux.run``` 로 쿠다 설치  
4.5 ```reboot```  
4.6 terminal에서 ```gedit .bashrc``` 로 PATH 추가  
```$ export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}```  
```$ export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64\${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}```  
4.7 **tty**에서 gcc 설치 ( ```sudo apt-get install g++``` )  
4.8 cuda sample build  
```cuda-install-samples-8.0.sh ~```  
```cd NVIDIA_CUDA-8.0_samples```  
```make```  
4.9 시간 오래 걸려서 설치가 끝나면 ```samples/1_Utilities/deviceQuery``` 폴더에서 ```./deviceQuery```로 실행해서 결과 확인  

5. CuDNN 설치  
5.1 https://developer.nvidia.com/cudnn 에서 최신버전을 다운로드  (회원가입 필요)  
5.2 cuDNN Library for Linux (압축파일)을 다운받은 뒤 해당 폴더에서 아래 명령을 순차적으로 실행  
```tar xvzf cudnn-x.x-linux-x64-v4.0-prod.tgz```  
```sudo cp cuda/include/cudnn.h /usr/local/cuda/include```  
```sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64```  
```sudo chmod a+r /usr/local/cuda/lib64/libcudnn*```  

6. Theano 설치

7. Tensorflow 설치

8. Caffe 설치



### 이슈
- Theano 이외에 Cafe, Tensorflow 등의 Deep Learning Library를 설치할 것
- Jupyter Notebook 말고 Jupyterhub 설치
