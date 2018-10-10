# SRF使用准备

## spack安装

### 配置spack环境

python 3（最好使用anaconda包中的python环境）

```shell
wget https://repo.anaconda.com/archive/Anaconda3-5.2.0-Linux-x86_64.sh
cd /path/to/download/anaconda
bash ~/Downloads/Anaconda3-5.2.0-Linux-x86_64.sh
```



C/C++环境（version 4 或 5）

```shell
sudo apt-get install gcc
```


fortrain编译器
```shell
sudo apt-get install gfortran
```



从github的tech-pi仓库（https://github.com/tech-pi）中，将spack包fork到自己的仓库，再由自己的仓库clone到本地。



添加spack路径到环境变量中

```shell
export SPACK_ROOT=/path/to/spack
export PATH=$SPACK_ROOT/bin:$PATH
```

测试
```shell
spack install libelf
```
    

添加spack基础环境配置
```
spack bootstrap
```



添加spack 命令行支持
```
. $SPACK_ROOT/share/spack/setup-env.sh
```


检查安装
```shell
spack spec netcdf
```


列出编译器
```
spack compilers 
```

加入我们自己添加的软件包
```shell
cd /path/to/spack/var/spack/repos
spack repo add ./techpi    
```

可通过spack repo list进行查看，若已经添加成功，则出现techpi仓库名

注：详细安装操作流程请参加[spack官网文档](https://spack.readthedocs.io/en/latest/getting_started.html)



### STIR/BBS/LMREC/CASTOR安装

```shell
spack install <安装包名称>
```
STIR包名称：`stir@master`

BBS包名称： `bbslmirp`

LMREC包名称： `lmrec`

CASTOR包名称 `castor` 依赖`root5.34.36`



安装完成后可以通过`spack find <安装包名称>` 来查找是否已经成功安装



### tensorflow安装配置(需支持GPU)：TODO

NVIDIA显卡驱动安装

在[NVIDIA官网](https://www.nvidia.cn/Download/index.aspx?lang=cn)查找计算机对应显卡驱动版本，并下载安装，安装教程与对应驱动版本对应，请参看下载页面

    

GPU安装



cuDNN安装





### SRF安装

    从github的tech-pi仓库（https://github.com/tech-pi）中，将SRF库拉取到本地

        git clone https://github.com/tech-pi/SRF.git

    

    添加anaconda的配置(optional)

        pip install msgpack



    从github上更新各依赖包到最新，包括dxshape,doufo,dxcore,dxlearn,jfs

        git clone https://github.com/tech-pi/dxlearn.git, pip install .

        git clone https://github.com/tech-pi/dxcore.git, pip install .

        git clone https://github.com/tech-pi/filesystem.git, pip install .

        git clone https://github.com/tech-pi/dxshape.git, pip install .

        git clone https://github.com/tech-pi/doufo.git, pip install .



    进入SRF文件夹并安装

        cd path/to/SRF

        pip install -e .



## SRF使用

相关配置文件及数据文件放在/mnt/gluster/Techpi/brain16/recon文件夹下。

### SRF调用自身重建方法



attention:使用每个模块，需要在新终端中spack load 模块名才能使用。如需使用stir,则输入 spack load stir

### SRF调用STIR重建方法

    进入SRF文件夹下的examples/external/stir目录，执行run_stir.sh脚本即可。



### SRF调用BBS重建方法

    进入SRF文件夹下的examples/external/bbs目录，执行run_bbs.sh脚本即可。



### SRF调用LMREC重建方法

    进入SRF文件夹下的examples/external/lmrec目录，执行run_lmrec.sh脚本即可。



### SRF调用CASTOR重建方法: TODO ask for gaoyu

    在home目录下新建castor的文件夹并添加部分文件

        git clone https://github.com/chengaoyu/CASTOR.git

        cd /path/to/CASROR

        cp -a config/ /path/to/home/castor



    使用时由root直接转为castor数据和几何，需要准备root2castor_config.json及对应root。

    重建时需要生成的数据文件和recon_config.json文件



    进入SRF文件夹下的examples/external/stir目录，执行run_stir.sh脚本即可。


