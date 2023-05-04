# Thrive AI: Llama Index

## Description

LlamaIndex (GPT Index) is a project that provides a central interface to connect your LLM’s with external data.

- Github: https://github.com/jerryjliu/llama_index

- PyPi:

- - LlamaIndex: https://pypi.org/project/llama-index/.

- - GPT Index (duplicate): https://pypi.org/project/gpt-index/.

- Twitter: https://twitter.com/gpt_index

- Discord https://discord.gg/dGcwcsnxhU

## Features

Llama Index comes with the following features:

- Connects any LLM with external data
- Written in Python
- Supports a variety of input formats
- Can connect with a plethora of database connectors

## Ecosystem

- LlamaHub: https://llamahub.ai/
- LlamaLab: https://github.com/run-llama/llama-lab

## Requirements

To use Llama Index, you will need the following:

- Python 3.6 or later
- Pip

## Installation

### Installation from Pip

You can simply do run the following command:

```
pip install llama-index
```

### Installation from Source

1. Git clone this repository
   ```
   git clone git@github.com:jerryjliu/llama_index.git
   ```
2. Install the required Python packages using pip
   ```
   pip install -r requirements.txt
   ```

## Official Installation Guide

You can follow the official installation guide <a href="https://gpt-index.readthedocs.io/en/stable/getting_started/installation.html">here</a>

## Usage

To use Llama Index, follow these steps:

### Indexing

1. Index the data. This step is crucial to ensure that the data is in the correct format for Llama Index to use. For more information about how indexing works in Llama index, you can refer to <a href="https://gpt-index.readthedocs.io/en/stable/guides/primer/index_guide.html">this article</a>.

2. To build indexes, create a file with `.py` extension. Open the file in any text editor preferably `VSCode`.

3. Import the dependencies:

   ```python
   from llama_index import GPTVectorStoreIndex, SimpleDirectoryReader
   ```

4. Read the file from the directory with a `SimpleDirectoryReader`:

   ```python
   documents = SimpleDirectoryReader('data').load_data()
   ```

5. Create the indexes from that file:

   ```python
   index = GPTVectorStoreIndex.from_documents(documents)
   ```

The `index` variable now contains the indexes for the data. You can use this variable to query the data. The completed code should look like this:

```python
from llama_index import GPTVectorStoreIndex, SimpleDirectoryReader

documents = SimpleDirectoryReader('data').load_data()
index = GPTVectorStoreIndex.from_documents(documents)
```

### Querying

1. To query our data, we'd require the index that we created earlier. The index is saved in `index` variable. We can use this variable to query the data. Let's first create a query engine from the index:

   ```python
   query_engine = index.as_query_engine()
   ```

2. Give the query engine a prompt and it will return the most relevant results:

   ```python
   response = query_engine.query("What did the author do growing up?")
   ```

3. Simply, print the response to see the results:

   ```python
   print(response)
   ```

The completed code should look like this:

```python
from llama_index import GPTVectorStoreIndex, SimpleDirectoryReader

documents = SimpleDirectoryReader('data').load_data()
index = GPTVectorStoreIndex.from_documents(documents)
query_engine = index.as_query_engine()
response = query_engine.query("What did the author do growing up?")
print(response)
```

### Saving Indexes for Future Use

1. Since indexing is an expensive process, we cannot afford to do it everytime our code runs. So, we need a way to save these indexes and then, read them later on for querying. To save the indexes, we can use the `persist` method on the index:

   ```python
   index.storage_context.persist()
   ```

2. To reload the index from the disk, we can use the method `load_index_from_storage` method from `llama_index`.

   ```python
   from llama_index import StorageContext, load_index_from_storage

   # rebuild storage context
   storage_context = StorageContext.from_defaults(persist_dir="./storage")
   # load index
   index = load_index_from_storage(storage_context)
   ```

### Reading an Excel File

1. To read an excel file, we'll have to install a loader for Llama index.
2. We do not need to install the loader through any `pip` commands, instead, we can do so through this simple code snippet.

   ```python
   from pathlib import Path
   from llama_index import download_loader

   PandasExcelReader = download_loader("PandasExcelReader")

   loader = PandasExcelReader()
   documents = loader.load_data(file=Path('./data.xlsx'), pandas_config={"header":0})
   ```

3. This loader will load all the data from that Excel file including sheets.
4. If you want to install other loaders, you can do so through <a href="https://llamahub.ai/">Llama Hub</a>
