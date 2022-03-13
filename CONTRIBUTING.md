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

Download KANJIDIC:
```sh
$ bin/download
```

KANJIDIC will be downloaded to the `data/` directory as `kanjidic.xml`, and
KANJIDIC's DTD file will be downloaded to the `schema/` directory as
`kanjidic-dtd.xml`.

Convert KANJIDIC:
```sh
$ bin/convert
```

The data files should now be updated.
