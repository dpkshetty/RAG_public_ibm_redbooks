# RAG Pipeline for RedBooks

This repository provides a Retrieval-Augmented Generation (RAG) pipeline for processing and utilizing RedBooks. The RedBooks are pre-converted into markdown files using the Python library `docling`. This pipeline uses ChromaDB for vector database storage and `llama-cpp-python` for Large Language Model (LLM) inference.

## Prerequisites

Before using this project, ensure you have the following dependencies installed:

- **[ChromaDB](https://github.com/chroma-core/chroma):** A vector database for storing embeddings.
- **[llama-cpp-python](https://github.com/abetlen/llama-cpp-python):** Python bindings for running LLaMA-based models locally.

For ppc64le you can use these commands to get chroma, llama.cpp.python and other libraries:
micromamba create -n env python=3.10

micromamba install -c rocketce -c defaults pytorch-cpu scikit-learn pyyaml httptools onnxruntime "pandas<1.6.0" tokenizers

pip install -U --extra-index-url https://repo.fury.io/mgiessing --prefer-binary chromadb transformers psutil langchain sentence_transformers gradio==3.50.2 llama-cpp-python




## Manual Installation

Install the other libraries with pip for x86 and with conda (rocketce or defaults as the channel)

## Usage

### 1. Convert the pdf files into a markdown file

1. Run the `converter_docling.py` script:
   ```bash
   python converter_docling.py
   ```

### 2. Generate the Vector Database

To generate the vector database from your markdown files:

1. Run the `chromaDB_md.py` script:
   ```bash
   python chromaDB_md.py
   ```
2. This will create a vector database in the `/db` directory. The database includes **5 collections**, each corresponding to a markdown file.

### 3. Configure the LLM

To use the Large Language Model with the context from the vector DB (LLM):

1. Open `run_model.py` in your preferred text editor.
2. Update the `model:path` variable to point to your **GGUF model**.

### 4. Run the LLM

Execute the pipeline by running:
```bash
python run_model.py
```

This will start serving the gradio UI over HTTP port `8082` 

## Alternative Installation: Ansible Playbooks

Alternatively this demo can be installed on a remote or local ppc64le RHEL host using the ansible playbook in the `ansible` directory.

For possible configuration options see the [example inventory file](ansible/example-inventory.yml).

## Folder Structure

- `/db`: Contains the vector database with collections generated by ChromaDB.
- `chromaDB_md.py`: Script for creating the vector database.
- `run_model.py`: Script for running the RAG pipeline using the configured LLM.

## Notes

- Ensure the RedBooks markdown files are in the expected format before running the pipeline.
- Make sure the GGUF model is compatible with `llama-cpp-python`.

## Contributing

If you would like to contribute to this project, feel free to fork the repository, make changes, and submit a pull request. 

## License

This project is licensed under the [MIT License](LICENSE). Feel free to use, modify, and distribute this project.

---

Happy experimenting with the RAG Pipeline for RedBooks!

