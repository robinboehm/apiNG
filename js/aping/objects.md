## Object Struktur

    {} appConfigObject (1x im scope, parameter von run)
        (gilt pro instanz = aufruf der direktive )
        Beinhaltet folgende Werte:
        {} App Default Settings (module.config)
        {} App Settings (aping.json)
        {} Settings aus den Attributen

        []
            {} requestConfigObject
                (gilt für jeden request)
                Beinhaltet folgende Werte:
                {} Plattform Default Settings (module.config)
                {} Definition Settings (json file)
                {} Settings aus dem betreffenden Attribut //z.b. {'user':'yyz','items':'5'}
                {} API spezifische Eigenschaften, die der Aufruf selbst hinzufügt
                    - (nextPageToken, ...)


    {} appResultObject (return von run)
        {} appConfigObject

        []
            {} platformObject (1x pro plattform)
                []
                    {} requestObject (1x pro request)
                        {} requestErrorObject
                        {} requestInfoObject
                        []
                            {} outputObject (zB. socialObject)


## scope
    {} appConfig (appConfigObject)
    {} appErrors (appErrorObject)
    [] results (Feed)
    [] platforms
        [] requests
            {} errors
            {} infos


## Objecte

**baseObjects**
* appConfigObject
* appErrorObject
* platformObject
* platformErrorObject
* requestConfigObject
* requestErrorObject (enthält Errormeldungen)
* requestInfoObject


**outputObjects**
* channelObject (Channel ist gleichbedeutend mit User, Page oder Kanal)
* socialObject (jeglicher Social Media Content)
* videoObject
* pictureObject
* audioObject
* eventObject
* ...

---

**Pro Object** gibt es **einen Service**, der folgendes liefert
* fn() liefert ein BlankoObject, das nur die notwendigsten Parameter hat
* fn()s liefern bestimmte Werte für das jeweilige Setting

---

**Pro Plattform** gibt es immer **eine Factory** und **einen Service**:
* Die FACTORY besorgt den API-Call und liefert die JSON-Daten zurück.
* Der SERVICE füllt die JSON-Daten in die entsprechenden Objekte um. Hierbei soll es immer eine Funktion geben, die einen kompletten Aufruf bearbeitet in dem sie jeweils pro Item eine eigene Funktion aufruft, in welcher die eigentliche Parse-Arbeit passiert

---

### Run Methode

FOLGENDER ABSCHNITT IST AUF TODO

Beim ersten Run werden alle Configs geparsed und in AppConfig und in die Liste der RequestConfigs geschrieben.

Nach dem Parsen wird durch die RequestConfigs durchgeloopt und durchgearbeitet
Diese Funktionen erweitern die RequestConfigs um neue Parameter/Werte.

Wenn die run Funktion nun neu aufgerufen wird, dann werden die Einträge nicht mehr geparsed sondern nur die
bestehenden RequestConfigs durchgeloopt