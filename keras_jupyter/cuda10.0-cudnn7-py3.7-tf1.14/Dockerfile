# chenaok/keras_jupyter

FROM nvidia/cuda:10.0-cudnn7-runtime-ubuntu18.04

USER root

RUN apt update && apt install -y wget vim git zsh make ffmpeg bzip2 build-essential curl 

RUN wget --quiet https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh -O ./anaconda.sh
RUN /bin/bash ./anaconda.sh -b -p /opt/conda
ENV PATH /opt/conda/bin:$PATH
RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc 
RUN echo "conda activate base" >> ~/.bashrc

RUN conda install python=3.7
RUN pip3 install tensorflow==1.15.0

RUN conda update -y conda
RUN conda install cudatoolkit==10.0.130
RUN conda install keras==2.2.4

#####################################################

RUN useradd -U docker
RUN groupmod -g 999 docker

ENV HOME /home/docker
ENV NOTEBOOK_HOME /notebooks

RUN mkdir $HOME
RUN chown docker:docker $HOME 
RUN mkdir $NOTEBOOK_HOME
RUN chown docker:docker $NOTEBOOK_HOME 

#####################################################

USER docker
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

WORKDIR $HOME 
RUN jupyter notebook --generate-config
RUN echo "c.NotebookApp.ip = '*'" >> $HOME/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.port = 8888" >> $HOME/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.open_browser = False" >> $HOME/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.notebook_dir = '$NOTEBOOK_HOME'" >> $HOME/.jupyter/jupyter_notebook_config.py


WORKDIR $HOME
RUN git clone https://github.com/chenaoki/dotfiles.git
WORKDIR $HOME/dotfiles
RUN python install.py

WORKDIR $NOTEBOOK_HOME
CMD ["sh", "-c", "jupyter notebook > $NOTEBOOK_HOME/log.txt 2>&1"]

