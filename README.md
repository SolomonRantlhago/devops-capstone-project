# devops-capstone-project

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.9](https://img.shields.io/badge/Python-3.9-green.svg)](https://shields.io/)

## Description

This project implements a RESTful microservice for managing customer **Accounts** as part of the IBM DevOps and Software Engineering Capstone project. The service is built with Python and Flask, follows the Model-View-Controller (MVC) pattern, and supports full CRUD operations — Create, Read, Update, Delete, and List — on account records backed by a PostgreSQL database.

The codebase is developed using Test-Driven Development (TDD) practices, maintaining at least 95% test coverage, and is designed to be built, tested, and deployed through a CI/CD pipeline using Tekton on OpenShift/Kubernetes.

## Development Environment

These labs are designed to be executed in the IBM Developer Skills Network Cloud IDE with OpenShift. Please use the links provided in the Coursera Capstone project to access the lab environment.

Once you are in the lab environment, you can initialize it with `bin/setup.sh` by sourcing it. (*Note: DO NOT run this program as a bash script. It sets environment variables and so must be sourced*):

```bash
source bin/setup.sh
```

This will install Python 3.9, make it the default, modify the bash prompt, create a Python virtual environment and activate it.

After sourcing it your prompt should look like this:

```bash
(venv) theia:project$
```

## Useful commands

Under normal circumstances you should not have to run these commands. They are performed automatically at setup but may be useful when things go wrong:

### Activate the Python 3.9 virtual environment

```bash
source ~/venv/bin/activate
```

### Installing Python dependencies

First make sure the Python 3.9 virtual environment is activated and then use:

```bash
make install
```

### Starting the Postgres Docker container

```bash
make db
```

You can use the `docker ps` command to make sure that postgres is up and running.

## Project layout

The code for the microservice is contained in the `service` package. All of the tests are in the `tests` folder. The code follows the **Model-View-Controller** pattern with all of the database code and business logic in the model (`models.py`), and all of the RESTful routing on the controller (`routes.py`).

```text
├── service         <- microservice package
│   ├── common/     <- common log and error handlers
│   ├── config.py   <- Flask configuration object
│   ├── models.py   <- code for the persistent model
│   └── routes.py   <- code for the REST API routes
├── setup.cfg       <- tools setup config
└── tests                       <- folder for all of the tests
    ├── factories.py            <- test factories
    ├── test_cli_commands.py    <- CLI tests
    ├── test_models.py          <- model unit tests
    └── test_routes.py          <- route unit tests
```

## Data Model

The Account model contains the following fields:

| Name | Type | Optional |
|------|------|----------|
| id | Integer| False |
| name | String(64) | False |
| email | String(64) | False |
| address | String(256) | False |
| phone_number | String(32) | True |
| date_joined | Date | False |

## API Endpoints

The service exposes the following REST endpoints for managing accounts:

| Operation | Method | URL |
|-----------|--------|-----|
| Create | `POST` | `/accounts` |
| Read | `GET` | `/accounts/{id}` |
| Update | `PUT` | `/accounts/{id}` |
| Delete | `DELETE` | `/accounts/{id}` |
| List | `GET` | `/accounts` |

## Local Kubernetes Development

This repo can also be used for local Kubernetes development. It is not advised that you run these commands in the Cloud IDE environment. The purpose of these commands is to simulate the Cloud IDE environment locally on your computer.

At a minimum, you will need [Docker Desktop](https://www.docker.com/products/docker-desktop) installed on your computer. For the full development environment, you will also need [Visual Studio Code](https://code.visualstudio.com) with the [Remote Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension from the Visual Studio Marketplace.

Please only use these commands for working stand-alone on your own computer with the VSCode Remote Container environment provided.

1. Bring up a local K3D Kubernetes cluster

```bash
    $ make cluster
```

2. Install Tekton

```bash
    $ make tekton
```

3. Install the ClusterTasks that the Cloud IDE has

```bash
    $ make clustertasks
```

You can now perform Tekton development locally, just like in the Cloud IDE lab environment.

## Author

This project was completed as part of the IBM DevOps and Software Engineering Professional Certificate on Coursera.

## License

Licensed under the Apache License. See [LICENSE](LICENSE)

## © IBM Corporation 2022. All rights reserved.
