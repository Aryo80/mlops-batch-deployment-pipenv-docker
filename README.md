# mlops-batch-deployment-pipenv-docker

This repository contains my learning progress and projects for the MLOps Zoomcamp. The MLOps Zoomcamp is a comprehensive course designed to teach the fundamentals and advanced concepts of Machine Learning Operations (MLOps). This repository serves as a documentation of my journey, including the homeworks, experiments, and models I have developed along the way.



## Pipenv Configuration

Use the following Pipfile configuration to set up the virtual environment with required dependencies:

```toml
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]
scikit-learn = "==1.5.0"
pandas = "*"
pyarrow = "*"
s3fs = "*"

[dev-packages]

[requires]
python_version = "3.10"
```
### Commands Description
```bash
pip install pipenv
```
Install Pipenv, a tool that provides a virtual environment and dependency management for Python projects.
```bash
 pipenv install
```
Installs dependencies specified in the Pipfile.lock file (if present) or Pipfile, creating a virtual environment for the project.
```bash
## pipenv shell
```
Activates the virtual environment created by Pipenv, allowing you to work within an isolated environment with project dependencies.



Returns the path of the Python interpreter executable currently being used. Useful for checking which Python interpreter is running.


### Dockerfile
The Dockerfile defines the environment for running the script inside a Docker container:

``` python
FROM agrigorev/zoomcamp-model:mlops-2024-3.10.13-slim

RUN pip install -U pip
RUN pip install pipenv 

WORKDIR /app

COPY [ "Pipfile", "Pipfile.lock", "./" ]

RUN pipenv install --system --deploy

COPY [ "batch.py", "batch.py" ]

RUN mkdir -p output/

ENTRYPOINT [ "python", "batch.py" ]
```
'''bash
docker build -t my-batch-script .

docker run my-batch-script yellow 2023 5
```
