# Installing Jupyter in Docker Container
Creating docker container with the following command
 ```
 docker run -p 8888:8888 -v $(pwd):/home/jovyan/work jupyter/minimal-notebook
 ```

we can also use other jupyter docker image provided by Jupyter Project in the docker hub. 

# Installing Jupyter with Custom Docker file
1. Create docker file
    ```
    ARG BASE_CONTAINER=jupyter/minimal-notebook
    FROM $BASE_CONTAINER

    # LABEL author="Author name"

    USER root

    # Run install component through pip
    RUN pip install pandas numpy matplotlib plotly

    # Switch back to jovyan to avoid accidental container runs as root
    USER $NB_UID
    ```
2. Build custom docker image
    ```
    docker build -t neutrofoton/jupyter-notebook .
    ```

3. Create a docker container
    ```
    docker run -p 8888:8888 -v /Users/neutro/workspace/source/github/dsc_ml_ai/notebook:/home/jovyan/work neutrofoton/jupyter-notebook
    ```

# Interacting with Jupyter Container Terminal
1. Entering the terminal container with bash
    ```
    docker exec -it e3c /bin/bash
    ```

2. Executing linux command
    ```
    $ ls
    $ cd work
    ```
3. Python and Jupyter info
    ```
    $ python --version
    $ ipython --version
    $ conda info -a
    $ pip list
    ```
4. Installing component
    ```
    pip install pandas numpy
    ```