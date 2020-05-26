# Install the official image for OpenFOAM plus 1812
FROM openfoamplus/of_v1812_centos73

# Define working directory in image
WORKDIR /home/ofuser

# Install as root
USER root
#f01030e1dcf3RUN echo "ofuser ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Install centos dependencies
RUN yum update; \
    yum install -y  gcc-gfortran  \
                    svn \
                    git \
                    gsl-devel
# Install as ofuser. Keeping the same naming as the official openfoamplus image
USER ofuser

# Install wave2foam
RUN source /opt/OpenFOAM/setImage_v1812.sh; \
    mkdir -p $FOAM_RUN/../applications/utilities; \
   cd $FOAM_RUN/../applications/utilities; \
   svn co http://svn.code.sf.net/p/openfoam-extend/svn/trunk/Breeder_1.6/other/waves2Foam; \
   cd waves2Foam; \
   ./Allwmake

USER ofuser

# Source the bashrc of Waves2Foam
RUN source /opt/OpenFOAM/setImage_v1812.sh; \
    source $FOAM_RUN/../applications/utilities/waves2Foam/bin/bashrc
