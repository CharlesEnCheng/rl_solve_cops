# rl_solve_cops
This is copied from Hanjun-Dai/graph_comb_opt (https://github.com/Hanjun-Dai/graph_comb_opt).

Plsease refer to the original author for further understanding. 

Here is a simply revised version regarding to config setting so that this code can be run on CPU successfully.



Commands may be used are,
- yet this information can be captured from the revised dockfile in graphnn.

wget https://repo.anaconda.com/archive/Anaconda2-5.3.1-Linux-x86_64.sh
bash Anaconda2-5.3.1-Linux-x86_64.sh

sudo apt install git
git clone --recursive https://github.com/Hanjun-Dai/graph_comb_opt
git clone https://github.com/Hanjun-Dai/graphnn

# for installing cuda and wont be used for this version
wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb
sudo apt-get update
sudo apt-get install cuda

gedit ~/.bashrc
export CUDA_HOME=/usr/local/cuda
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

# for installing mkl (way - 1)
wget http://registrationcenter-download.intel.com/akdlm/irc_nas/tec/12147/l_mkl_2017.4.239.tgz
tar xzvf l_mkl_2017.4.239.tgz
cd l_mkl_2017.4.239
sudo ./install_GUI.sh

# for installing mkl (way - 2)
wget https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB
sudo apt-key add GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB
sudo sh -c 'echo deb https://apt.repos.intel.com/mkl all main > /etc/apt/sources.list.d/intel-mkl.list'
sudo apt-get update
sudo apt-get install intel-mkl-64bit-2020.4-912

# add mkl into env
gedit ~/.bashrc
source /opt/intel/parallel_studio_xe_2020.4.912/bin/psxevars.sh


# if run cpu version
1. make_common in graphnn: remove USE_GPU
2. makefile in code: switch build to build_cpuonly & remain CXXFLAGS += $(addprefix -I,$(include_dirs)); CXXFLAGS += -fPIC

# tbb 
apt-get -y install libtbb-dev

# suggest to build up the env through docker directly - tested on mac
1. cd to Dockerfile directory
2. docker build -t env:01 .
3. docker run -it env:01
4. docker container prune
5. docker rmi env:01
6. docker images
