# Data Prepper

Data Prepper is a data ingestion and transformation framework designed to streamline the process of preparing data for analysis and consumption. It offers a flexible architecture with various processors, inputs, and sinks to accommodate a wide range of data sources and destinations.

## Overview

Data Prepper follows the ETL (Extract, Transform, Load) paradigm:

- **Extract**: Data is extracted from various sources such as Kafka, files, or HTTP endpoints.
- **Transform**: The extracted data is transformed using configurable processors to enrich, filter, or modify it.
- **Load**: The transformed data is loaded into sinks such as Elasticsearch, Kafka, or files for storage, analysis, or further processing.

## Processors

Data Prepper provides several processors to perform transformations and enrichment on ingested data. Some of the key processors include:

### 1. [Filter Processor]([https://link-to-filter-processor-docs]([https://opensearch.org/docs/latest/data-prepper/pipelines/configuration/processors/processors/](https://opensearch.org/docs/latest/data-prepper/pipelines/configuration/sources/sources/)))

Sources define where your data comes from within a Data Prepper pipeline.

### 2. [Filter Processor]([https://link-to-filter-processor-docs](https://opensearch.org/docs/latest/data-prepper/pipelines/configuration/processors/processors/))

The Filter Processor allows users to specify conditions for filtering out unwanted data records before they are sent to sinks.

### 3. [Transformation Processor](https://link-to-transformation-processor-docs)

The Transformation Processor facilitates data format conversion, schema normalization, and other transformations to make the data suitable for downstream analysis.

## Inputs

Data Prepper supports various input sources for ingesting data into the pipeline. Some of the supported input types are:

### 1. [Kafka Input](https://link-to-kafka-input-docs)

The Kafka Input allows Data Prepper to consume data from Apache Kafka topics, enabling real-time data ingestion and processing.

### 2. [File Input](https://link-to-file-input-docs)

With the File Input, users can ingest data from files stored in local directories or remote file systems, providing flexibility in data source selection.

### 3. [HTTP Input](https://link-to-http-input-docs)

The HTTP Input enables data ingestion from HTTP endpoints, making it convenient to integrate with web services and APIs.

## Sinks

Data Prepper supports multiple sink types for storing or forwarding processed data. Some of the available sink options include:

### 1. [Elasticsearch Sink](https://link-to-elasticsearch-sink-docs)

The Elasticsearch Sink sends processed data to Elasticsearch for indexing and analysis, making it ideal for log processing and search applications.

### 2. [Kafka Sink](https://link-to-kafka-sink-docs)

With the Kafka Sink, Data Prepper can publish processed data to Kafka topics, facilitating seamless integration with downstream Kafka consumers.

### 3. [File Sink](https://link-to-file-sink-docs)

The File Sink writes processed data to files stored in local directories or remote file systems, providing a simple yet versatile storage option.

## Getting Started

To get started with Data Prepper, follow these steps:

1. Clone the Data Prepper repository.
2. Install any necessary dependencies.
3. Configure your inputs, processors, and sinks in the Data Prepper configuration file.
4. Run Data Prepper with your configuration to start ingesting and processing data.

For detailed installation instructions and usage guidelines, refer to the official documentation.

## Contributing

Contributions to Data Prepper are welcome! Whether you want to report a bug, request a feature, or submit a pull request, please follow the contribution guidelines outlined in the repository.

## License

Data Prepper is licensed under the Apache License 2.0. See the LICENSE file for more details.
