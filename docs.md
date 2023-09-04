# lm_dataformat Documentation

## Overview

The `lm_dataformat` library is designed to handle various data formats and archive types. It provides functionalities for reading and writing data in different formats like JSON, JSONL, DAT, and others. The library also supports various compression methods like Zstandard, Gzip, and Tar.

---

## Table of Contents

- [Imports](#imports)
- [Constants](#constants)
- [Utility Functions](#utility-functions)
- [Classes](#classes)
  - [Reader](#reader)
  - [Archive](#archive)
  - [DatArchive](#datarchive)
  - [JSONArchive](#jsonarchive)

---

## Imports

The library imports various Python modules to handle file operations, compression, and JSON parsing.

```python
import os
import zstandard
import ujson as json
import tarfile
...
```

---

## Constants

### `VALID_EXTENSIONS`

A list of valid file extensions that the library can handle.

```python
VALID_EXTENSIONS = ['openwebtext.tar.xz', '_data.xz', '.dat.zst', '.jsonl', '.jsonl.zst', '.jsonl.zst.tar', '.json.zst', '.txt', '.zip', '.tar.gz', '.json.gz', '.gz']
```

---

## Utility Functions

### `has_valid_extension(file)`

Check if a file has a valid extension.

**Parameters:**

- `file`: The file name to check.

**Returns:**

- `True` if the file has a valid extension, `False` otherwise.

### `_listdir_or_file(x)`

Lists file in a directory or return the file itself.

**Parameters:**

- `x`: The directory or file path.

**Returns:**

- A list of file paths.

### `listdir_or_file(x)`

Filters files based on valid extensions.

**Parameters:**

- `x`: The directory or file path.

**Returns:**

- A list of file paths with valid extensions.

### `tarfile_reader(file, streaming=False)`

Custom tarfile parser.

**Parameters:**

- `file`: The tar file to read.
- `streaming`: Whether to stream the file or not.

**Returns:**

- Yields file content.

### `handle_jsonl(jsonl_reader, get_meta, autojoin_paragraphs, para_joiner, key='text')`

Handles JSONL files.

**Parameters:**

- `jsonl_reader`: The JSONL reader object.
- `get_meta`: Whether to get meta information.
- `autojoin_paragraphs`: Whether to join paragraphs automatically.
- `para_joiner`: The character to join paragraphs.
- `key`: The key to extract text.

**Returns:**

- Yields text and optionally meta information.

---

## Classes

### Reader

Responsible for reading various file formats.

#### Methods

- `__init__(self, in_path)`: Constructor
- `stream_data(self, get_meta=False, threaded=False)`: Streams data from files.
- Various `read_*` methods for different file formats.

### Archive

Handles writing data to an archive.

#### Methods

- `__init__(self, out_dir, compression_level=3, threads=8)`: Constructor
- `add_data(self, data, meta={})`: Adds data to the archive.
- `commit(self, archive_name='default')`: Commits the current chunk to disk.

### DatArchive

Similar to Archive but for `.dat` files.

#### Methods

- `__init__(self, out_dir)`: Constructor
- `add_data(self, data)`: Adds data to the archive.
- `commit(self, archive_name=None)`: Commits the current chunk to disk.

### JSONArchive

Similar to Archive but for `.json` files.

#### Methods

- `__init__(self, out_dir)`: Constructor
- `add_data(self, data)`: Adds data to the archive.
- `commit(self)`: Commits the current chunk to disk.

---

This documentation provides a comprehensive overview of the `lm_dataformat` library, detailing its various components and functionalities.
