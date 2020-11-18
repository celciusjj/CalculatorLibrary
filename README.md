# CalculatorLibrary

# Manual de instalacion del pipeline
* Crear una carpeta .circleci y un archivo config.yml
* El archivo contiene diferentes parametros, se enunciaran los mas importantes:
- Version: Los config.yml comienzan con el numero de version del circleCI
- Docker: Contiene un entorno de ejecución de python 3.7 (Image), circleCI usa docker como su ejecutor
- Step: Marca el comienzo de la lista de pasos de compilación
- Run: La ejecución de programas o comandos de línea de comandos que se realizaran, encontramos la clave (Command) la cual ejecuta los comandos deseados, en nuestro caso, instalación de dependencias y ejecucion de los test.

Ejemplo:
```
version: 2
jobs:
  build:
    docker:
      - image: circleci/python:3.7

    working_directory: ~/repo

    steps:
      # Step 1: obtain repo from GitHub
      - checkout
      # Step 2: create virtual env and install dependencies
      - run:
          name: install dependencies
          command: |
            python3 -m venv venv
            . venv/bin/activate
            pip install -r requirements.txt
      # Step 3: run linter and tests
      - run:
          name: run tests
          command: |
            . venv/bin/activate
            flake8 --exclude=venv* --statistics
            pytest -v --cov=calculator
```


* Para probar los test manualmente: pytest -v --cov
* Para testear el lintern manualmente: flake8 --statistics
 
* Realizamos commit a nuestro repositorio
* Ingresamos a CircleCI y nos conectamos con github
* Hacemos click en hacer set up del proyecto
* Omitimos la config por defecto debido a que ya se ha creado una.
* Comienza la build, y nos indica el estado de compilcación
