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

## OBIS-USA IPT Introduction

## Occurrence Core
When you are doing your mappings to Darwin Core, what terms are required? Right now we will focus on those required in the Occurrence core.

| Darwin Core Term | Role | Definition | Comment | Example |
|------------------|-----------|-------------------------------------------|---------------------------------------|-----------------|
| [`occurrenceID`](https://dwc.tdwg.org/terms/#dwc:occurrenceID) | **required** | An identifier for the Occurrence (as opposed to a particular digital record of the occurrence). In the absence of a persistent global unique identifier, construct one from a combination of identifiers in the record that will most closely make the occurrenceID globally unique. | To construct a globally unique identifier for each occurrence you can usually concatenate station + date + scientific name (or something similar) but you'll need to check this is unique for each row in your data. It is preferred to use the fields that are least likely to change in the future for this. For ways to check the uniqueness of your occurrenceIDs see the [QA / QC]({{ page.root }}/06-qa-qc/index.html) section of the workshop. | Station_95_Date_09JAN1997:14:35:00.000_Atractosteus_spatula |
| [`basisOfRecord`](https://dwc.tdwg.org/terms/#dwc:basisOfRecord) | **required** | The specific nature of the data record.  | Pick from these controlled vocabulary terms: [HumanObservation](http://rs.tdwg.org/dwc/terms/HumanObservation), [MachineObservation](http://rs.tdwg.org/dwc/terms/MachineObservation), [MaterialSample](http://rs.tdwg.org/dwc/terms/MaterialSample), [PreservedSpecimen](http://rs.tdwg.org/dwc/terms/PreservedSpecimen), [LivingSpecimen](http://rs.tdwg.org/dwc/terms/LivingSpecimen), [FossilSpecimen](http://rs.tdwg.org/dwc/terms/FossilSpecimen), [MaterialEntity](http://rs.tdwg.org/dwc/terms/MaterialEntity), [Event](http://rs.tdwg.org/dwc/terms/Event), [Taxon](http://rs.tdwg.org/dwc/terms/Taxon), [Occurrence](http://rs.tdwg.org/dwc/terms/Occurrence), [MaterialCitation](http://rs.tdwg.org/dwc/terms/MaterialCitation) | HumanObservation |
| [`scientificName`](https://dwc.tdwg.org/terms/#dwc:scientificName) | **required** | The full scientific name, with authorship and date information if known. When forming part of an Identification, this should be the name in lowest level taxonomic rank that can be determined. This term should not contain identification qualifications, which should instead be supplied in the `identificationQualifier` term. | Note that cf., aff., etc. need to be parsed out to the `identificationQualifier` term. For a more thorough review of `identificationQualifier` see [this paper](https://doi.org/10.3389/fmars.2021.620702). | Atractosteus spatula |
| [`scientificNameID`](https://dwc.tdwg.org/terms/#dwc:scientificNameID) | **required** | An identifier for the nomenclatural (not taxonomic) details of a scientific name. | Must be a WoRMS LSID for sharing to OBIS. Note that the numbers at the end are the AphiaID from WoRMS. | urn:lsid:marinespecies.org:taxname:218214 |
| [`occurrenceStatus`](https://dwc.tdwg.org/terms/#dwc:occurrenceStatus) | **required** | A statement about the presence or absence of a Taxon at a Location. | For OBIS, only valid values are `present` and `absent`. | present |
| [`kingdom`](https://dwc.tdwg.org/terms/#dwc:kingdom) | **required** | The full scientific name of the kingdom in which the taxon is classified.| Not required for OBIS but GBIF needs this to disambiguate scientific names that are the same but in different kingdoms. | Animalia |

## Event Core
What terms are required in Event core?

:::::::::::: spoiler

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
Nothing is required from the OBIS perspective but if you are using the Extended Measurement or Fact extension other than eventID, which is required to link the extension back to the Event core. You can also use occurrenceID to link to occurrence records in the Occurrence core or extension. See here for all potential fields in the extension and what goes in them. See below of the most relevant terms to be included in the eMoF table.

## Observation Method-Specific Recommendations

### Environmental DNA (eDNA)

### Passive Acoustic Monitoring

### Plankton Imagery

### Animal Telemetry
