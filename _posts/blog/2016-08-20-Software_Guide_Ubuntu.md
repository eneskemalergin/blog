---
layout: post
title: Software Guide of Ubuntu 16.04 for my Research
excerpt:
categories: blog
tags: ["Research", "Guide", "Ubuntu"]
published: true
comments: true
share: true
---
Hello everybody, today I am sharing my first guide which is about building my new research computer. This is a small guide for setting up Ubuntu 16.04 and necessary software for my research.

### Specs of my computer

__Operating System and System type / version:__ Ubuntu 16.04.1

__Processor type and speed:__ Intel i5 6600K, 3.5 GHz

__RAM amount:__ 64GB

__GPU:__ Nvidia 1070 gtx, 8GB

__Hard drive size:__ 500GB SSD, 3TB SATA


### Steps to Software Installation/Configuration
- Install Nvidia drivers
  >  

  - ```sudo add-apt-repository ppa:graphics-drivers/ppa```
  - ```sudo apt-get update```
  - ```sudo apt-get install nvidia-367```
  - restart = ```sudo reboot```

- Install CUDA 7.5
  > I am installing CUDA 7.5 because tensorflow does not work with 8.0 yet. We have to use another version of gcc and g++ since 5.4 is not compatible. Also we will install CUDA 7.5 installer for Ubuntu 14.04 version it won't be much difference.

  - ```sudo apt-get install gcc-4.9```
  - ```sudo apt-get install g++-4.9```
  - ```sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 10```
  - ```sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 20```
  - ```sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 10```
  - ```sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 20```
  - ```wget linkToCUDA7.5Installer```
  - ```sudo sh cuda_7.5.18_linux.run --override```

  ```bash
  Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 352.39? ((y)es/(n)o/(q)uit): no
  Install the CUDA 7.5 Toolkit? ((y)es/(n)o/(q)uit): yes
  Enter Toolkit Location [ default is /usr/local/cuda-7.5 ]:
  Do you want to install a symbolic link at /usr/local/cuda? ((y)es/(n)o/(q)uit): yes
  Install the CUDA 7.5 Samples? ((y)es/(n)o/(q)uit): no
  Installing the CUDA Toolkit in /usr/local/cuda-7.5 ...
  ```
  - Then add following to .bashrc
  - ```echo 'export PATH=/usr/local/cuda/bin:$PATH' >> ~/.bashrc```
  - ```echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc```
  - ```source ~/.bashrc```


- Install Cudnn
  - Download source code [here](https://developer.nvidia.com/rdp/form/cudnn-download-survey)
  - ```tar xvf cudnn-7.5-linux-x64-v5.1-prod.tgz```
  - ```sudo cp cuda/include/cudnn.h /usr/local/cuda/include/```
  - ```sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64/```
  - ```sudo chmod a+r /usr/local/cuda/lib64/libcudnn*```

- Install Chrome
  >

  - ```wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb```
  - ```sudo dpkg -i --force-depends google-chrome-stable_current_amd64.deb```
  - ```sudo apt-get install -f```
  - ```rm google-chrome-stable_current_amd64.deb```

  > <span style="color:red">If chrome lags when you highlight or something just go and unchecked Use 'Hardware acceleration if available' in advance settings of chrome settings</span>

- Configure workspaces in Ubuntu

  - system settings > Appearance > Behavior > Check 'Enable Workspaces'
  - If you want to configure new shortcuts:
    - System Settings > Keyboard > Shortcuts > Navigation > You can assign new shortcuts

- Install vim

  - ```sudo apt-get install vim```

- Install git

  - ```sudo apt-get install git```
  - ```git config --global user.name "name"```
  - ```git config --global user.email "email"```

- Install htop
  > It is really nice command line tool to see and control system
  - ```sudo apt-get install htop```



- Install Atom text editor

  - ```sudo add-apt-repository ppa:webupd8team/atom```
  - ```sudo apt-get update```
  - ```sudo apt-get install atom```

- Install a good Theme for Ubuntu
  > It is really nice to have a new look...

  - ```mkdir ~/.icons```
  - ```sudo apt install unity-tweak-tool```
  - ```sudo add-apt-repository ppa:noobslab/icons2```
  - ```sudo apt-get update```
  - ```sudo apt-get install square-icons```
  - Open unity tweak tool
  - Appearance > Icons > select square-light or square-dark

- Install Anaconda Python Distribution
  > Anaconda distribution is really easy Python distributor that I can manage my libraries.

  - Download Anaconda Python 2.7 from [here](https://www.continuum.io/downloads)
  - ```bash Downloads/Anaconda2-4.1.1-Linux-x86_64.sh```

- Install tensorflow with GPU

  - Create virtual machine
  - ```conda create -n tf python=2.7```
  - ```source activate tf```
  - ```pip install --upgrade pip```
  - ```pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-0.10.0rc0-cp27-none-linux_x86_64.whl```


- Install R and RStudio
  > I love R since it's amazing tool for statistics and learning mathematical background of most algorithms. Also Rstudio is really high quality interpreter for R.

  - ```sudo echo "deb http://cran.rstudio.com/bin/linux/ubuntu xenial/" | sudo tee -a /etc/apt/sources.list```
  - ```gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9```
  - ```gpg -a --export E084DAB9 | sudo apt-key add -```
  - ```sudo apt-get update```
  - ```sudo apt-get install r-base r-base-dev```
  - ```sudo apt-get install gdebi-core```
  - ```wget https://download1.rstudio.org/rstudio-0.99.896-amd64.deb```
  - ```sudo gdebi -n rstudio-0.99.896-amd64.deb```
  - ```rm rstudio-0.99.896-amd64.deb```

  > Hey do you know there is a comment section below that you can share your ideas with me?

  > Until next time, be safe...
