# API response

When you send a request to an API, you usually receive a response that contains data in JSON format. JSON stands for 
JavaScript Object Notation and is a widely used, lightweight data exchange format that can be easily read and processed 
by both humans and machines. An API response generally consists of the following components:

## Status code: 

The HTTP status code indicates whether the request was successful or not. A status code in the range of 200 to 299 
usually indicates a successful request, while codes in the range of 400 to 499 indicate client errors and codes in the 
range of 500 to 599 indicate server errors.

## Headers: 

The headers contain meta-information about the response, such as the content type (usually application/json for 
JSON data) and possibly additional pagination or authentication information.

## Data: 

The actual data returned in the API response is usually structured in JSON format. JSON data represents hierarchical 
or nested data structures in the form of key-value pairs. In Python, JSON data can be easily converted into native 
data structures such as dictionaries or lists.

Here is an example of a typical JSON response (response body) from an API of the Georoc database according to our 
pre-written Python code:

> **Note**: Please note that the response body has been shortened for reasons of clarity.

```json
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
                ...
                "BE",
                "ER",
                "HO"
            ],
            "itemGroup": [
                "te",
                "te",
                "mj",
                ...
                "te",
                "ree",
                "ree"
            ],
            "standardNames": [
                "",
                "",
                "",
                ...
                "",
                "",
                ""
            ],
            "standardValues": [
                null,
                null,
                null,
                ...
                null,
                null,
                null
            ],
            "values": [
                120,
                3.1,
                0.99,
                ...
                2,
                1.79,
                0.65
            ],
            "units": [
                "PPM",
                "PPM",
                "WT%",
                ...,
                "PPM",
                "PPM",
                "PPM"
            ]
        }
    ]
}
```

### Here is a description of the most important elements and their meaning:

**numItems**: The number of items contained in the response. In this case, there is only one element.

**data**: A list containing the actual data. Each element in this list represents a single sample.

**sampleNum**: The unique number of the sample.

**uniqueID**: A unique identification number for the sample, but empty here.

**batches**: A list of batch numbers associated with the sample.

**references**: A list of references containing information about the sources related to the sample.

**authors**: A list of authors involved in the studies or publications related to this sample.

**reference**: Contains details such as DOI, journal title, page number, reference number, title of the study and year of publication.

**sampleid**: The ID associated with the sampling feature.

**sampleName**: The name of the sample.

**locationNames**: A list of geographic names associated with the sample.

**locationTypes**: The type of geographic locations associated with the locationNames.

**elevationMin and elevationMax**: The minimum and maximum elevation of the sampling locations.

**landOrSea**: Indicates whether the sample is from land or sea.

**rockTypes, rockClasses, rockTextures**: Information about the rock type, rock class and rock texture.

**ageMin and ageMax**: The minimum and maximum age of the sample.

**materials, minerals, inclusionTypes**: Lists of materials, minerals and inclusion types found in the sample.

**locationNum**: A number that identifies the geographic location of the sample.

**latitude, longitude, latitudeMin, latitudeMax, longitudeMin, longitudeMax**: Geographical coordinates of the sample.

**tectonicSetting**: The tectonic setting of the sample location.

**method**: The methods used to analyse the sample.

**comment**: Comments or additional notes about the sample.

**institutions**: The institutions associated with the analysis of the sample.

**itemName, itemGroup, standardNames, standardValues, values, units**: Detailed chemical analysis results of the sample, including the names of the measured items, their groupings, standard names and values, the measured values and the units of these values.

This data structure provides a comprehensive overview of the sample, including its geographical, geological and chemical 
properties as well as the associated scientific literature.
