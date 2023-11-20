# API response

When you send a request to an API, you usually receive a response that contains data in JSON format. JSON stands for 
JavaScript Object Notation and is a widely used, lightweight data exchange format that can be easily read and processed 
by both humans and machines. An API response generally consists of the following components:

#### Status code: 

The HTTP status code indicates whether the request was successful or not. A status code in the range of 200 to 299 
usually indicates a successful request, while codes in the range of 400 to 499 indicate client errors and codes in the 
range of 500 to 599 indicate server errors.

#### Headers: 

The headers contain meta-information about the response, such as the content type (usually application/json for 
JSON data) and possibly additional pagination or authenti cation information.

#### Data: 

The actual data returned in the API response is usually structured in JSON format. JSON data represents hierarchical 
or nested data structures in the form of key-value pairs. In Python, JSON data can be easily converted into native 
data structures such as dictionaries or lists.

Here is an example of a typical JSON response (response body) from an API of the Georoc database according to our 
pre-written Python code:

```json
[
  {
    "isFieldSpecimen": true,
    "samplingFeatureID": 12345,
    "specimenMediumCV": "string",
    "specimenTypeCV": "string"
  }
]
```