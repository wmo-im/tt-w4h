# whos-metadata
A workspace to discuss and implement a strategy to enhance WHOS (WMO Hydrological Observing System) metadata

## Abstract

This directory is intended to host resources concerning [WHOS](https://community.wmo.int/activity-areas/wmo-hydrological-observing-system-whos) (WMO Hydrological Observing System) metadata, with focus in enhancing the metadata records as made available through any of the WHOS-DAB (Data Access Broker [DAB](https://github.com/ESSI-Lab/DAB)) profilers such as [OAI-PMH](https://www.openarchives.org/pmh/).

A set of [KPIs](https://github.com/wmo-im/wmdr/issues/42) (Key Performance Indicators) to assess the quality of metadata records was developed by [TT-WIGOSMD](https://github.com/wmo-im/tt-wigosmd), along with a [software tool](https://github.com/wmo-im/pywmdr) to calculate these for a given set of WIGOS metadata records. These records must be coded according to the WIGOS Metadata Representation ([WMDR](https://github.com/wmo-im/WMDR)) model XML [schema](https://schemas.wmo.int/wmdr/1.0/).

WHOS-DAB is capable of producing WMDR-1.0 records by means of its OAI-PMH profiler. The endpoint for this is https://whos.geodab.eu/gs-service/services/essi/token/<MY_TOKEN>/view/<SELECTED_VIEW>/oaipmh

The general goal would be to achieve better KPI results for the WHOS metadataset.

Specific actions could be divided into:
- Profiling, for example:
  - fine-tuning of the XML schema of the WMDR-1.0 profile (goal: validate against [wmdr.xsd](https://schemas.wmo.int/wmdr/1.0/wmdr.xsd))
- Mapping, for example:
  - mapping of already existing metadata elements from the different data providers into WMDR
- Metadata enriching at the broker, for example:
  - adding metadata elements that are not present in the provider web service but can be deduced somehow
- Metadata enriching at the source, for example:
  - adding or adjusting metadata elements at the data provider web service. Requires interaction with data provider IT staff.

## How to collaborate

Issues should be started for each specific action. 

## How to get WHOS WMDR records

1. Register to WHOS to get a token [here](https://whos.geodab.eu/gs-service/whos/registration.html)
2. Use your favorite client tool to connect to the WHOS-DAB OAI-PMH endpoint: https://whos.geodab.eu/gs-service/services/essi/token/<MY_TOKEN>/view/<SELECTED_VIEW>/oaipmh
3. Set the verb as a request parameter:
 - verb=ListRecords to download whole datasets
 - verb=GetRecord to download a single record. Requires identifier=<IDENTIFIER>
 - verb=ListIdentifiers to download the list of identifiers of the dataset 
4. Additionally, set metadataPrefix=WIGOS-1.0 to get the records in the WMDR-1.0 format
5. Alternatively, download, install and use [pywmdr](https://github.com/wmo-im/pywmdr) with the following sintax:

    `pywmdr harvest [OPTIONS] {identifiers|records|record|parse_files} OUTPUT`

Instructions for download and install can be found in the repo's [README](https://github.com/wmo-im/pywmdr#readme)
## How to evaluate metadata KPIs

1. Get WMDR records as above
2. Evaluate the retrieved files and save the results using pywmdr:

   `pywmdr metrics [OPTIONS] {evaluate|metrics} PATH`

For more help on pywmdr commands, run pywmdr [COMMAND] --help or read the [README](https://github.com/wmo-im/pywmdr#readme)
