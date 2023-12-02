# Introduction

The GEOROC database (Geochemistry of Rocks of the Oceans and Continents) is a comprehensive collection of published 
analyses of igneous and metamorphic rocks and minerals. It contains concentrations of major and trace elements, radiogenic 
and non-radiogenic isotope ratios and analytical age data for whole rocks, glasses, minerals and inclusions. The metadata 
includes geographic and other sample information, analytical details and references.

The GEOROC database, originally established at the Max Planck Institute for Chemistry in Mainz, was transferred to the 
University of Göttingen in 2021. It will continue to be maintained there as part of the DIGIS project of the Institute 
of Geochemistry and Isotope Geology at the Geosciences Centre (GZG) and the University and State Library (SUB). The development 
of GEOROC 2.0 includes a new data model for greater interoperability, options for data input and improved database access.

As part of the DIGIS project, a new API interface has been created for the GEOROC database, allowing easy access to its 
contents with basic programming skills. Users can now query the database and retrieve data via the new API, making it more 
accessible and useful for researchers and other interested parties. This Jupyter notebook demonstrates the basic capabilities 
of GEOROC data access via the new DIGIS API.

***

The programming language Python has established itself in recent years as one of the most popular languages for 
scientific applications. Especially in geoscience and geochemistry, Python is widely used due to its ease of use and 
extensive libraries. In this context, the GeoRoc API-Key 
allows access to large geochemical datasets, which are of great importance for research and analysis in this field.

This introduction provides an overview of how to work with Python to perform API queries using the GeoRoc API Key and 
associated documentation, and then proceed to work with the geochemical data obtained. First, you should familiarize 
yourself with the GeoRoc database, which was developed by the Max Planck Institute for Chemistry in Mainz, Germany. 
The database contains an extensive collection of geochemical analyses of rocks from throughout Earth's history, 
including information on sampling locations, analytical methods, and data quality. 

By using the GEOROC API, you can 
access this valuable information and use it in your own projects. To work with the GeoRoc API, one first needs an API 
key. This can be requested via the [GEOROC website](https://georoc.mpch-mainz.gwdg.de//georoc/). Once you have received 
the API key, you can consult the official documentation of the GeoRoc API to learn about the available endpoints, 
parameters and data types. The documentation also provides examples of API queries and troubleshooting tips. To use 
Python for API queries, it is recommended to use the requests library. 

This allows you to easily send HTTP requests 
and process the JSON data returned by the API. In addition, other Python libraries such as pandas and matplotlib can 
be used to efficiently analyze, visualize and further process the geochemical data obtained. Overall, the combination 
of Python and the GeoRoc API opens up access to a wealth of geochemical information that is invaluable for the study 
of Earth's history and the chemical composition of rocks. With the right tools and resources, this potential can be 
fully exploited and used in both both in academic research and in the practical application of geochemistry insights 
can be gained.
