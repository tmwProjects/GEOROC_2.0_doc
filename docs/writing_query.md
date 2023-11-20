# Writing simple API query

First, install the required Python libraries and import the modules:

```bash
pip install requests
```

Then you should import the relevant modules into your Python document:

```python
import requests
import json
import pandas as pd
```

Define your API key, base URL and headers for the API request:

```python
api_key = "your_api_key_here"

base_url = "https://api-test.georoc.eu/api/v1/"

headers = {
        "accept": "application/json",
        "DIGIS-API-ACCESSKEY": api_key
}
```

Create a function to perform API queries for different endpoints:

```python
def api_query(endpoint, params=None):
    response = requests.get(f"{base_url}{endpoint}",headers=headers, params=params)
    if response.status_code == 200:
        data = json.loads(response.text)
        print(f"API query successful for endpoint:{endpoint}")
        return data
    else:
        print(f"API query error for endpoint: {endpoint}, Statuscode:{response.status_code}")
        print(response.text)
        return None
```
Use the api_query function to retrieve data from different endpoints:

Retrieve location data:

```python
sites_data = api_query("queries/sites")
```

Retrieve first level location information:

```python
locations_l1_data = api_query("queries/locations/l1")
```

Get second level location information:

```python
locations_l2_data = api_query("queries/locations/l2")
```

Get third level location information:

```python
locations_l3_data = api_query("queries/locations/l3")
```

Authors retrieve:

```python
authors_data = api_query("queries/authors")
```

Retrieve authors by PersonID:

```python
person_id = 1
authors_by_id_data = api_query(f"queries/authors/{person_id}")
```

Retrieve quotes:

```python
citations_data = api_query("queries/citations")
```

Retrieve citations by CitationID:

```python
citation_id = 1
citations_by_id_data = api_query(f"queries/
citations/{citation_id}")
```

Retrieve complete datasets by SamplingFeatureID:

```python
sampling_feature_id = 1
full_data_data = api_query(f"queries/fulldata/{sampling_feature_id}")
```

Retrieve all SamplingFeatureIDs filtered by different fields:

```python
samples_data = api_query("queries/samples")
```

Write a function that uses the endpoint "SamplingFeatureID" with all available parameters and retrieves the results according to any filter criteria:

```python
def get_filtered_samples(
    limit=None,
    offset=None,
    settings=None,
    location1=None,
    location2=None,
    location3=None,
    rocktype=None,
    rockclass=None,
    mineral=None,
    element=None,
    elementtype=None,
    materials=None,
    inclusiontypes=None,
    samplingtechniques=None,
    elements=None,
    elementtypes=None
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

You can use this function to generate precise data based on the filter parameters obtained.
Example: Apply multiple filters simultaneously:print(filtered_samples_combined)

```python
filtered_samples_combined = get_filtered_samples(
    limit="1",
    location1="CENTRAL INDIAN TECTONIC ZONE",
    location2="BANGLADESH",print(filtered_samples_combined)
    location3="MADDHAPARA; INDIA",
    rocktype="PLU"
)
```
This function can be used with all possible parameters from the documentation. If you want to use these examples 
directly, be sure to use the **api_query** function in your code so that the **get_filtered_samples** function works 
correctly.

Additional endpoints and parameters can be used according to the [API documentation](https://api-test.georoc.eu/api/v1/docs/index.html#/).