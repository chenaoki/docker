# chenaoki/pytorch_jupyter

FROM pytorch/pytorch:1.2-cuda10.0-cudnn7-runtime

RUN apt-get update && apt-get install -y zsh

RUN conda install -y jupyter
RUN conda install -c conda-forge matplotlib


RUN useradd -U docker
RUN groupmod -g 999 docker

ENV HOME /home/docker
ENV NOTEBOOK_HOME /notebooks

RUN mkdir $HOME
RUN chown docker:docker $HOME 
RUN mkdir $NOTEBOOK_HOME
RUN chown docker:docker $NOTEBOOK_HOME 


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


