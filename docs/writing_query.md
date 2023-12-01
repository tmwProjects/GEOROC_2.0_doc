# Writing simple API query

You should import the relevant modules into your Python document:

```python
import requests
import json
import sys
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

Die Funktion check_api_connection() dient dazu, die Verbindung zu einem API-Server zu überprüfen. Sie ruft den 
ping-Endpunkt der API auf und prüft, ob eine Antwort erhalten wird.

Bei erfolgreicher Verbindung zur API zeigt sie eine Erfolgsmeldung an.
Scheitert die Verbindung, gibt sie eine Fehlermeldung aus und beendet das Programm mit sys.exit(1), was einen 
Fehlerzustand signalisiert. Diese Funktion ist besonders nützlich, um zu Beginn eines Skripts sicherzustellen, dass die 
API erreichbar ist, bevor weitere API-bezogene Operationen durchgeführt werden. Es ist eine Art von Initialcheck, um zu 
vermeiden, dass weitere Teile des Skripts ausgeführt werden, wenn keine Verbindung zur API besteht.

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

Die Funktion get_filtered_samples() ist dafür konzipiert, gefilterte Daten von einer API basierend auf einer Vielzahl 
von Parametern abzurufen. Sie ermöglicht es, spezifische Abfragen an die API zu senden, indem verschiedene Filterkriterien 
festgelegt werden, wie etwa geografische Lage, Gesteinstypen, Veröffentlichungsdaten und mehr. 

##### Hier ist eine kurze Übersicht:

Parameter der Funktion:

Die Funktion akzeptiert eine breite Palette von Parametern (z.B. limit, offset, rocktype, agemin, etc.), die es dem Benutzer 
ermöglichen, die Abfrage zu spezifizieren. Jeder Parameter entspricht einem möglichen Filterkriterium in der API-Abfrage.

Aufbau der Abfrage:

Die Funktion erstellt eine Abfrage, indem sie die übergebenen Parameter in ein Dictionary (filters) umwandelt. Dabei 
werden nur die Parameter berücksichtigt, die nicht None sind, um sicherzustellen, dass nur relevante Filter an die API 
gesendet werden.

API-Aufruf:

Die Funktion ruft dann die api_query Funktion auf, übergibt ihr den Endpunkt (queries/samples) und die erstellten Filter 
als Parameter. Diese Funktionsweise ermöglicht es, dynamisch Daten basierend auf den übergebenen Filterkriterien abzurufen.

Rückgabe der Daten:

Schließlich gibt die Funktion die von der API zurückgegebenen Daten zurück. Diese Daten entsprechen den gesetzten 
Filterkriterien und können für weitere Analysen oder Verarbeitungen verwendet werden. 

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

#### Nutzung der get_filtered_samples() Funktion

Um die get_filtered_samples() Funktion effektiv zu nutzen, folgen Sie diesen Schritten, die anhand eines konkreten 
Beispiels illustriert werden:

1. Aufrufen der Funktion mit spezifischen Parametern:

Verwenden Sie limit="1", um die Anzahl der zurückgegebenen Datensätze auf einen zu beschränken.
Setzen Sie location1, location2 und location3, um geografische Orte festzulegen.
Bestimmen Sie mit rocktype="PLU" den Gesteinstyp, der in der Abfrage gefiltert werden soll.

2. Erwartungen an die Funktion:

Die Funktion zielt darauf ab, Daten abzurufen, die genau den gesetzten Filterkriterien entsprechen.
Dies beinhaltet die Filterung nach spezifischen tektonischen Zonen, geografischen Orten und Gesteinstypen.

3. Interpretation des Outputs:

Nach dem Aufruf erhalten Sie eine Ausgabe wie folgt:
numItems: Zeigt die Anzahl der Datensätze an, die tatsächlich zurückgegeben wurden.
totalCount: Gibt die Gesamtzahl der Datensätze an, die den Filterkriterien entsprechen.
data: Eine Liste der gefilterten Daten, die spezifische Informationen über jede Probe enthält, wie sampleID und geografische Koordinaten (latitude und longitude).

```python
filtered_samples_combined = get_filtered_samples(
    limit="1",
    location1="CENTRAL INDIAN TECTONIC ZONE",
    location2="BANGLADESH",
    location3="MADDHAPARA; INDIA",
    rocktype="PLU"
    # Fügen Sie bei Bedarf weitere Parameter hinzu
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

#### Grundkonzept

**Syntax**: FIELD=OPERATOR:VALUE

**FIELD**: Ein Feld ist einer der akzeptierten Abfrageparameter. Dies könnte ein beliebiger Parameter sein, wie location1, agemin, rocktype etc.

**OPERATOR**: Ein Operator definiert die Art der Abfrage. Verschiedene Operatoren sind verfügbar:

* "lt" (kleiner als, <)
* "gt" (größer als, >)
* "eq" (gleich, =)
* "in" (innerhalb einer Liste)
* "lk" (ähnlich, LIKE in SQL)
* "btw" (zwischen, BETWEEN in SQL)

**VALUE**: Der Wert, gegen den das Feld verglichen wird. Dies kann eine unzitierte Zeichenkette, eine Ganzzahl oder eine Dezimalzahl sein.

##### Operatoren und ihre Nutzung

"lt" und "gt":
Anwendbar nur auf numerische Werte.
Beispiel: agemin=lt:100 (Alter kleiner als 100)

"eq":
Standardoperator, wenn kein anderer angegeben ist.
Kann für jeden Wertetyp verwendet werden.
Beispiel: rocktype=eq:Basalt (Rocktype gleich Basalt)

"in":
Zum Filtern innerhalb einer Liste von Werten.
Die Werte müssen durch Kommas getrennt sein.
Beispiel: location1=in:USA,Canada,Mexico (Location1 in einer der angegebenen Regionen)

"lk":
Nur für Zeichenketten.
Unterstützt Wildcards * (für beliebig viele Zeichen) und ? (für ein einzelnes Zeichen).
Beispiel: title=lk:Geology* (Titel beginnt mit "Geology")

"btw":
Für numerische Bereiche.
Nimmt zwei durch Kommas getrennte Werte an.
Wenn ein Wert fehlt, wird standardmäßig 0 oder 9999999 angenommen.
Beispiel: agemin=btw:100,200 (Alter zwischen 100 und 200)
Beispiele für die Verwendung

Angenommen, Sie möchten Proben finden, die aus einer bestimmten Region stammen, ein bestimmtes Alter haben und einer 
bestimmten Gesteinsart entsprechen. Sie könnten dann folgende Filter verwenden:

```python
filtered_samples_combined = get_filtered_samples(
    location1="eq:CENTRAL INDIAN TECTONIC ZONE",
    agemin="gt:150",
    rocktype="eq:Granite"
)
```

> **Hinweise**:
> 
> * Die Verwendung mehrerer Filter kann die Abfrage verlangsamen, da mehr Tabellen in der Auswertung berücksichtigt werden müssen.
> 
> 
> * Die Filter werden konjunktiv ausgewertet, d.h., alle Bedingungen müssen erfüllt sein, damit ein Eintrag in das Ergebnis aufgenommen wird.

Additional endpoints and parameters can be used according to the [API documentation](https://api-test.georoc.eu/api/v1/docs/index.html#/).


