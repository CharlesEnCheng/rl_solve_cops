FROM nvidia/cuda:8.0-cudnn7-devel-ubuntu16.04
LABEL author=github/tahsinkose

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install gcc g++ gfortran wget cpio && \
  cd /tmp && \
  wget http://registrationcenter-download.intel.com/akdlm/irc_nas/tec/15275/l_mkl_2019.3.199.tgz && \
  tar -xzf l_mkl_2019.3.199.tgz && \
  cd l_mkl_2019.3.199 && \
  sed -i 's/ACCEPT_EULA=decline/ACCEPT_EULA=accept/g' silent.cfg && \
  sed -i 's/ARCH_SELECTED=ALL/ARCH_SELECTED=INTEL64/g' silent.cfg && \
  sed -i 's/COMPONENTS=DEFAULTS/COMPONENTS=;intel-comp-l-all-vars__noarch;intel-comp-nomcu-vars__noarch;intel-openmp__x86_64;intel-tbb-libs__x86_64;intel-mkl-common__noarch;intel-mkl-installer-license__noarch;intel-mkl-core__x86_64;intel-mkl-core-rt__x86_64;intel-mkl-doc__noarch;intel-mkl-doc-ps__noarch;intel-mkl-gnu__x86_64;intel-mkl-gnu-rt__x86_64;intel-mkl-common-ps__noarch;intel-mkl-core-ps__x86_64;intel-mkl-common-c__noarch;intel-mkl-core-c__x86_64;intel-mkl-common-c-ps__noarch;intel-mkl-tbb__x86_64;intel-mkl-tbb-rt__x86_64;intel-mkl-gnu-c__x86_64;intel-mkl-common-f__noarch;intel-mkl-core-f__x86_64;intel-mkl-gnu-f-rt__x86_64;intel-mkl-gnu-f__x86_64;intel-mkl-f95-common__noarch;intel-mkl-f__x86_64;intel-mkl-psxe__noarch;intel-psxe-common__noarch;intel-psxe-common-doc__noarch;intel-compxe-pset/g' silent.cfg && \
  ./install.sh -s silent.cfg && \
  cd .. && rm -rf * && \
  rm -rf /opt/intel/.*.log /opt/intel/compilers_and_libraries_2019.3.199/licensing && \
  echo "/opt/intel/mkl/lib/intel64" >> /etc/ld.so.conf.d/intel.conf && \
  ldconfig && \
  echo "source /opt/intel/mkl/bin/mklvars.sh intel64" >> /etc/bash.bashrc

RUN apt-get -y install libtbb-dev
RUN apt-get install -y mesa-utils -y module-init-tools

RUN wget https://repo.anaconda.com/archive/Anaconda2-5.3.1-Linux-x86_64.sh
RUN bash Anaconda2-5.3.1-Linux-x86_64.sh -b -p

RUN apt-get install -y nano
ENV PATH=/root/anaconda2/bin:$PATH

RUN apt-get -y install git
RUN git clone https://github.com/CharlesEnCheng/rl_solve_cops.git
