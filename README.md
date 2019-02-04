# Set_Ubuntu_for_Tensorflow-gpu_with_docker

tensorflow-gpu 를 docker image 로 설치하기

1. Ubuntu 18.04 를 설치 한다.
  - docker image 이기 때문에 ubuntu version 에 의존하지 않지만 nvidia driver 를 최신으로 설치하기 위해 18.04 를 설치 함.

2. nvidia driver 를 설치
  - cuda toolkit 을 설치하지 않기 때문에 nvidia driver 를 설치해 주어야 함.
  - ubuntu-drivers 의 결과중 최신을 설치해 줌.
  $ ubuntu-drivers devices
  $ sudo apt install nvidia-<version>

3. docker-ce 설치
  - https://www.tensorflow.org/install/docker
  $ sudo apt-get remove docker docker-engine docker.io containerd runc
  $ sudo apt-get update
  $ sudo apt-get install \
                 apt-transport-https \
                 ca-certificates \
                 curl \
                 gnupg-agent \
                 software-properties-common
  $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  $ sudo add-apt-repository \
                 "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
                 $(lsb_release -cs) \
                 stable"
  $ sudo apt-get update
  $ sudo apt-get install docker-ce docker-ce-cli containerd.io

4. nvidia docker 설치
  - https://github.com/NVIDIA/nvidia-docker
  $ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
  $ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
  $ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
                 sudo tee /etc/apt/sources.list.d/nvidia-docker.list
  $ sudo apt-get update
  $ sudo apt-get install -y nvidia-docker2
  $ sudo pkill -SIGHUP dockerd
  
  $ sudo pkill -SIGHUP dockerd
  
