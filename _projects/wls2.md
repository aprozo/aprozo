---
layout: distill
title: WSL2
description: How to setup wsl2 environment
tags: programming, wsl2
img: assets/img/Github-Desktop-Wsl2.webp
giscus_comments: false
featured: true
importance: 2
category: programming

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: WSL2 Install
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Python
  - name: VS code extensions (inside WSL2)
#   subsections:
#     - name: VS code extensions


# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }
---



### WSL2 Install
open Windows PowerShell (right click - "Run as administrator")

`wsl --install`  - it will install latest wsl2 Ubuntu version.

If there are any problems, one can download it from Microsoft Store : https://www.microsoft.com/store/productId/9PDXGNCFSCZV?ocid=pdpshare

I would also advice to install [Windows Terminal Preview](https://www.microsoft.com/store/productId/9N8G5RFZ9XK3?ocid=pdpshare)

Then reboot your laptop.


start new UBUNTU terminal, and update some packages (just copy/paste inside the new terminal):


{% highlight bash %}
cd ~
sudo apt-get install dpkg-dev cmake g++ gcc binutils libx11-dev libxpm-dev \
libxft-dev libxext-dev python3 libssl-dev \ 
gfortran libpcre3-dev \
xlibmesa-glu-dev libglew-dev libftgl-dev \
libmysqlclient-dev libfftw3-dev libcfitsio-dev \
graphviz-dev libavahi-compat-libdnssd-dev \
libldap2-dev python3-dev libxml2-dev libkrb5-dev \
libgsl0-dev qtwebengine5-dev -y 

cd ~
mkdir install 
cd install 
wget https://root.cern/download/root_v6.28.06.Linux-ubuntu22-x86_64-gcc11.4.tar.gz
tar -xzvf 	root_v6.28.06.Linux-ubuntu22-x86_64-gcc11.4.tar.gz 
rm  root_v6.28.06.Linux-ubuntu22-x86_64-gcc11.4.tar.gz 
source ~/install/root/bin/thisroot.sh
 
sudo apt-get install firefox xdg-utils sshfs -y 
sudo apt-get install texlive-full -y
sudo apt-get install python3-pip
pip install notebook
export PATH="$HOME/.local/bin:$PATH"
}
{% endhighlight %}


I would also recommend to update your `$HOME/.bashrc` file in your Home directory, one could take an example in this repository.

At least add there :

``` bash
 source ~/install/root/bin/thisroot.sh
 ```


## Python
Miniconda install [here](https://educe-ubc.github.io/conda.html)

One needs to install CUDA for machine learning [https://canonical-ubuntu-wsl.readthedocs-hosted.com/en/latest/tutorials/gpu-cuda/](https://canonical-ubuntu-wsl.readthedocs-hosted.com/en/latest/tutorials/gpu-cuda/)


``` bash
conda update conda
conda activate
conda config --set channel_priority strict
conda create -c conda-forge --name tf root
conda activate tf
pip install --upgrade pip
python3 -m pip install tensorflow==2.12
conda install -c conda-forge cudatoolkit=11.2.2
pip install cudnn==8.9.4
conda update --force conda

conda install -c anaconda pandas
conda install -c conda-forge uproot
pip install --user root_numpy
pip install --upgrade matplotlib
#pip3 install energyflow
```

Or better install from atttached environmental list 
``` bash 
conda create --name tf --file condaEnv.list
```

Verify tensorflow installation :

```bash 
# Verify the installation:
python3 -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```





## Install on Windows

Visual Studio Code https://code.visualstudio.com/download

NoMachine https://www.nomachine.com/


### VS code extensions (inside WSL2):
``` bash
code --install-extension albertopdrf.root-file-viewer 
code --install-extension eamodio.gitlens
code --install-extension esbenp.prettier-vscode
code --install-extension GitHub.copilot
code --install-extension James-Yu.latex-workshop
code --install-extension ms-azuretools.vscode-docker
code --install-extension MS-CEINTL.vscode-language-pack-ru
code --install-extension ms-vscode.cmake-tools
code --install-extension ms-vscode.cpptools
code --install-extension ms-vscode.cpptools-extension-pack
code --install-extension ms-vscode.cpptools-themes
code --install-extension twxs.cmake
```