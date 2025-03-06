---
title: "MBON Workshop Test"
start: true
teaching: 0
exercises: 90
---

:::::::::::: questions

- What are the required fields to publish to OBIS?
- What are the recommended fields?
- What do I need to know to share certain ocean observing method data in Darwin Core?
- How do I publish my data when it is ready?

:::::::::::::::::::::::

::::::::::: objectives

- Enabling access to the OBIS-USA IPT so data providers can enter their metadata.
- Understand required Darwin Core terms for Occurrence, Event, and extensions.
- Understand other recommended data that can be included in these files and how to create the files.

::::::::::::::::::::::

## Darwin Core
[Darwin Core](https://www.tdwg.org/standards/dwc/) (DwC) is an international standard maintained by the Biodiversity Information Standards (or [TDWG](https://www.tdwg.org/)) association. Darwin Core consists of a glossary of terms that facilitate the sharing of information about biological occurrences as documented by observations, specimens, samples, and other evidence. To see a full list of Darwin Core terms, please see the [Quick Reference Guide](https://dwc.tdwg.org/terms/). To learn more about the foundations of Darwin Core, read 
[Wieczorek et al., 2012](https://doi.org/10.1371/journal.pone.0029715).

Observations of marine life can be translated into Darwin Core and shared regardless of the observing method. At the end of the day, biological occurrences are data about an organism at a time in a place. That is the essence of what we want to capture with Darwin Core. Any additional information you can provide on top of that (environmental variables at the time of the observation, data about how the occurrence was determined, etc.) is icing on the cake.

#### Demonstrated Use of Darwin Core
As members of the ocean observing community, it is important for us to share our data in the Darwin Core format so it can be easily aggregated and analyzed with other biological occurrences that have been published to databases like the [Ocean Biodiversity Information System](https://obis.org/) (OBIS; containing over 136 million records at the time of this workshop) and the [Global Biodiversity Information Facility](https://www.gbif.org/) (GBIF; containing over 3 billion records at the time of this workshop). By adding our data to these systems, we can enhance what is known about marine life in U.S. waters and globally, and help fill data gaps where other observations may not exist.

#### Darwin Core Archives
A Darwin Core Archive is a zipped folder containing Darwin Core-formatted data (one or several files depending on how many extensions you use), an Ecological Metadata Language (EML) XML file, and a meta.xml file that describes what's in the zipped folder. Darwin Core Archives are what OBIS and GBIF harvest into their systems. Fortunately, the software created and maintained by GBIF, the [Integrated Publishing Toolkit](https://www.gbif.org/ipt) (IPT), produces Darwin Core Archives for us. We will be learning more about the IPT in the [next section](#obis-usa-ipt-introduction). 

::::::::::::::::::::::::::::::::::::: challenge

### Challenge

Download this [Darwin Core Archive](https://ipt-obis.gbif.us/archive.do?r=tpwd_harc_texasaransasbay_bagseine&v=2.3) and 
examine what's in it. Did you find anything unusual or that you don't understand what it is?

:::::::::::::::::::::::: solution 

### Solution

```Folder
dwca-tpwd_harc_texasaransasbay_bagseine-v2.3
 |-- eml.xml
 |-- event.txt
 |-- extendedmeasurementorfact.txt
 |-- meta.xml
 `-- occurrence.txt
```
::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::

::::::::::::: keypoints

- Biological occurrences can be shared to Darwin Core no matter what observing or sampling method was used.
- The essence of the information we want to capture in Darwin Core is **what** organism was observed, **when**, and **where**.
- To see a full list of Darwin Core terms, see the [Quick Reference Guide](https://dwc.tdwg.org/terms/).

:::::::::::::::::::::::

## OBIS-USA IPT Introduction

## Occurrence Core
Now that we have a firm basis for understanding the different terms in Darwin Core the next part to understand is how data tables are organized and the difference between cores and extensions. You will always have a core table (Occurrence core or Event core) with either no extensions or several. What you choose depends on the data you have and how to represent it best. 

The original Darwin Core core is the Occurrence Core. Once people started using that core they began to see that they needed extensions to that core to best represent the data they were trying to share and therefore several extensions have been developed (and are continuing to be developed). As more monitoring data has been shared over time, another core type called Event Core was added. Without getting too far into the weeds on the cores and extensions, what’s most important to understand is that you need to pick your core type and once you do that then you pick the extensions to go with it. For example, if your data took place as part of an event (cruise, transects, etc) you will pick Event Core. If there was no sampling event, then you will pick Occurrence Core.

When you are doing your mappings to Darwin Core, what terms are required? What other terms might be useful to include? You can find the full list of Darwin Core Occurrence terms on the [Quick Reference Guide](https://dwc.tdwg.org/terms/#occurrence).

:::::::::::: spoiler

## What terms are required in Occurrence Core?

| Darwin Core Term | Role | Definition | Comment | Example |
|------------------|-----------|-------------------------------------------|---------------------------------------|-----------------|
| [`occurrenceID`](https://dwc.tdwg.org/terms/#dwc:occurrenceID) | **required** | An identifier for the Occurrence (as opposed to a particular digital record of the occurrence). In the absence of a persistent global unique identifier, construct one from a combination of identifiers in the record that will most closely make the occurrenceID globally unique. | To construct a globally unique identifier for each occurrence you can usually concatenate station + date + scientific name (or something similar) but you'll need to check this is unique for each row in your data. It is preferred to use the fields that are least likely to change in the future for this. For ways to check the uniqueness of your occurrenceIDs see the [QA / QC]({{ page.root }}/06-qa-qc/index.html) section of the workshop. | Station_95_Date_09JAN1997:14:35:00.000_Atractosteus_spatula |
| [`basisOfRecord`](https://dwc.tdwg.org/terms/#dwc:basisOfRecord) | **required** | The specific nature of the data record.  | Pick from these controlled vocabulary terms: [HumanObservation](http://rs.tdwg.org/dwc/terms/HumanObservation), [MachineObservation](http://rs.tdwg.org/dwc/terms/MachineObservation), [MaterialSample](http://rs.tdwg.org/dwc/terms/MaterialSample), [PreservedSpecimen](http://rs.tdwg.org/dwc/terms/PreservedSpecimen), [LivingSpecimen](http://rs.tdwg.org/dwc/terms/LivingSpecimen), [FossilSpecimen](http://rs.tdwg.org/dwc/terms/FossilSpecimen), [MaterialEntity](http://rs.tdwg.org/dwc/terms/MaterialEntity), [Event](http://rs.tdwg.org/dwc/terms/Event), [Taxon](http://rs.tdwg.org/dwc/terms/Taxon), [Occurrence](http://rs.tdwg.org/dwc/terms/Occurrence), [MaterialCitation](http://rs.tdwg.org/dwc/terms/MaterialCitation) | HumanObservation |
| [`scientificName`](https://dwc.tdwg.org/terms/#dwc:scientificName) | **required** | The full scientific name, with authorship and date information if known. When forming part of an Identification, this should be the name in lowest level taxonomic rank that can be determined. This term should not contain identification qualifications, which should instead be supplied in the `identificationQualifier` term. | Note that cf., aff., etc. need to be parsed out to the `identificationQualifier` term. For a more thorough review of `identificationQualifier` see [this paper](https://doi.org/10.3389/fmars.2021.620702). | Atractosteus spatula |
| [`scientificNameID`](https://dwc.tdwg.org/terms/#dwc:scientificNameID) | **required** | An identifier for the nomenclatural (not taxonomic) details of a scientific name. | Must be a WoRMS LSID for sharing to OBIS. Note that the numbers at the end are the AphiaID from WoRMS. | urn:lsid:marinespecies.org:taxname:218214 |
| [`occurrenceStatus`](https://dwc.tdwg.org/terms/#dwc:occurrenceStatus) | **required** | A statement about the presence or absence of a Taxon at a Location. | For OBIS, only valid values are `present` and `absent`. | present |
| [`kingdom`](https://dwc.tdwg.org/terms/#dwc:kingdom) | **required** | The full scientific name of the kingdom in which the taxon is classified.| Not required for OBIS but GBIF needs this to disambiguate scientific names that are the same but in different kingdoms. | Animalia |

::::::::::::::::::::

## Event Core
As we have indicated earlier, the Event core is for datasets that include known sampling events - details are known 
about how, when, and where samples were taken.

An innovation that OBIS made was introducing the Extended Measurement or Fact extension (also sometimes referred to as 
OBIS-ENV-DATA, or eMoF). This uses the Event core with an Occurrence extension + the 
[extended Measurement or Fact extension](https://rs.gbif.org/extension/obis/extended_measurement_or_fact.xml). The eMoF 
extension makes it possible to include measurements for **both** the events (salinity, temperature, gear type, etc.) and 
the occurrences (weight, length, etc.). Prior to this you were only able to include measurements of the occurrence (in 
the Measurement or Facts extension).

It is important to know that the structure of the eMoF table is likely quite a bit different than how the original data 
are recorded in your dataset. Rather than documenting each measurement in separate columns, measurements will be 
condensed into one column: `measurementValue` (e.g. 15). Then, the column `measurementType`  allows free text 
describing what the measurement actually is (e.g. length). Finally the column `measurementUnit` is used to indicate the 
unit of the measurement (e.g. cm).

The unconstrained nature of `measurementType` allows for flexibility in describing measurements, which can be quite a 
useful. But what if you wanted to obtain all OBIS records that have "length" measurements? Due to the inevitable 
heterogeneity in how different people document "length", you would have to try to account for all these different ways! 
Fortunately the eMoF table can get around this challenge by providing a way to include Unique Resource Identifiers 
(URIs). These URIs are used to populate the `measurementTypeID` field, as well as `measurementUnitID` and 
`measurementValueID`. URIs mean that if you call the `measurementType` "abundance" but I call it "Abundance per square 
meter" and we both use the `measurementTypeID` "http://vocab.nerc.ac.uk/collection/P01/current/SDBIOL02/" then we know 
this is the same measurement type even if we didn't use the same words to describe it. Choosing the right URI can be 
difficult but you can read about finding codes in 
[the OBIS Manual](https://manual.obis.org/vocabulary.html#map-emof-measurement-identifiers-to-preferred-bodc-vocabulary). 
All you need to know for now is that `measurementTypeID` should be populated with a URI belonging to the NERC P01 
collection, easily accessible through the [SeaDataNet P01 facet search](https://vocab.seadatanet.org/p01-facet-search), 
and `measurementUnitID` should be popualted with a 
[NERC P06 code](https://vocab.nerc.ac.uk/search_nvs/P06/?searchstr=&options=identifier,preflabel,altlabel,status_accepted&rbaddfilter=inc&searchstr2=). 
OBIS is soon releasing video tutorials to help with choosing URIs, so stay tuned to their [manual](https://manual.obis.org/) 
and [YouTube list](https://www.youtube.com/@oceanbiodiversityinformati6931/playlists) for updates.

:::::::::::: spoiler

## What terms are required in Event core?

| Darwin Core Term | Role | Definition | Comment | Example |
|------------------|-----------|-------------------------------------------|---------------------------------------|-----------------|
| [eventID](https://dwc.tdwg.org/terms/#dwc:eventID) | **required** | An identifier for the set of information associated with an Event (something that occurs at a place and time). May be a global unique identifier or an identifier specific to the data set. | `INBO:VIS:Ev:00009375`<br/>`Station_95_Date_09JAN1997:14:35:00.000` <br/> `FFS-216:2007-09-21:A:replicateID1024`|
| [`eventDate`](https://dwc.tdwg.org/terms/#dwc:eventDate) | **required** | The date-time or interval during which an Event occurred. For occurrences, this is the date-time when the event was recorded. Not suitable for a time in a geological context. | Must follow [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601). See more information on dates in the [Data Cleaning]({{ page.root }}/03-data-cleaning/index.html) section of the workshop. | 2009-02-20T08:40Z |
| [`decimalLatitude`](https://dwc.tdwg.org/terms/#dwc:decimalLatitude) | **required** | The geographic latitude (in decimal degrees, using the spatial reference system given in geodeticDatum) of the geographic center of a Location. Positive values are north of the Equator, negative values are south of it. Legal values lie between -90 and 90, inclusive. | For OBIS and GBIF the required `geodeticDatum` is WGS84. Uncertainty around the geographic center of a Location (e.g. when sampling event was a transect) can be recorded in `coordinateUncertaintyInMeters`. See more information on coordinates in the [Data Cleaning]({{ page.root }}/03-data-cleaning/index.html) section of the workshop. | -41.0983423 |
| [`decimalLongitude`](https://dwc.tdwg.org/terms/#dwc:decimalLongitude) | **required** | The geographic longitude (in decimal degrees, using the spatial reference system given in geodeticDatum) of the geographic center of a Location. Positive values are east of the Greenwich Meridian, negative values are west of it. Legal values lie between -180 and 180, inclusive | For OBIS and GBIF the required `geodeticDatum` is WGS84. See more information on coordinates in the [Data Cleaning]({{ page.root }}/03-data-cleaning/index.html) section of the workshop. | -121.1761111 |
| [`countryCode`](https://dwc.tdwg.org/terms/#dwc:countryCode) | **required** | The standard code for the country in which the location occurs. | Use an [ISO 3166-1-alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) country code. Not required for OBIS but GBIF prefers to have this for their system. For international waters, leave blank. | US, MX, CA |
| [`geodeticDatum`](https://dwc.tdwg.org/terms/#dwciri:geodeticDatum) | **required** | The ellipsoid, geodetic datum, or spatial reference system (SRS) upon which the geographic coordinates given in decimalLatitude and decimalLongitude as based. | Must be [WGS84](https://epsg.io/4326) for data shared to OBIS and GBIF but it's best to state explicitly that it is. | WGS84 |

::::::::::::::::::::

## Extensions

### Extended Measurement or Fact Extension (eMoF)
As we have indicated earlier, the Event core is for datasets that include known sampling events - details are known 
about how, when, and where samples were taken.

An innovation that OBIS made was introducing the Extended Measurement or Fact extension (also sometimes referred to as 
OBIS-ENV-DATA, or eMoF). This uses the Event core with an Occurrence extension + the 
[extended Measurement or Fact extension](https://rs.gbif.org/extension/obis/extended_measurement_or_fact.xml). The eMoF 
extension makes it possible to include measurements for **both** the events (salinity, temperature, gear type, etc.) and 
the occurrences (weight, length, etc.). Prior to this you were only able to include measurements of the occurrence (in 
the Measurement or Facts extension).

It is important to know that the structure of the eMoF table is likely quite a bit different than how the original data 
are recorded in your dataset. Rather than documenting each measurement in separate columns, measurements will be 
condensed into one column: `measurementValue` (e.g. 15). Then, the column `measurementType`  allows free text 
describing what the measurement actually is (e.g. length). Finally the column `measurementUnit` is used to indicate the 
unit of the measurement (e.g. cm).

The unconstrained nature of `measurementType` allows for flexibility in describing measurements, which can be quite a 
useful. But what if you wanted to obtain all OBIS records that have "length" measurements? Due to the inevitable 
heterogeneity in how different people document "length", you would have to try to account for all these different ways! 
Fortunately the eMoF table can get around this challenge by providing a way to include Unique Resource Identifiers 
(URIs). These URIs are used to populate the `measurementTypeID` field, as well as `measurementUnitID` and 
`measurementValueID`. URIs mean that if you call the `measurementType` "abundance" but I call it "Abundance per square 
meter" and we both use the `measurementTypeID` "http://vocab.nerc.ac.uk/collection/P01/current/SDBIOL02/" then we know 
this is the same measurement type even if we didn't use the same words to describe it. Choosing the right URI can be 
difficult but you can read about finding codes in 
[the OBIS Manual](https://manual.obis.org/vocabulary.html#map-emof-measurement-identifiers-to-preferred-bodc-vocabulary). 
All you need to know for now is that `measurementTypeID` should be populated with a URI belonging to the NERC P01 
collection, easily accessible through the [SeaDataNet P01 facet search](https://vocab.seadatanet.org/p01-facet-search), 
and `measurementUnitID` should be popualted with a 
[NERC P06 code](https://vocab.nerc.ac.uk/search_nvs/P06/?searchstr=&options=identifier,preflabel,altlabel,status_accepted&rbaddfilter=inc&searchstr2=). 
OBIS is soon releasing video tutorials to help with choosing URIs, so stay tuned to their [manual](https://manual.obis.org/) 
and [YouTube list](https://www.youtube.com/@oceanbiodiversityinformati6931/playlists) for updates.

:::::::::::: callout

## :pushpin: Tip 

You can search for `measurementTypes` that other OBIS data providers have used by using the 
[OBIS mof report](https://mof.obis.org/). BE CAREFUL though to make sure the
definition in the URI matches exactly your measurement type if you want to reuse it for your data.

::::::::::::::::::::

:::::::::::: spoiler

## Extended Measurement or Fact Extension Terms

Nothing is *required* from the OBIS perspective but if you are using this extension then `eventID` is required to be 
able to link the extension back to the Event core. You can also use `occurrenceID` to link to occurrence records in 
the Occurrence core or extension. See [here](https://rs.gbif.org/extension/obis/extended_measurement_or_fact.xml) for 
all potential fields in the extension and what goes in them. See below of the most relevant terms to be included in the 
eMoF table.
 
| Darwin Core Term | Definition | Comment | Example |
|------------------|------------------------------------|---------------------------------------|-----------------|
| `eventID` | An identifier for the set of information associated with an Event (something that occurs at a place and time). May be a global unique identifier or an identifier specific to the data set.| This will be constructed in the Event core but you need to reference it here in the extension so the files can link to each other correctly. | `INBO:VIS:Ev:00009375`<br/>`Station_95_Date_09JAN1997:14:35:00.000` <br/> `FFS-216:2007-09-21:A:replicateID1024`|
| `occurrenceID` | The identifier of the occurrence the measurement or fact refers to. If not applicable, it should be left empty. | Only needed if you have measurements that you need to link back to an occurrence like weight, length, abundance, etc. | `urn:catalog:UWBM:Bird:89776` <br/> `Station_95_Date_09JAN1997:14:35:00.000_Atractosteus_spatula` <br/> `FFS-216:2007-09-21:A:replicateID1024:objectID1345330` |
| `measurementID` | An identifier for the MeasurementOrFact (information pertaining to measurements, facts, characteristics, or assertions). May be a global unique identifier or an identifier specific to the data set. | This is not necessarily required when creating the eMoF but it can be useful, especially if you would like a way to identify a specific measurement in the data | `9c752d22-b09a-11e8-96f8-529269fb1459` |
| `measurementType` | The nature of the measurement, fact, characteristic, or assertion. Recommended best practice is to use a controlled vocabulary. |  | `temperature`<br/> `salinity`<br/> `length`<br/> `device type`|
| `measurementTypeID` | An identifier for the measurementType (global unique identifier, URI). The identifier should reference the measurementType in a vocabulary. | OBIS uses NERC to provide these but you can use other vocabularies or ontologies like ENVO or others. When using NERC vocabulary terms, you must choose a term from the P01 collection. | `http://vocab.nerc.ac.uk/collection/P01/current/TEMPPR01/` <br/> `http://vocab.nerc.ac.uk/collection/P01/current/ODSDM021/	` <br/> `http://vocab.nerc.ac.uk/collection/P01/current/OBSINDLX/` <br/> |
| `measurementValue` | The value of the measurement, fact, characteristic, or assertion |  | `20`<br/> `61.5`<br/> `121`<br/> `Van Veen grab` |
| `measurementValueID` | An identifier for facts stored in the column measurementValue (global unique identifier, URI). This identifier can reference a controlled vocabulary (e.g. for sampling instrument names, methodologies, life stages) or reference a methodology paper with a DOI. When the measurementValue refers to a value and not to a fact, the **measurementvalueID has no meaning and should remain empty**. |  | `http://vocab.nerc.ac.uk/collection/L22/current/TOOL0653/`|
| `measurementAccuracy` | The description of the potential error associated with the measurementValue. |  | `0.01 C`<br/>`0.03` <br/>`5 mm`|
| `measurementUnit` | The units associated with the measurementValue. Recommended best practice is to use the International System of Units (SI). |  | `C`<br/> `PPT`<br/> `mm` |
| `measurementUnitID` | An identifier for the measurementUnit (global unique identifier, URI). The identifier should reference the measurementUnit in a vocabulary. | Recommended practice is populate this field with a term from NERC vocablary's P06 collection | `http://vocab.nerc.ac.uk/collection/P06/current/UPAA/`<br/>`http://vocab.nerc.ac.uk/collection/P06/current/UPPT/` <br/>`http://vocab.nerc.ac.uk/collection/P06/current/UXMM/` |

::::::::::::::::::::

In the [IOOS Bio Data Guide repository](https://github.com/ioos/bio_data_guide), you can see [a script](https://github.com/ioos/bio_data_guide/blob/main/datasets/TPWD_HARC_BagSeine/TPWD_HARC_BagSeine_OBISENV.md) used to take data in its original form and align it to Darwin Core Event Core with Extended Measurement or Fact. More information on how to organize data fields into Event and Measurement or Fact can be found in the [OBIS Manual](https://manual.obis.org/).

## Observation Method-Specific Recommendations

### Environmental DNA (eDNA)
#### Key Points


#### Resources
* For more detailed information about the DNA-derived Data Extension, see [here](https://ioos.github.io/mbon_data_workshop_2025/edna-extension.html).
* For more about eDNA metadata, check out the [FAIR eDNA project](https://fair-edna.github.io/index.html).

### Passive Acoustic Monitoring (PAM)
#### Key Points


#### Resources
* To see how the SanctSound project processes their PAM data and distills it into DwC, see [here](https://github.com/ioos/bio_data_guide/blob/main/datasets/SanctSound/README.md).

### Plankton Imagery
#### Key Points


#### Resources
*
*
*

### Animal Telemetry
#### Key Points


#### Resources
* For more detailed information about how to translate acoustic and satellite telemetry into DwC, see [here](https://ioos.github.io/mbon_data_workshop_2025/acoustic-telemetry.html).
