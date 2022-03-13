# kanjidic-jsonl

[KANJIDIC] redistributed in the [jsonlines] format.

[![pipeline status](https://gitlab.com/x4ku/kanjidic-jsonl/badges/main/pipeline.svg)](https://gitlab.com/x4ku/kanjidic-jsonl/-/commits/main)

## Overview

This project redistributes [KANJIDIC] in the [jsonlines] format.

You can download the latest files here:

| File                 | Description            |
| -------------------- | ---------------------- |
| [`kanjidic.jsonl`]   | KANJIDIC records       |
| [`kanjidic.json`]    | KANJIDIC record schema |
| [`kanjidic-dtd.xml`] | Additional information |

These files are updated automatically every month.

## Usage

You can read and work with the data files from this project as-is, line-by-line.
Each line is a JSON array containing a record's *values*. There is no need to
even load the entire file into memory if your use-case does not require it -
simply read and work with one line at a time.

By storing only values instead of highly redundant dictionaries (i.e. *keys* and
*values*), we are able to achieve a massive reduction in file size while still
retaining the ability to express the complex structure of these records in JSON.
If you would prefer to convert these records into dictionaries/objects, a
reference implementation is provided below.

### Converting Records to Dictionaries

The reference implementation below uses the [`kanjidic.json`] schema file to
convert records from the [`kanjidic.jsonl`] file into dictionaries/objects.

```py
import json
from pathlib import Path

def map_schema(value, schema):
    if type(schema) is list:
        return [map_schema(v, schema[0]) for v in value]
    if type(schema) is dict:
        kvs = zip(schema.keys(), value, schema.values())
        return {k: map_schema(v, s) for k, v, s in kvs}
    return value

with open(Path('schema') / 'kanjidic.json') as file:
    schema = json.load(file)

with open(Path('data') / 'kanjidic.jsonl') as file:
    records = [map_schema(json.loads(line), schema) for line in file]
```

The `records` variable should now contain the records as dictionaries.

## License

See the [`LICENSE`] file before using any of the files provided by this project
in your own work.


<!-- links -->

[`LICENSE`]: LICENSE
[`kanjidic.json`]: schema/kanjidic.json
[`kanjidic.jsonl`]: data/kanjidic.jsonl
[`kanjidic-dtd.xml`]: schema/kanjidic-dtd.xml

[KANJIDIC]: http://www.edrdg.org/wiki/index.php/KANJIDIC_Project
[jsonlines]: https://jsonlines.org/
