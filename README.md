# Repository for roadsafety projects

* Script for processing data (read: Handleiding product Bestand geRegistreerde Ongevallen Nederland)
* Example PowerBI (very basic and under construction)
* OpenStreetmap:
  * mapping road accidents on neighborhood to finding safe routes to school.
  * working on an algorithm for automatic routing (python osmnx).
  * accesibility for blind and disabled (tactile_paving)
  * reading: Route planning for blind pedestrians using OpenStreetMap ([document link](https://journals.sagepub.com/doi/full/10.1177/2399808320933907)

# Inzicht in de verkeersveiligheid op buurt en straat nivo

## Doel van dit systeem

Informatie over verkeersongevallen beschikbaar stellen aan burgers zodat deze geinformeerd worden over de verkeersveiligheidsituatie in hun omgeving. Bewoners en andere geintresseerden kunnen met dit hulpmiddel de situatie op gemeente en buurt nivo onderzoeken.

* Is mijn wijk veiliger of onveiliger dan andere wijken
* Waar komen vaak ongevallen voor en wie zijn daar bij betrokken
* Welke maatregelen zijn er getroffen om de veiligheid te verhogen?
* Is er een veilige route naar mijn werk en de school te vinden?

Toon een kaart van nederland met de actuele gemeente en buurt indeling, plaatsen waar ongevallen hebben plaastgevonden en de door de gemeente of provincie genomen verkeersmaatregelen.

[Verkeersongevallen - Bestand geRegistreerde Ongevallen Nederland](https://data.overheid.nl/en/dataset/9841-verkeersongevallen---bestand-geregistreerde-ongevallen-nederland)

*Het bestand geRegistreerde Ongevallen Nederland is een bestand met de ongevallenmeldingen van de politie gekoppeld aan het digitale wegennet (het Nationale Wegenbestand, NWB). Met dit product kunt u verschillende verkeersveiligheidsanalyses voor uw beheersgebied uitvoeren en is in het bijzonder geschikt voor: - beleid (formuleren, monitoren, evalueren), - onderzoek en - wegbeheer.*

## Aantallen
```
  17M mensen
   2M ongevallen periode 2003-2020
13808 buurten 
 3177 wijken
  355 gemeentes
   12 provincies
    1 nederland (vroeger hadden we nog nederland 2)
```

## Data bewerking:

Gebruik de [google colab](https://colab.research.google.com/) python runtime omgeving

* Laad geregistreerde ongevallen [Verkeersongevallen - Bestand geRegistreerde Ongevallen Nederland](https://data.overheid.nl/en/dataset/9841-verkeersongevallen---bestand-geregistreerde-ongevallen-nederland)
* Laad tabel Provincie / Gemeente / Wijk / Buurt (geografische grenzen en aantal inwoners)
  * PDOK Wijk- en Buurtkaart 2020 versie 1
  * https://geodata.nationaalgeoregister.nl/wijkenbuurten2020/wms?request=GetCapabilities
  * Leid de hierarchie af uit de codering
  * We hebben nog geen provincies in onze hierarchie
* Bepaal voor elk ongeval in welke gemeente / wijk / buurt deze plaatsvond op basis van de actuele gemeentelijke indeling
  * Let op oudere ongevallen zijn soms in niet meer bestaande gemeenten geregistreerd dus moeten we ze herindelen tegen de nu geldende situatie
  * Map ongelukken op basis van de buurt grenzen
  * Probleem ongeveer 680 ongevallen vallen net buiten alle grenzen
  * Wellicht moeten we een tabel met gemeentelijke herindeling maken

Kaart projecties:
* Rijksdriehoekstelsel EPSG:28992
* GPS: WGS84

## TO-DO:
* Opschonen en verrijken data:
 * MAXSNELHD (soms groter dan 130 km, soms 100km in woonwijk)
 * Wegsoort (snelweg, deze willen we niet meetellen in een wijk)
 * Binnen / buiten de bebouwde kom (is deze data nodig, grens bebouwde kom is moeilijk te bepalen)
 * Bepaal de maximale snelheid op de weg [WEGGEG](https://data.overheid.nl/en/dataset/bb5bbc65-2a1a-49e4-a9e8-417ae3920703)
 * Laad tabel NWB wegen - Wegvakken (RWS) [documentatie](https://data.overheid.nl/en/dataset/9b50f8a3-7c67-4efb-9046-fb7a57eca18c) [download link](https://geo.rijkswaterstaat.nl/services/ogc/gdr/nwb_wegen/ows?service=WFS&version=2.0.0&request=GetFeature&typeName=wegvakken&outputFormat=csv)
 
