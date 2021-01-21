# rl_solve_cops
This is copied from Hanjun-Dai/graph_comb_opt (https://github.com/Hanjun-Dai/graph_comb_opt).
Plsease refer to the original author for further understanding. 
Here is a simply revised version regarding to config setting so that this code can be run on CPU successfully.

Commands may be used are,
- yet this information can be captured from the revised dockfile in graphnn.

wget https://repo.anaconda.com/archive/Anaconda2-5.3.1-Linux-x86_64.sh<br/>
bash Anaconda2-5.3.1-Linux-x86_64.sh<br/>
sudo apt install git<br/>
git clone --recursive https://github.com/Hanjun-Dai/graph_comb_opt.<br/>
git clone https://github.com/Hanjun-Dai/graphnn.<br/>

# for installing cuda but wont be used for this version 
wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb<br/>
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub<br/>
sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb<br/>
sudo apt-get update<br/>
sudo apt-get install cuda<br/>

gedit ~/.bashrc<br/>
export CUDA_HOME=/usr/local/cuda<br/>
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH<br/>
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH<br/>

# for installing mkl (way - 1) (dont use this one. this will cause the lib.so building fail.)
wget http://registrationcenter-download.intel.com/akdlm/irc_nas/tec/12147/l_mkl_2017.4.239.tgz<br/>
tar xzvf l_mkl_2017.4.239.tgz<br/>
cd l_mkl_2017.4.239<br/>
sudo ./install_GUI.sh<br/>

# for installing mkl (way - 2) (this one is tested pass)
wget https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB<br/>
sudo apt-key add GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB<br/>
sudo sh -c 'echo deb https://apt.repos.intel.com/mkl all main > /etc/apt/sources.list.d/intel-mkl.list'<br/>
sudo apt-get update<br/>
sudo apt-get install intel-mkl-64bit-2020.4-912<br/>

# add mkl into env<br/>
gedit ~/.bashrc<br/>
source /opt/intel/parallel_studio_xe_2020.4.912/bin/psxevars.sh<br/>


# if run cpu version
1. make_common in graphnn: remove USE_GPU<br/>
2. makefile in code: switch build to build_cpuonly & remain CXXFLAGS += $(addprefix -I,$(include_dirs)); CXXFLAGS += -fPIC<br/>

# tbb 
apt-get -y install libtbb-dev<br/>

# suggest to build up the env through docker directly - tested on mac
1. cd to Dockerfile directory<br/>
2. docker build -t env:01 .<br/>
3. docker run -it env:01<br/>
4. docker container prune<br/>
5. docker rmi env:01<br/>
6. docker images<br/>
