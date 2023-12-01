# Data extraction

## Extract the SampleID from the Response body

To do this, you can use the filtered_samples_combined variable that contains the response body of the API call. Since 
the API response is a list of objects, you can extract the SampleID from the first object in the list:

```python
def extract_sample_ids(filtered_samples):
    return [sample['sampleID'] for sample in filtered_samples['data']]

print(extract_sample_ids(filtered_samples_combined))
```

```Bash
Output:

[495504]
```

***

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

# Optional: Ausgabe der Daten für jede SampleID
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