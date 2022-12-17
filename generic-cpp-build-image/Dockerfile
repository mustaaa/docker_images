FROM ubuntu:18.04

# grpc release version used:
ENV RELEASE_TAG="v1.49.2"
ENV BASE_PATH=/opt/grpc

##
# Install requirements
#
RUN apt-get update
RUN apt-get install -y sudo build-essential cmake gcc git pkg-config
## Install bash for easier operation in the future
RUN apt-get install -y bash

# Install python3.7 needed for conan 
# RUN apt install -y python3.7
# RUN apt install -y python3-pip
# RUN python3.7 -m pip install -U MarkupSafe
# RUN python3.7 -m pip install conan

##
# Download gRPC and initialise submodules so as to later install these
#
WORKDIR /opt
RUN git clone -b $RELEASE_TAG https://github.com/grpc/grpc --recursive
WORKDIR ${BASE_PATH}
RUN git submodule update --init

# Install third-party libraries and then install gRPC
WORKDIR ${BASE_PATH}/test/distrib/cpp
# Remote location for script: https://raw.githubusercontent.com/grpc/grpc/${RELEASE_TAG}/test/distrib/cpp/run_distrib_test_cmake.sh
RUN ./run_distrib_test_cmake.sh

# Get back to the original directory
WORKDIR ${BASE_PATH}