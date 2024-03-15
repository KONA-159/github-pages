---
title: sitk::ERROR: No ImageJ/Fiji application found.问题解决过程
---

# sitk::ERROR: No ImageJ/Fiji application found.问题解决过程

- 没有安装ImageJ
  - [Fiji (imagej.net)](https://imagej.net/software/fiji/)
  - 安装numpy

- 可能是由于没有配置环境变量导致
  - 修改conda环境变量
    - conda env config vars set SITK_SHOW_COMMAND=/location/Fiji.app/ImageJ-linux64 -n env_name
    - conda env config vars set PATH=$PATH:$SITK_SHOW_COMMAND -n env_name
  - 如果在修改base环境变量
    - 修改~/.bash_profile
    - 添加 export PATH=$PATH:$SITK_SHOW_COMMAND
    - source ~/.bash_profile更新环境变量
  - 直接把Fiji.app丢到python解释器目录下
- 可能是ImageJ缺少JAVA运行时环境导致
  - java --version查看是否安装java
    - apt-get install java（Ubantu）
    - yum install java-1.8.0-openjdk
  - 直接安装ImageJ与jre捆绑版本
    - [下载 (imagej.net)](https://imagej.net/ij/download.html)

- 最后发现是因为simpleitk版本过高
  - 使用conda install -c simpleitk simpleitk=1.2降低版本
    - 出现了ResolvePackageNotFound：Python 3.1
      - 意思是当前python版本过低
        - 这是由于conda 4.10的bug导致，当前python版本为3.10+时，conda会误以为是3.1
          - 解决方法：
            - 升级conda：conda update conda
            - 降低python版本：conda install python=3.7（simpleitk1.2.4与Python3.8以下兼容）
