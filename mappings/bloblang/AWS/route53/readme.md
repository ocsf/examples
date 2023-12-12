# What is Benthos 

### If you have not already check out  https://www.benthos.dev/ 

- **Prerequisites**: 
    - `Example mappings assume your data is already transformed into JSON.`
    - `The examples use Kafka topics where the data is already filtered upstream. (you can use whatever input and output you like but we use kafka for examples)`

- **Stream Processing**:
    - `the logic in the mappings require that you understand the basics of stream processing and the order in which it operates`
    - `(placeholder for video link)`

- **Filter Architecture**:  
    - `in the mappings I have included Benthos is imputing raw Json logs, renaming fields, applying conditional match, and introducing OCSF specific variables`
    - `Below is a visual representation of the filters in a flow diagram`
    ![AWS CloudTrail](AWS_route53.png)