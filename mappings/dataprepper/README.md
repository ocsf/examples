# Data Prepper

Data Prepper is a data ingestion and transformation framework designed to streamline the process of preparing data for analysis and consumption. It offers a flexible architecture with various processors, inputs, and sinks to accommodate a wide range of data sources and destinations.

## Overview

Data Prepper follows the ETL (Extract, Transform, Load) paradigm:

- **Extract**: Data is extracted from various sources such as Kafka, files, or HTTP endpoints.
- **Transform**: The extracted data is transformed using configurable processors to enrich, filter, or modify it.
- **Load**: The transformed data is loaded into sinks such as Elasticsearch, Kafka, or files for storage, analysis, or further processing.

## Inputs

# OpenSearch Data Prepper - Basic Processors Syntax Examples

Processors perform an action on your data, such as filtering, transforming, or enriching.

### Append Processor
    processors:
      - append:
          field: "new_field"
          value: "example_value"

### Convert Processor
    processors:
      - convert:
          field: "field_name"
          type: "integer"

### Date Processor
    processors:
      - date:
          field: "date_field"
          target_field: "new_date_field"
          formats:
            - "ISO8601"

### Grok Processor
    processors:
      - grok:
          field: "message"
          patterns:
            - "%{IP:client_ip} %{USER:client_user}"

### Remove Processor
    processors:
      - remove:
          field: "field_name"

### Rename Processor
    processors:
      - rename:
          field: "old_field"
          target_field: "new_field"


## Inputs

Data Prepper supports various input sources for ingesting data into the pipeline. Some of the supported input types are:

### 1. [Kafka Input]([https://link-to-kafka-input-docs](https://opensearch.org/docs/latest/data-prepper/pipelines/configuration/sources/kafka/))

You can use the Apache Kafka source (kafka) in Data Prepper to read records from one or more Kafka topics. These records hold events that your Data Prepper pipeline can ingest. The kafka source uses Kafka’s Consumer API to consume messages from the Kafka broker, which then creates Data Prepper events for further processing by the Data Prepper pipeline.

### 2. [HTTP Input]([https://link-to-http-input-docs](https://opensearch.org/docs/latest/data-prepper/pipelines/configuration/sources/http-source/))

http_source is a source plugin that supports HTTP. Currently, http_source only supports the JSON UTF-8 codec for incoming requests, such as [{"key1": "value1"}, {"key2": "value2"}]. The following table describes options you can use to configure the http_source source.

## Sinks

Data Prepper supports multiple sink types for storing or forwarding processed data. Some of the available sink options include:

### 1. [Opensearch Sink]([https://link-to-elasticsearch-sink-docs](https://opensearch.org/docs/latest/data-prepper/pipelines/configuration/sinks/opensearch/))

You can use the opensearch sink plugin to send data to an OpenSearch cluster, a legacy Elasticsearch cluster, or an Amazon OpenSearch Service domain.

### 2. [S3 Sink]([https://link-to-kafka-sink-docs](https://opensearch.org/docs/latest/data-prepper/pipelines/configuration/sinks/s3/))

The s3 sink saves and writes batches of Data Prepper events to Amazon Simple Storage Service (Amazon S3) objects. The configured codec determines how the s3 sink serializes the data into Amazon S3.

### 3. [File Sink]([https://link-to-file-sink-docs](https://opensearch.org/docs/latest/data-prepper/pipelines/configuration/sinks/file/))

Use the file sink to create a flat file output, usually a .log file.

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
