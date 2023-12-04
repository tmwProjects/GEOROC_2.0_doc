# Writing API query

## Introduction

In our example for accessing the data, we describe the technical implementation via the GEOROC 2.0 API using a total of 
3 endpoints to obtain geochemical measurement data. Depending on the requirements of your project, you should consult 
the official [technical documentation of the API](https://api-test.georoc.eu/api/v1/docs/index.html#/) to select and customise the appropriate endpoints for your needs.

This example has been successfully tested under the following system requirements and versions:

```bash
Python Version: 3.11.6

Operating system:
  * Ubuntu 22.04.3 LTS 
  
IDE: 
  * PyCharm 2022.2.3 (Community Edition)

Libraries:
  * requests Version: 2.31.0
  * json Version: 2.0.9
```

***

In Python programmes, import instructions are usually at the beginning of the code. They integrate external modules or 
libraries that provide additional functionalities. These imports have the following meanings:

**import requests**: Includes the requests module, which is used for sending HTTP requests to web servers. It is particularly 
useful for interacting with web APIs.

**import json**: Adds the json module, which provides functions for processing JSON data. It enables the parsing of JSON 
strings into Python objects and vice versa.

**import sys**: Integrates the sys module, which provides functions for interacting with the Python interpreter, such as 
terminating a script with a specific exit code.

```python
import requests
import json
import sys
```

The first part of the code defines basic elements for the API interaction:

API key **(api_key)**: This is a string that is used for authentication with the API. It ensures that only authorised users 
have access to the API.

Base URL **(base_url)**: It defines the basic address of the API. All endpoint calls are formulated relative to this base URL.

Header **(headers)**: A dictionary containing the necessary HTTP headers for the requests, including accepting JSON formats 
and including the API key.

This initialisation creates the basis for subsequent communication with the API and ensures secure and standardised interaction.

```python
api_key = "your_api_key_here"

base_url = "https://api-test.georoc.eu/api/v1/"

headers = {
        "accept": "application/json",
        "DIGIS-API-ACCESSKEY": api_key
}
```

***

The second part of the code contains the api_query function:

**Purpose**: This function is designed to send GET requests to various endpoints of the API and process the responses.

Parameters:

**endpoint**: Specifies the specific endpoint of the API to which the request is sent.

**params (optional)**: Contains additional parameters for the request.

**Processing logic**: The function uses the requests library to execute the GET request. It checks the status code of the 
response: If the status code is 200, the response is interpreted as JSON and returned; if the status code is not 200, 
an error message is issued and None is returned.

The **api_query** function thus demonstrates an efficient and structured approach to performing and handling API requests in 
Python. It emphasises the importance of error handling and provides a user-friendly method for interacting with web APIs.

```python
def api_query(endpoint, params=None):
    response = requests.get(f"{base_url}{endpoint}",headers=headers, params=params)
    if response.status_code == 200:Python Version: 3.11.6
        data = json.loads(response.text)
        print(f"\nAPI query successful for endpoint:{endpoint}")
        print("+---------------------------------------------------------------------+")
        return data
    else:
        print(f"API query error for endpoint: {endpoint}, Statuscode:{response.status_code}")
        print("+---------------------------------------------------------------------+")
        print(response.text)
        return None
```

```Bash
Output:

API query successful for endpoint:ping
+---------------------------------------------------------------------+
```

***

The **check_api_connection()** function is designed to validate connectivity with an API server. This function initiates a 
call to the ping endpoint of the relevant API and checks the response to confirm the availability of the server.

In the event of a successful connection, the function generates a confirmation message indicating the successful 
establishment of the connection. In the opposite scenario, if the connection fails, the function triggers an error 
message and terminates the executing programme using sys.exit(1). This specific action communicates an error status.

The particular relevance of this function lies in its ability to check the accessibility of the API at the beginning of 
the execution of a script. This so-called initial check is essential to ensure that subsequent, API-dependent operations 
of the script are not initiated if the API is not available. This procedure helps to avoid unnecessary execution of 
script parts that would be doomed to failure without an established API connection.

```python
def check_api_connection():
    endpoint = "ping"
    response = api_query(endpoint)

    if response is not None:
        print("Connection to API server successful!")
        print("+---------------------------------------------------------------------+")
    else:
        print("Failed to connect to API server!")
        print("+---------------------------------------------------------------------+")
        sys.exit(1)

check_api_connection()
```

```Bash
Output:

Connection to API server successful!
+---------------------------------------------------------------------+
```

***

The **get_filtered_samples()** function is designed to retrieve filtered data from an API based on a number of parameters. 
of parameters. It allows specific queries to be sent to the API by defining various filter criteria such as geographic location 
filter criteria, such as geographic location, rock types, publication dates and more.

##### Here is a short overview:

**Parameters of the function**:

The function accepts a wide range of parameters (e.g. limit, offset, rocktype, agemin, etc.) that allow the user to specify the query. 
to specify the query. Each parameter corresponds to a possible filter criterion in the API query.


**Structure of the query**:

The function creates a query by converting the transferred parameters into a dictionary (filters). In doing so 
parameters that are not None are taken into account to ensure that only relevant filters are sent to the API. 
are sent to the API.


**API call**:

The function then calls the **api_query** function, passes it the endpoint (queries/samples) and the created filters 
as parameters. This functionality makes it possible to dynamically retrieve data based on the passed filter criteria.


**Returning the data**:

Finally, the function returns the data returned by the API. This data corresponds to the set 
filter criteria and can be used for further analyses or processing.

```python
def get_filtered_samples(
        limit=None,
        offset=None,
        setting=None,
        location1=None,
        location2=None,
        location3=None,
        latitude=None,
        longitude=None,
        rocktype=None,
        rockclass=None,
        mineral=None,
        material=None,
        inclusiontype=None,
        sampletech=None,
        chemistry=None,
        title=None,
        publicationyear=None,
        doi=None,
        firstname=None,
        lastname=None,
        agemin=None,
        agemax=None,
        geoage=None,
        geoageprefix=None,
        lab=None,
        polygon=None,
        addcoordinates=None #Boolian value True/False
):

    endpoint = "queries/samples"

    filters = {
        key: value
        for key, value in locals().items()
        if key not in ["endpoint"] and value is not None
    }

    data = api_query(endpoint, params=filters)
    return data
```

```Bash
Output:

API query successful for endpoint:queries/samples
+---------------------------------------------------------------------+
```

***

#### Using the get_filtered_samples() function

To use the **get_filtered_samples()** function effectively, follow these steps, which are illustrated using a concrete example. 
illustrated using a concrete example:

1. call the function with specific parameters:

Use **limit="1"** to limit the number of records returned to one.
Set location1, location2 and location3 to specify geographical locations.
Use **rocktype="PLU"** to specify the rock type to be filtered in the query.

2. expectations of the function:

The function aims to retrieve data that exactly matches the set filter criteria.
This includes filtering by specific tectonic zones, geographic locations and rock types.

3. interpretation of the output:

After the call you will receive an output as follows:

**numItems**: Displays the number of records that were actually returned.

**totalCount**: Indicates the total number of data records that match the filter criteria.

**data**: A list of the filtered data containing specific information about each sample, such as sampleID and geographic 

coordinates (latitude and longitude).

```python
filtered_samples_combined = get_filtered_samples(
    limit="1",
    location1="CENTRAL INDIAN TECTONIC ZONE",
    location2="BANGLADESH",
    location3="MADDHAPARA; INDIA",
    rocktype="PLU"
    # Add further parameters if required
)

print(filtered_samples_combined)
```

```Bash
Output:

{'numItems': 1, 'totalCount': 10, 'data': [{'sampleID': 495504, 'latitude': 0, 'longitude': 0}]}
```

This function can be used with all possible parameters from the documentation. If you want to use these examples 
directly, be sure to use the **api_query** function in your code so that the **get_filtered_samples** function works 
correctly.

***

### Filter DSL

Die Filter DSL (Domain-Specific Language) Syntax für die get_filtered_samples Funktion in der API ermöglicht eine 
flexible und leistungsstarke Art, Daten abzufragen. Hier ist eine detaillierte Beschreibung, wie Sie diese Syntax im 
Zusammenhang mit den Parametern nutzen können:

#### Basic concept

**Syntax**: FIELD=OPERATOR:VALUE

**FIELD**: A field is one of the accepted query parameters. This could be any parameter, such as location1, agemin, rocktype etc.

OPERATOR**: An operator defines the type of query. Various operators are available:

* "**lt**" (less than, <)
* "**gt**" (greater than, >)
* "**eq**" (equal to, =)
* "**in**" (within a list)
* "**lk**" (similar, LIKE in SQL)
* "**btw**" (between, BETWEEN in SQL)

**VALUE**: The value against which the field is compared. This can be an unquoted string, an integer or a decimal number.

##### Operators and their use

"**lt**" and "**gt**":
Only applicable to numerical values.

> **Example**: agemin=lt:100 (age less than 100)

"**eq**":
Standard operator if no other is specified.
Can be used for any value type.

> **Example**: rocktype=eq:Basalt (Rocktype equals Basalt)

"**in**":
For filtering within a list of values.
The values must be separated by commas.

> **Example**: location1=in:USA,Canada,Mexico (Location1 in one of the specified regions)

"**lk**":
Only for character strings.
Supports wildcards * (for any number of characters) and ? (for a single character).

> **Example**: title=lk:Geology* (title begins with "Geology")

"**btw**":
For numeric ranges.
Takes two values separated by commas.
If a value is missing, 0 or 9999999 is assumed by default.

> **Example**: agemin=btw:100,200 (age between 100 and 200)


##### Example of use

Suppose you want to find samples that come from a certain region, are of a certain age and correspond to a certain type of rock. 
age and correspond to a certain type of rock. You could then use the following filters:

```python
filtered_samples_combined = get_filtered_samples(
    location1="eq:CENTRAL INDIAN TECTONIC ZONE",
    agemin="gt:150",
    rocktype="eq:Granite"
)
```

> **Notes**:
> 
> * The use of multiple filters can slow down the query, as more tables have to be taken into account in the evaluation.
> 
> 
> * The filters are evaluated conjunctively, i.e. all conditions must be met for an entry to be included in the result.