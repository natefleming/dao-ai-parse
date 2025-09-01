# DAO AI Parse

A document parsing and processing project built on top of the [dao-ai](https://github.com/natefleming/dao-ai) framework for Databricks environments.

## Overview

This project provides document parsing capabilities specifically designed for Databricks workflows. It leverages the dao-ai framework to create a streamlined pipeline for processing various document types and storing them in vector databases for AI-powered applications.

## Relationship to DAO AI

This project is built as an extension of the [dao-ai](https://github.com/natefleming/dao-ai) framework:

- **dao-ai** provides the core configuration management, schema creation, and resource orchestration
- **dao-ai-parse** extends these capabilities with specialized document parsing functionality
- Uses dao-ai's `AppConfig` system for managing Databricks resources like catalogs, schemas, and vector stores
- Integrates seamlessly with dao-ai's volume path management and checkpoint handling

## Features

- **Multi-format Document Support**: Processes PDF, DOCX, HTML, PPTX, and image files
- **Advanced Text Processing**: Uses Docling for document conversion and structure preservation
- **Intelligent Chunking**: Employs LlamaIndex's SentenceSplitter for optimal text segmentation
- **Databricks Integration**: Built specifically for Databricks notebooks and streaming workflows
- **Vector Store Ready**: Outputs structured data ready for vector database indexing
- **Configurable Pipeline**: Leverages dao-ai's YAML-based configuration system

## Project Structure

```
dao-ai-parse/
├── config/
│   └── example.yaml          # Configuration example using dao-ai schema
├── notebooks/
│   └── 01_parse_documents.py # Main Databricks notebook for document processing
├── dao-ai-parse/
│   └── main.py              # Standalone Python entry point
└── pyproject.toml           # Dependencies (no library building)
```

## Dependencies

This project relies on several key libraries:

- **dao-ai**: Core framework for Databricks resource management
- **docling**: Advanced document parsing and conversion
- **llama-index**: Text chunking and document processing
- **transformers**: Tokenization for chunk size management
- **torch**: Deep learning backend for document processing
- **databricks-vectorsearch**: Vector database integration

## Configuration

The project uses dao-ai's configuration system. See `config/example.yaml` for a complete configuration example that defines:

- Unity Catalog schemas
- Vector store configurations
- Source and checkpoint volume paths
- LLM and embedding model endpoints

## Usage

### In Databricks

1. Upload documents to the configured source volume path
2. Run the `notebooks/01_parse_documents.py` notebook
3. The pipeline will:
   - Parse documents using Docling
   - Chunk text using LlamaIndex
   - Store results in Delta tables
   - Prepare data for vector indexing

## Key Components

### Document Parsing Pipeline

The parsing pipeline in `01_parse_documents.py` includes:

1. **Document Conversion**: Uses Docling with configurable PDF pipeline options
2. **Text Chunking**: Employs SentenceSplitter with 1024 token chunks and 128 token overlap
3. **Streaming Processing**: Processes documents using Spark structured streaming
4. **Delta Table Storage**: Stores parsed content with metadata in Delta format

### Configuration Integration

Leverages dao-ai's `AppConfig` for:
- Schema creation and management
- Vector store configuration
- Volume path setup and validation
- Resource orchestration

## Benefits of Using DAO AI

By building on dao-ai, this project inherits:

- **Standardized Configuration**: YAML-based config with schema validation
- **Resource Management**: Automated creation of catalogs, schemas, and volumes
- **Best Practices**: Production-ready patterns for Databricks workflows
- **Extensibility**: Easy integration with other dao-ai based projects
- **Maintenance**: Shared infrastructure and configuration patterns

## Getting Started

1. Set up your dao-ai configuration (see `config/example.yaml`)
2. Ensure your Databricks environment has the necessary permissions
3. Upload documents to your configured source volume
4. Run the parsing notebook to process your documents
5. Use the resulting Delta tables with your AI applications

For more information about the underlying framework, see the [dao-ai documentation](https://github.com/natefleming/dao-ai).
