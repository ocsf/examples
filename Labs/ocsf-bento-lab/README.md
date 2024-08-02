<!--
 Licensed to the Apache Software Foundation (ASF) under one
 or more contributor license agreements.  See the NOTICE file
 distributed with this work for additional information
 regarding copyright ownership.  The ASF licenses this file
 to you under the Apache License, Version 2.0 (the
 "License"); you may not use this file except in compliance
 with the License.  You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing,
 software distributed under the License is distributed on an
 "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
 KIND, either express or implied.  See the License for the
 specific language governing permissions and limitations
 under the License.
-->
# OpenSearch Quick start 
This is a docker compose environment to quickly get up and running with a Bento, OpenSearch environment and MinIO as a storage backend.

**note**: If you don't have docker installed, you can head over to the [Get Docker](https://docs.docker.com/get-docker/)
page for installation instructions.

## Usage
Start up the  servers by running the following.
```
docker-compose up
```
The OpenSearch dashboard server will then be available at http://localhost:5601
```
2. Drop you raw data set into the minio bucket that corresponds with the vendor data  
found here: http://localhost:9001/login.
```
user = admin
password = password

Once read the data will be deleted from the bucket and sent to the ocsf index you just created in Open search.
```

curl -s -XPUT http://localhost:9200/ocsf-3002-authentication/_settings  -H 'Content-Type: application/json' -d '{"index.mapping.total_fields.limit": 10000}'
curl -s -XPUT http://localhost:9200/ocsf-3001-account_change/_settings  -H 'Content-Type: application/json' -d '{"index.mapping.total_fields.limit": 10000}'
curl -s -XPUT http://localhost:9200/ocsf-6003-api_activity/_settings  -H 'Content-Type: application/json' -d '{"index.mapping.total_fields.limit": 10000}'
```
FYI index is set to ocsf-<class_uid>-<ocsf_bucket varrable>  
so ocsf-3002-authentication would be a class name.
```
3. proceed to Open search dashboard server and enjoy 

To stop everything, just run `docker-compose down`.

