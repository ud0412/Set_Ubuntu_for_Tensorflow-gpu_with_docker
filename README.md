# Set_Ubuntu_for_Tensorflow-gpu_with_docker

tensorflow-gpu 를 docker image 로 설치하기

1. Ubuntu 18.04 를 설치 한다.
  * docker image 이기 때문에 ubuntu version 에 의존하지 않지만 nvidia driver 를 최신으로 설치하기 위해 18.04 를 설치 함.

2. nvidia driver 를 설치
  * cuda toolkit 을 설치하지 않기 때문에 nvidia driver 를 설치해 주어야 함.
  * ubuntu-drivers 의 결과중 최신을 설치해 줌.
  <pre><code>
  $ ubuntu-drivers devices
  $ sudo apt install nvidia-396
</code></pre>
  * reboot
  * reboot 후 아래 명령어로 drvier 설치 확인
  <pre><code>
  $nvidia-smi 
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 396.37                 Driver Version: 396.37                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 1060    Off  | 00000000:01:00.0 Off |                  N/A |
| N/A   50C    P2    27W /  N/A |    326MiB /  6078MiB |      1%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1040      G   /usr/lib/xorg/Xorg                           187MiB |
|    0      1724      G   compiz                                       136MiB |
+-----------------------------------------------------------------------------+
  </code></pre>
3. docker-ce 설치
  - https://www.tensorflow.org/install/docker
  <pre><code>
  $ sudo apt-get remove docker docker-engine docker.io containerd runc
  $ sudo apt-get update
  $ sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
  $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  $ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
  $ sudo apt-get update
  $ sudo apt-get install docker-ce docker-ce-cli containerd.io
</code></pre>
4. nvidia docker 설치
  - https://github.com/NVIDIA/nvidia-docker
<pre><code>
  $ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
  $ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
  $ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
  $ sudo apt-get update
  $ sudo apt-get install -y nvidia-docker2
  $ sudo pkill -SIGHUP dockerd
</code></pre>
5. tensorflow image download & test
<pre><code>
  $ docker run --runtime=nvidia -it --rm tensorflow/tensorflow:latest-gpu python -c "import tensorflow as tf; tf.enable_eager_execution(); print(tf.reduce_sum(tf.random_normal([1000, 1000])))"
</code></pre>
