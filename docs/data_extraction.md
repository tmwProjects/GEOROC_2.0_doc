# Data extraction

## Extract the SamplingFeatureID from the Response body

To do this, you can use the filtered_samples_combined variable that contains the response body of the API call. Since 
the API response is a list of objects, you can extract the SamplingFeatureID from the first object in the list:

```python
sampling_feature_id = filtered_samples_combined[0]["samplingFeatureID"]
```

## Extracting specific parameters from the response body using the SamplingFeatureID

Now that you have the SamplingFeatureID, you can create a function to query the geochemical data of the Georoc 
database. Use the fulldata API endpoint documentation to do this:

```python
def get_geochemical_data(sampling_feature_id):
    endpoint = f"queries/fulldata/{sampling_feature_id}"
    data = api_query(endpoint)
    return data
```

Call the function get_geochemical_data with the extracted SamplingFeatureID to retrieve the geochemical data:

```python
geochemical_data = get_geochemical_data(sampling_feature_id)
```

Now you can use the following lines to query the parameters defined in this way from the response body. In this 
example, they are the name abbreviations of the chemical elements, their measured values, size unit and whether 
they are major oxides, trace elements or REEs.

```python
item_groups = geochemical_data[0]["item_Group"]
item_names = geochemical_data[0]["item_Name"]
values = geochemical_data[0]["values"]
units = geochemical_data[0]["units"]
```

After the data has been extracted, it can be transferred into a Python object. We use the Pandas module to store the 
data in a Pandas data frame.

```python
geochemical_data_df = pd.DataFrame(
    {
        "Item_Group": item_groups,
        "Item_Name": item_names,
        "Value": values,
        "Unit": units,
    }
)
```
If required, the data transferred in this way can be examined once with the following line:

```python
print(geochemical_data_df)
```

From now on, the data received can be further processed and analysed. There are good modules for Python in the 
scientific context for this, such as Scipy, matplotlib, numby or math.
