# Create a docker container that will execute run PETPVC
#
# Example usage:
#  docker run -v </path/to/input/data>:/input \
#    -v </path/to/output/data>:/output bathomas/petpvc \
#    pvc_rbv /input/<pet.nii.gz> /input/<mask.nii.gz> /output/<pvcOutput.nii.gz> \
#    -x 6 -y 6 -z 6

# Start with Ubuntu phusion/baseimage
FROM phusion/baseimage:0.9.18

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

RUN apt-get update
RUN apt-get -y install cmake wget g++ git

RUN mkdir -p /opt/ITK
WORKDIR /opt/ITK
RUN wget http://downloads.sourceforge.net/project/itk/itk/4.9/InsightToolkit-4.9.0.tar.gz && tar xvzf InsightToolkit-4.9.0.tar.gz

RUN mkdir -p /opt/ITK/BUILD && \
cd /opt/ITK/BUILD && \
cmake ../InsightToolkit-4.9.0 \
&& make -j && make install

RUN mkdir -p /opt/PETPVC && cd /opt/PETPVC && \
git clone https://github.com/UCL/PETPVC.git code && \
mkdir BUILD && cd BUILD && \
cmake ../code && \
make -j && make test && make install

#Set number of cores to use (currently 4)
ENV ITK_GLOBAL_DEFAULT_NUMBER_OF_THREADS=4
