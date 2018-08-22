# mbuckler/tf-faster-rcnn-deps
#
# Dockerfile to hold dependencies for the Tensorflow implmentation
# of Faster RCNN

Bootstrap: docker

From: nvidia/cuda:8.0-cudnn6-devel
WORKDIR /root

# Get required packages
RUN apt-get update && \
  apt-get install vim \
                  python-pip \
                  python-dev \
                  python-opencv \
                  python-tk \
                  libjpeg-dev \
                  libfreetype6 \
                  libfreetype6-dev \
                  zlib1g-dev \
                  cmake \
                  wget \
                  cython \
                  git \

                  tmux \
                  -y
                  
# Get required python modules
RUN pip install --upgrade pip
RUN pip install image \
                scipy \
                matplotlib \
                PyYAML \
                numpy \
                pillow \
                pandas \
                easydict \
                tensorflow-gpu==1.4.1
# Update numpy
RUN pip install -U numpy

# Install python interface for COCO
RUN git clone https://github.com/pdollar/coco.git
WORKDIR /root/coco/PythonAPI
RUN make

# Add CUDA to the path
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/cuda/lib64
ENV CUDA_HOME /usr/local/cuda
ENV PYTHONPATH /root/coco/PythonAPI
RUN ldconfig
