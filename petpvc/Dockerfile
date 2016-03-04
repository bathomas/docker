# Create a base docker container that will execute recon-all and zip the output
#
# Example usage:
#   docker run --rm -ti \
#       -v </input/directory>:/input \
#       -v </output/directory>:/output \
#       vistalab/recon-all -i /input/<input_file_name> -subjid <subject_id> -all
#

# Start with Ubuntu phusion/baseimage
FROM phusion/baseimage:0.9.18

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

RUN apt-get update
RUN apt-get -y install cmake wget g++

RUN mkdir -p /opt/ITK
WORKDIR /opt/ITK
RUN wget http://downloads.sourceforge.net/project/itk/itk/4.9/InsightToolkit-4.9.0.tar.gz && tar xvzf InsightToolkit-4.9.0.tar.gz

RUN mkdir -p /opt/ITK/BUILD && \
cd /opt/ITK/BUILD && \
cmake ../InsightToolkit-4.9.0 \
&& make -j && make install

RUN apt-get -y install git
RUN mkdir -p /opt/PETPVC && cd /opt/PETPVC && \
git clone https://github.com/UCL/PETPVC.git code && \
mkdir BUILD && cd BUILD && \
cmake ../code && \
make -j && make test && make install



# Start with base freesurfer container
#FROM vistalab/freesurfer

# Copy the run script
#COPY run /opt/run

# Make sure we can execute the script and install zip
#RUN chmod +x /opt/run \
#    && apt-get update && apt-get -y install zip

# Set entrypoint to run the script
#ENTRYPOINT ["/opt/run"]
