# EMENDA Dockerfile for klocwork 2017 server 12.3
# Need to insert your KW license file into the project root
# To obtain a license please contact support@emenda.com

# Use Latest Ubuntu Official image
FROM ubuntu:latest

# Defined variables
# Update your Database port, Server port and license port to your own environment
# Update installer path, server directory and project root directory to your own environment 
ARG DATABASE_PORT=3123
ARG KW_PORT=8123
ARG LICENSE_PORT=27000
ARG INSTALLER_PATH=/opt/Klocwork
ARG INSTALL_DIRECTORY=/opt/Klocwork/Server
ARG PROJECTS_ROOT=/opt/Klocwork/Projects_root_12_3
ARG INSTALLER_FILE=[PATH_OF_YOUR_KW_12_3_LINUX_INSTALLER]
ARG LICENSE_FILE=[PATH_OF_YOUR_KW_LICENSE]

# Install pre-requisites packages for KW, GCC (minimum)
RUN apt-get -y update 
RUN apt-get -y install hostname 
RUN apt-get -y install wget
RUN apt-get -y install libaio1
RUN apt-get -y install libc6-i386

# Install built tools (possible to install your own build tool)
RUN apt-get install -y gcc

# Open KW ports
EXPOSE $KW_PORT $DATABASE_PORT $LICENSE_PORT

# Create KW users (default Username)
ARG USERNAME=Username
RUN useradd -m -d /home/$USERNAME -s /bin/sh $USERNAME
RUN echo "$USERNAME:$USERNAME" | chpasswd

# Making KW Directories and attributes permissions
RUN mkdir $INSTALLER_PATH
RUN mkdir $INSTALL_DIRECTORY
RUN mkdir $PROJECTS_ROOT
RUN chown $USERNAME:$USERNAME $INSTALLER_PATH
RUN chown $USERNAME:$USERNAME $INSTALL_DIRECTORY
RUN chown $USERNAME:$USERNAME $PROJECTS_ROOT

# KW Installation
#Logging as non root user - important pre-requisite from KW installation
USER $USERNAME
#Downloading installer file
RUN wget $INSTALLER_FILE -O $INSTALLER_PATH/$INSTALLER_FILE
#Extracting KW Installer
RUN tar -zxvf $INSTALLER_PATH/$INSTALLER_FILE -C $INSTALLER_PATH
RUN chmod 750 $INSTALLER_PATH/$INSTALLER_FILE
RUN chown $USERNAME:$USERNAME $INSTALL_DIRECTORY
#Running KW Installation and Projects_root configuration
RUN $INSTALLER_PATH/$INSTALLER_FILE -a --database-port $DATABASE_PORT --klocwork-port $KW_PORT  --license-port $LICENSE_PORT  --projects-root $PROJECTS_ROOT $INSTALL_DIRECTORY

#Copy License File on project root (install your license path here)
RUN cp $LICENSE_FILE $PROJECTS_ROOT/licenses




