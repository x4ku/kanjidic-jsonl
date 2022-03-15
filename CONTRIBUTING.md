# Contributing Instructions

Instructions for contributing to this project.

## Setup

Create and activate a virtual environment:
```sh
$ python -m venv env
$ source env/bin/activate
```

Install dependencies:
```sh
$ pip install -r requirements-dev.txt
```

## Development

Lint the source code with `flake8`:
```sh
$ flake8 bin/*
```

Run the unit tests:
```sh
$ bin/test
```

## Updating Data Files

Download:
```sh
$ bin/download
```

Convert:
```sh
$ bin/convert
```

The data files should now be updated.
