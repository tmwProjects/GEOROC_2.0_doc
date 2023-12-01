# Data extraction

## Extract the SampleID from the Response body

In the context of the topic discussed in the previous chapter, it is necessary to transform the response body into an 
adequate list structure. This step is essential to ensure an efficient query at the 'fulldata' endpoint. The function 
specified below is intended to help realise this process:

```python
def extract_sample_ids(filtered_samples):
    return [sample['sampleID'] for sample in filtered_samples['data']]

print(extract_sample_ids(filtered_samples_combined))
```

```Bash
Output:

[495504]
```

In our minimum example, we had set the limit to 1, which meant that only one SampleID could be extracted.

***

## Obtain data using the SampleIDs

For example, in order to obtain certain measurement data for a specific sample or setting, we need another function 
that returns the data for the corresponding SampleID(s) in JSON format.

```python
def get_measurement_data(sample_ids):
    all_data = []
    for sample_id in sample_ids:
        endpoint = f"queries/fulldata/{sample_id}"
        response = api_query(endpoint)
        if response:
            all_data.append(response)
        else:
            print(f"Keine Daten gefunden für Sample ID {sample_id}")
    return all_data


sample_ids = extract_sample_ids(filtered_samples_combined)
measurement_data = get_measurement_data(sample_ids)

# Optional: Output of the data for each SampleID
for data in measurement_data:
    print(json.dumps(data, indent=4))
```

```Bash
Output:

{
    "numItems": 1,
    "data": [
        {
            "sampleNum": 495504,
            "uniqueID": "",
            "batches": [
                2070702
            ],
            "references": [
                {
                    "authors": [
                        {
                            "personfirstname": "T.",
                            "personid": 4882,
                            "personlastname": "TSUNOGAE"
                        },
                        {
                            "personfirstname": "Y.",
                            "personid": 19830,
                            "personlastname": "TSUTSUMI"
                        },
                        {
                            "personfirstname": "I.",
                            "personid": 21953,
                            "personlastname": "HOSSAIN"
                        },
                        {
                            "personfirstname": "KAZUKI",
                            "personid": 21954,
                            "personlastname": "TAKAHASHI"
                        }
                    ],
                    "reference": {
                        "doi": "10.1016/j.jseaes.2017.09.016",
                        "journal": "J. ASIAN EARTH SCI.",
                        "pages": "22-39",
                        "ref_num": 21941,
                        "title": "PETROLOGY, GEOCHEMISTRY AND LA-ICP-MS U-PB GEOCHRONOLOGY OF PALEOPROTEROZOIC BASEMENT ROCKS IN BANGLADESH: AN EVALUATION OF CALC-ALKALINE MAGMATISM AND IMPLICATION FOR COLUMBIA SUPERCONTINENT AMALGAMATION",
                        "year": 2018
                    },
                    "samplingfeatureid": 495504
                }
            ],
            "sampleName": "SL1",
            "locationNames": [
                "BANGLADESH",
                "CENTRAL INDIAN TECTONIC ZONE",
                "MADDHAPARA; INDIA"
            ],
            "locationTypes": [
                "INTRAPLATE SUBUNIT",
                "ISLAND/REGION/SITE",
                "PROVINCE/REGION"
            ],
            "elevationMin": "",
            "elevationMax": "",
            "landOrSea": "SAE",
            "rockTypes": [
                "PLU",
                "PLU"
            ],
            "rockClasses": [
                "NOT GIVEN",
                "NOT GIVEN"
            ],
            "rockTextures": [
                "",
                ""
            ],
            "ageMin": null,
            "ageMax": null,
            "materials": [
                "",
                ""
            ],
            "minerals": [
                "",
                ""
            ],
            "inclusionTypes": null,
            "locationNum": 765133,
            "latitude": 26,
            "longitude": 89,
            "latitudeMin": "26.0",
            "latitudeMax": "26.0",
            "longitudeMin": "89.0",
            "longitudeMax": "89.0",
            "tectonicSetting": "INTRAPLATE VOLCANICS",
            "method": [
                "ICPAES",
                "ICPMS",
                "IGN"
            ],
            "comment": [
                "ELAN 6000",
                ""
            ],
            "institutions": [
                ""
            ],
            "itemName": [
                "CO",
                "HF",
                "TIO2",
                "GD",
                "MNO",
                "ZN",
                "FE2O3T",
                "TM",
                "V",
                "CAO",
                "NB",
                "CE",
                "SN",
                "CR",
                "PB",
                "MGO",
                "PR",
                "CS",
                "CU",
                "BI",
                "GE",
                "Y",
                "K2O",
                "SR",
                "LOI",
                "TH",
                "LU",
                "SC",
                "ZR",
                "TA",
                "NA2O",
                "AL2O3",
                "BA",
                "TL",
                "EU",
                "DY",
                "LA",
                "TB",
                "NI",
                "RB",
                "SB",
                "U",
                "ND",
                "SIO2",
                "SM",
                "W",
                "P2O5",
                "YB",
                "GA",
                "BE",
                "ER",
                "HO"
            ],
            "itemGroup": [
                "te",
                "te",
                "mj",
                "ree",
                "mj",
                "te",
                "mj",
                "ree",
                "te",
                "mj",
                "te",
                "ree",
                "te",
                "te",
                "te",
                "mj",
                "ree",
                "te",
                "te",
                "te",
                "te",
                "te",
                "mj",
                "te",
                "mj",
                "te",
                "ree",
                "te",
                "te",
                "te",
                "mj",
                "mj",
                "te",
                "te",
                "ree",
                "ree",
                "ree",
                "ree",
                "te",
                "te",
                "te",
                "te",
                "ree",
                "mj",
                "ree",
                "te",
                "mj",
                "ree",
                "te",
                "te",
                "ree",
                "ree"
            ],
            "standardNames": [
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                ""
            ],
            "standardValues": [
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null,
                null
            ],
            "values": [
                120,
                3.1,
                0.99,
                5.31,
                0.18,
                110,
                10.08,
                0.26,
                174,
                7.2,
                6.6,
                75.2,
                1,
                120,
                19,
                5.72,
                8.96,
                3.2,
                60,
                1,
                1.6,
                18.9,
                2.38,
                715,
                1.18,
                4.1,
                0.26,
                27,
                122,
                0.46,
                2.93,
                15.64,
                770,
                0.41,
                1.64,
                3.55,
                37.2,
                0.71,
                70,
                82,
                1,
                1.5,
                34.7,
                52.51,
                6.66,
                1110,
                0.43,
                1.75,
                19,
                2,
                1.79,
                0.65
            ],
            "units": [
                "PPM",
                "PPM",
                "WT%",
                "PPM",
                "WT%",
                "PPM",
                "WT%",
                "PPM",
                "PPM",
                "WT%",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "WT%",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "WT%",
                "PPM",
                "WT%",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "WT%",
                "WT%",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "WT%",
                "PPM",
                "PPM",
                "WT%",
                "PPM",
                "PPM",
                "PPM",
                "PPM",
                "PPM"
            ]
        }
    ]
}
```

A large amount of potentially relevant data can be identified by analysing the response body in JSON format. This data 
structure is particularly important in the context of web-based applications, such as online databases for scientific 
publications. The JSON format is characterised here by its seamless integration and user-friendliness.

In addition, numerous contemporary programming languages and data analysis tools support the reading and writing of 
JSON data. This support significantly simplifies the processing of information, for example geochemical measurement data.

With regard to the specific requirements of the analysis and visualisation of such geochemical data, conversion into 
formats such as CSV or Excel can be advantageous. These formats are particularly useful if the intention is to analyse 
or manually check the data in spreadsheet software.

In the case that a detailed analysis and visualisation of the measurement data in a specific context is intended, the 
CSV format proves to be a viable alternative. For efficient data manipulation and analysis, it would be advisable to 
restructure the response body accordingly to ensure smooth compatibility with the relevant analysis libraries.

***

## CSV restructuring for measurement data analysis