# chenaok/keras_jupyter

FROM continuumio/anaconda3

MAINTAINER chenaoki <chenaoki@gmail.com>

RUN apt-get update --fix-missing

USER root
ENV HOME /root
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

ENV NOTEBOOK_HOME /notebooks
RUN mkdir -p $NOTEBOOK_HOME 

##########################

RUN conda update -y conda
RUN conda install cudatoolkit
RUN conda install cudnn
RUN conda install tensorflow-gpu
RUN conda install keras
RUN conda install -c numba numba

##########################


WORKDIR $HOME 
RUN jupyter notebook --generate-config
RUN echo "c.NotebookApp.ip = '*'" >> $HOME/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.port = 8888" >> $HOME/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.open_browser = False" >> $HOME/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.notebook_dir = '$NOTEBOOK_HOME'" >> $HOME/.jupyter/jupyter_notebook_config.py


##########################


WORKDIR $HOME
RUN apt-get install -y zsh
RUN git clone https://github.com/chenaoki/dotfiles.git
WORKDIR $HOME/dotfiles
RUN python install.py
WORKDIR $HOME

##########################


