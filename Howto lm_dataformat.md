# How to Use `lm_dataformat` Library

## Introduction

The `lm_dataformat` library is designed for handling various data formats and archive types, making it easier to read and write large datasets. This guide will walk you through how to use the library, what you can do with it, and what you can't.

## Table of Contents

1. [Installation](#installation)
2. [Reading Data](#reading-data)
3. [Writing Data](#writing-data)
4. [Limitations](#limitations)

---

## Installation

Before using the library, you need to install it. As of now, the library is not available on PyPI, so you would have to clone the repository and install it manually.

```bash
pip install lm-dataformat
```

---

## Reading Data

### Using the `Reader` Class

The `Reader` class is designed to read various file formats. Here's a simple example:

```python
from lm_dataformat import Reader

# Initialize the Reader class
reader = Reader("path/to/directory_or_file")

# Stream data from the file(s)
for data in reader.stream_data():
    print(data)
```

#### Parameters for `stream_data`

- `get_meta`: If set to `True`, it will also yield metadata along with the data.
- `threaded`: If set to `True`, it will read the data in a threaded manner for better performance.

```python
for data in reader.stream_data(get_meta=True, threaded=True):
    print(data)
```

---

## Writing Data

### Using the `Archive` Class

The `Archive` class is designed to write data to an archive. Here's a simple example:

```python
from lm_dataformat import Archive

# Initialize the Archive class
archive = Archive("path/to/output_directory")

# Add data to the archive
archive.add_data("Hello, world!", meta={"author": "John Doe"})

# Commit the data to disk
archive.commit()
```

#### Parameters for `add_data`

- `data`: The data you want to add.
- `meta`: Any metadata you want to include.

#### Parameters for `commit`

- `archive_name`: The name of the archive. Default is 'default'.

---

## Limitations

1. The library does not support all archive and compression formats. It mainly supports JSON, JSONL, DAT, and their compressed versions.
2. The library is not designed for handling extremely large files that exceed the system's memory.
