# RINF-TWG-CCS
Modelisation of CCS aspects in OP and SoL (as per micro-level ontology).

## Objectives
This repository collects the code samples for the Chapter 4 of the TWG RINF CCS working group final report, strictly based on the [ERA Vocabulary](https://github.com/Interoperable-data/ERA_vocabulary) and [SKOS Concepts](https://data-interop.era.europa.eu/era-vocabulary/skos/index.html), with the updates as per WG 2024.

1. Expressing physical units in RINF, although these will be considered mainly internally at EU AR (as the requirement is present on the general RINF level).
2. Signal & Non-stopping areas, and especially (4.2.3) the types and the modelling on micro-level:
   - Complex station (more than two operational SignalGrids)
   - Simple station (One or two SignalGrids)
   - Section of Line with possibility to manage capacity
4. Areas of implementation (GSM-R)

The examples should demonstrate also how the micro-level (in essence an operational layer) should and can be complemented to the nano-level (in essence the engineering layer, as elaborated by the sector, for instance with the railML ontology). The modelling of the engineering level is however out of scope of the ontologies currently provided by the Agency.

## Contributing
Please fork this repository, add the files in your fork as you see fit and submit a pull request for review by the Agency.

In order to organize these files, please use the naming `<IM-code> - <OP identifier | SoL identifier>.rdf`. The schematic layout plan extract should exactly reuse that name but use the PNG or equivalent file extension.

## Confidentiality
Never publish information on this public repository which would violate the confidentiality rules of your organization in regards to signalling layouts.
