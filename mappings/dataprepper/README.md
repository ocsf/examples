# Data Prepper

Data Prepper is a data ingestion and transformation framework designed to streamline the process of preparing data for analysis and consumption. It offers a flexible architecture with various processors, inputs, and sinks to accommodate a wide range of data sources and destinations.

For more specific instructions on getting started with Data Prepper, please visit the [OpenSearch Data Prepper documentation](https://opensearch.org/docs/latest/data-prepper/getting-started/).


## Overview

Data Prepper follows the ETL (Extract, Transform, Load) paradigm:

- **Extract**: Data is extracted from various sources such as Kafka, files, or HTTP endpoints.
- **Transform**: The extracted data is transformed using configurable processors to enrich, filter, or modify it.
- **Load**: The transformed data is loaded into sinks such as Elasticsearch, Kafka, or files for storage, analysis, or further processing.

## Processors

Processors perform an action on your data, such as filtering, transforming, or enriching.

### Add Entry Processor Example
      - add_entries:
          entries:
            - key: category_uid
              value: 4

### Rename Processor Example
    processors:
      - rename:
          field: ip
          target_field: "src_endpoint/ip"

### Date Processor
    processors:
      - date:
          field: "timestamp"
          target_field: "time_dt"
          formats:
            - "ISO8601"

### Grok Processor
    processors:
      - grok:
          field: "message"
          patterns:
            - "%{IP:client_ip} %{USER:client_user}"

### Convert Processor
    processors:
      - convert:
          field: "src_endpoint/port"
          type: "integer"

### Remove Processor
    processors:
      - remove:
          field: "field_name"


## Inputs

Data Prepper supports various input sources for ingesting data into the pipeline. Some of the supported input types are:

### 1. Kafka Input

You can use the Apache Kafka source (kafka) in Data Prepper to read records from one or more Kafka topics. These records hold events that your Data Prepper pipeline can ingest. The kafka source uses Kafka’s Consumer API to consume messages from the Kafka broker, which then creates Data Prepper events for further processing by the Data Prepper pipeline.

### 2. HTTP Input

http_source is a source plugin that supports HTTP. Currently, http_source only supports the JSON UTF-8 codec for incoming requests, such as [{"key1": "value1"}, {"key2": "value2"}]. The following table describes options you can use to configure the http_source source.

## Sinks

Data Prepper supports multiple sink types for storing or forwarding processed data. Some of the available sink options include:

### 1. Opensearch Sink

You can use the opensearch sink plugin to send data to an OpenSearch cluster, a legacy Elasticsearch cluster, or an Amazon OpenSearch Service domain.

### 2. S3 Sink

The s3 sink saves and writes batches of Data Prepper events to Amazon Simple Storage Service (Amazon S3) objects. The configured codec determines how the s3 sink serializes the data into Amazon S3.

### 3. File Sink

Use the file sink to create a flat file output, usually a .log file.
