# Module
## Common fields
_Fields common to all schemas in this document_

Property name | Description | Type | Required? | Example 
--- | --- | --- | --- | ---
 describedBy | The URL reference to the schema. | string | no |  |  |  | 
schema_version | The version number of the schema in major.minor.patch format. | string | no | 4.6.1

## Channel<a name='Channel'></a>
_Information about a single microscope channel._

Location: module/protocol/channel.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
channel_id | User given ID.  If there is an accompanying codebook, this name should correspond to the channel id used in the codebook. | string | yes |  | Channel ID |  | 1; A
excitation_wavelength | Excitation wavelength of the lightsource in nanometers. | number | yes |  | Excitation wavelength |  | 640
filter_range | Emission filter in nanometers. | string | yes |  | Filter range |  | 461/70
multiplexed | Whether multiple targets were detected simultaneously in this channel. | string | yes |  | Multiplexed experiment | yes, no | Should be one of: yes, or no.
target_fluorophore | The name of the fluorophore this channel is designed to assay. | string | no |  | Target fluorophore |  | Alexa 647
exposure_time | Acquisition time for a single image per channel, in milliseconds. | number | yes |  | Exposure time |  | 400

## Probe<a name='Probe'></a>
_Information about probes used to detect targets._

Location: module/protocol/probe.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
probe_label | The label of a probe used to detect target in this experiment. | string | yes |  | Probe label |  | ACTA1; cFos
probe_sequence | Sequence of a probe used to detect target. | string | no |  | Probe sequence |  | AGGCTATAGCGGAGCTACG; aggctatagcggagctacg
target_name | The name of the target molecule. | string | no |  | Target name |  | ACTA1_exon1; nuclear cFos
target_codebook_label | A label used in the codebook for the target. | string | no |  | Target label in codebook |  | AKT1; CFOS
target_label | An identifier for the target molecule. | string | yes |  | Target label |  | CHEBI:85345; ENSG00000170345
subcellular_structure | Target subcellular structure. | object | no | [See module  cellular_component_ontology](module.md/#cellular_component_ontology) | Target subcellular structure |  | 
probe_reagents | Name of reagents used to construct the probe. | object | no | [See module  purchased_reagents](module.md/#purchased_reagents) | Probe construction reagents |  | 
assay_type | Type of assay used to detect target. | object | yes | [See module  process_type_ontology](module.md/#process_type_ontology) | Assay type |  | MERFISH; in situ sequencing
fluorophore | Fluorophore used to detect target. | array | no |  | Fluorophore |  | Cy5; Alexa 488
channel_label | Channel label used to assay signal. | array | no |  | Channel |  | 1; A

## Matrix<a name='Matrix'></a>
_Information relating to generation of matrices_

Location: module/protocol/matrix.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
data_normalization_methods | Method(s) used to normalize data in the matrix | array | no |  | Data normalization method(s) | CPM (counts per million), TPM (transcripts per kilobase million), RPKM (reads per kilobase of exon per million reads mapped), FPKM (fragments per kilobase of exon per million fragments mapped), DESeq2’s median of ratios, TMM (EdgeR’s trimmed mean of M values), SF (size factor), UQ (Upper quartile), Downsampling, other, unknown | 
derivation_process | Type of computational tool used in generating the matrix object. | array | no |  | Derivation process | alignment, quantification, peak calling, peak annotation, gene filtering, cell filtering, merging, cell calling, ambient RNA correction, doublet removal, batch correction, depth normalization, other | 

## File content ontology<a name='File content ontology'></a>
_A term that describes the contents of a file._

Location: module/ontology/file_content_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | General description of the contents of the file. | string | yes |  | Content description |  | DNA sequence (raw); Sequence alignment
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Content description ontology ID |  | data:3497; data:0863
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Content description ontology label |  | DNA sequence (raw); Sequence alignment

## Length unit ontology<a name='Length unit ontology'></a>
_A term that may be associated with a cell type-related ontology term._

Location: module/ontology/length_unit_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a length unit being used. | string | yes |  | Length unit |  | micrometer; meter
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Length unit ontology ID |  | UO:0000017; UO:0000008
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Length unit ontology label |  | micrometer; meter

## Cell cycle ontology<a name='Cell cycle ontology'></a>
_A term that may be associated with a cell cycle-related ontology term._

Location: module/ontology/cell_cycle_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a cell cycle of the cells in the specimen. | string | yes |  | Cell cycle |  | meiotic cell cycle; mitotic G1 phase
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Cell cycle ontology ID |  | GO:0051321; GO:0000080
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Cell cycle ontology label |  | meiotic cell cycle; mitotic G1 phase

## Library amplification ontology<a name='Library amplification ontology'></a>
_A term that may be associated with a process-related ontology term._

Location: module/ontology/library_amplification_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a library amplification approach being used. | string | yes |  | Library amplification |  | PCR; in vitro transcription
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Library amplification ontology ID |  | OBI:0000415; EFO:0009013
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Library amplification ontology label |  | PCR; in vitro transcription

## Contributor role ontology<a name='Contributor role ontology'></a>
_A term that describes the role of a contributor in the project._

Location: module/ontology/contributor_role_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The primary role of the contributor in the project. | string | yes |  | Contributor role |  | principal investigator; experimental scientist
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Contributor role ontology ID |  | EFO:0009736; EFO:0009741
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Contributor role ontology label |  | principal investigator; experimental scientist

## Ethnicity ontology<a name='Ethnicity ontology'></a>
_A term that may be associated with a ethnicity-related ontology term._

Location: module/ontology/ethnicity_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The ethnicity of the human donor. | string | yes |  | Ethnicity |  | European; Hispanic or Latin American
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Ethnicity ontology ID |  | HANCESTRO:0005; HANCESTRO:0014
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Ethnicity ontology label |  | European; Hispanic or Latin American

## Cellular component ontology<a name='Cellular component ontology'></a>
_A term that may be associated with an intra-cellular structure ontology term._

Location: module/ontology/cellular_component_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a subcellular structure. | string | yes |  | Subcellular structure |  | cytoplasm; nucleus
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Subcellular structure ontology ID |  | GO:0005737; GO:0005634
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Subcellular structure ontology label |  | cytoplasm; nucleus

## Library construction ontology<a name='Library construction ontology'></a>
_A term that may be associated with a process-related ontology term._

Location: module/ontology/library_construction_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a library construction approach being used. | string | yes |  | Library construction |  | 10X v2 sequencing; Smart-seq2
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Library construction ontology ID |  | EFO:0009310; EFO:0008931
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Library construction ontology label |  | 10X v2 sequencing; Smart-seq2

## Process type ontology<a name='Process type ontology'></a>
_A term that may be associated with a process-related ontology term._

Location: module/ontology/process_type_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a process type being used. | string | yes |  | Process type |  | enzymatic dissociation; blood draw
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Process type ontology ID |  | EFO:0009128; EFO:0009121
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Process type ontology label |  | enzymatic dissociation; blood draw

## Sequencing ontology<a name='Sequencing ontology'></a>
_A term that may be associated with a process-related ontology term._

Location: module/ontology/sequencing_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a sequencing approach being used. | string | yes |  | Sequencing approach |  | tag based single cell RNA sequencing; full length single cell RNA sequencing
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Sequencing approach ontology ID |  | EFO:0008440; EFO:0008441
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Sequencing approach ontology label |  | tag based single cell RNA sequencing; full length single cell RNA sequencing

## Species ontology<a name='Species ontology'></a>
_A term that may be associated with a species-related ontology term._

Location: module/ontology/species_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of the species to which the organism belongs. | string | yes |  | Species |  | Homo sapiens; Mus musculus
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Species ontology ID |  | NCBITaxon:9606; NCBITaxon:10090
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Species ontology label |  | Homo sapiens; Mus musculus

## Disease ontology<a name='Disease ontology'></a>
_A term that may be associated with a disease-related ontology term._

Location: module/ontology/disease_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The text for the term as the user provides it. | string | yes |  | Disease |  | type 2 diabetes mellitus; normal
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Disease ontology ID |  | MONDO:0005148; PATO:0000461
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Disease ontology label |  | type 2 diabetes mellitus; normal

## Strain ontology<a name='Strain ontology'></a>
_A term that may be associated with a strain-related ontology term._

Location: module/ontology/strain_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of the strain to which the organism belongs. | string | yes |  | Strain |  | C57BL/6; BALB/c
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Strain ontology ID |  | EFO:0004472; EFO:0000602
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Strain ontology label |  | C57BL/6; BALB/c

## File format ontology<a name='File format ontology'></a>
_A term that may be associated with a file format-related ontology term._

Location: module/ontology/file_format_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of the file format. | string | yes |  | File format |  | FASTQ; JSON
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | File format ontology ID |  | format:1930; format:3464
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | File format ontology label |  | FASTQ; JSON

## Enrichment ontology<a name='Enrichment ontology'></a>
_A term that may be associated with a process-related ontology term._

Location: module/ontology/enrichment_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of an enrichment approach being used. | string | yes |  | Enrichment |  | fluorescence-activated cell sorting; Ficoll-Hypaque method
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Enrichment ontology ID |  | EFO:0009108; EFO:0009110
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Enrichment ontology label |  | fluorescence-activated cell sorting; Ficoll-Hypaque method

## Organ part ontology<a name='Organ part ontology'></a>
_A term that may be associated with an anatomy-related ontology term._

Location: module/ontology/organ_part_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The text for the term as the user provides it. | string | yes |  | Organ part |  | bone marrow; islet of Langerhans
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Organ part ontology ID |  | UBERON:0002371; UBERON:0000006
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Organ part ontology label |  | bone marrow; islet of Langerhans

## Microscopy ontology<a name='Microscopy ontology'></a>
_A term that may be associated with a microscopy-related ontology term._

Location: module/ontology/microscopy_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of the type of microscopy used in an imaging experiment. | string | yes |  | Microscopy |  | confocal microscopy; fluorescence microscopy
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Microscopy ontology ID |  | FBbi:00000251; FBbi:00000246
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Microscopy ontology label |  | confocal microscopy; fluorescence microscopy

## Time unit ontology<a name='Time unit ontology'></a>
_A term that may be associated with a time unit-related ontology term._

Location: module/ontology/time_unit_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a time unit being used. | string | yes |  | Time unit |  | second; week
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Time unit ontology ID |  | UO:0000010; UO:0000034
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Time unit ontology label |  | second; week

## Protocol type ontology<a name='Protocol type ontology'></a>
_A term that may be associated with a protocol-related ontology term._

Location: module/ontology/protocol_type_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a protocol type used. | string | yes |  | Protocol type |  | dissociation protocol; enrichment protocol
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Protocol type ontology ID |  | EFO:0009088; EFO:0009089
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Protocol type ontology label |  | dissociation protocol; enrichment protocol

## Development stage ontology<a name='Development stage ontology'></a>
_A term that may be associated with a development stage-related ontology term._

Location: module/ontology/development_stage_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of the development stage of the organism. | string | yes |  | Development stage |  | human adult stage; Theiler stage 28
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Development stage ontology ID |  | HsapDv:0000087; EFO:0002588
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Development stage ontology label |  | human adult stage; Theiler stage 28

## Instrument ontology<a name='Instrument ontology'></a>
_A term that may be associated with a instrument-related ontology term._

Location: module/ontology/instrument_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The full name of the instrument used. | string | yes |  | Instrument |  | Illumina HiSeq 2500; ONT MinION
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Instrument ontology ID |  | EFO:0008565; EFO:0008632
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Instrument ontology label |  | Illumina HiSeq 2500; ONT MinION

## Mass unit ontology<a name='Mass unit ontology'></a>
_A term that may be associated with a cell type-related ontology term._

Location: module/ontology/mass_unit_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a mass unit being used. | string | yes |  | Mass unit |  | kilogram; microgram
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Mass unit ontology ID |  | UO:0000009; UO:0000023
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Mass unit ontology label |  | kilogram; microgram

## Biological macromolecule ontology<a name='Biological macromolecule ontology'></a>
_A term that may be associated with a biological macromolecule-related ontology term._

Location: module/ontology/biological_macromolecule_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of the biological macromolecule being used. | string | yes |  | Biological macromolecule |  | polyA RNA; mRNA
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Biological macromolecule ontology ID |  | OBI:0000869; CHEBI:33699
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Biological macromolecule ontology label |  | polyA RNA; messenger RNA

## Cell type ontology<a name='Cell type ontology'></a>
_A term that may be associated with a cell type-related ontology term._

Location: module/ontology/cell_type_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The name of a cell type supplied by a user. | string | yes |  | Cell type |  | bone marrow hematopoietic cell; cardiac muscle cell
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Cell type ontology ID |  | CL:1001610; CL:0000746
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Cell type ontology label |  | bone marrow hematopoietic cell; cardiac muscle cell

## Organ ontology<a name='Organ ontology'></a>
_A term that may be associated with an anatomy-related ontology term._

Location: module/ontology/organ_ontology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
text | The text for the term as the user provides it. | string | yes |  | Organ |  | heart; immune system
ontology | An ontology term identifier in the form prefix:accession. | string | no |  | Organ ontology ID |  | UBERON:0000948; UBERON:0002405
ontology_label | The preferred label for the ontology term referred to in the ontology field. This may differ from the user-supplied value in the text field. | string | no |  | Organ ontology label |  | heart; immune system

## Funder<a name='Funder'></a>
_Information about the project funding source._

Location: module/project/funder.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
grant_title | The name of the grant funding the project. | string | no |  | Grant title |  | Study of single cells in the human body.
grant_id | The unique grant identifier or reference. | string | yes |  | Grant ID |  | BB/P0000001/1
organization | The name of the funding organization. | string | yes |  | Funding organization |  | Biotechnology and Biological Sciences Research Council (BBSRC); California Institute of Regenerative Medicine (CIRM)

## Contact<a name='Contact'></a>
_Information about an individual who submitted or contributed to a project._

Location: module/project/contact.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
name | Name of individual who has contributed to the project. | string | yes |  | Contact name |  | John,D,Doe; Jane,,Smith
email | Email address for the individual. | string | no |  | Email address |  | dummy@email.com
phone | Phone number of the individual or their lab. | string | no |  | Phone number |  | (+1) 234-555-6789
institution | Name of primary institute where the individual works. | string | yes |  | Institute |  | EMBL-EBI; University of Washington
laboratory | Name of lab or department within the institute where the individual works. | string | no |  | Laboratory/Department |  | Division of Vaccine Discovery; Department of Biology
address | Street address where the individual works. | string | no |  | Street address |  | 0000 Main Street, Nowheretown, MA, 12091
country | Country where the individual works. | string | no |  | Country |  | USA
corresponding_contributor | Whether the individual is a primary point of contact for the project. | boolean | no |  | Corresponding contributor |  | Should be one of: yes, or no.
project_role | Primary role of the individual in the project. | object | no | [See module  contributor_role_ontology](module.md/#contributor_role_ontology) | Project role |  | principal investigator; computational scientist
orcid_id | The individual's ORCID ID linked to previous work. | string | no |  | ORCID ID |  | 0000-1111-2222-3333

## Publication<a name='Publication'></a>
_Information about a journal article, book, web page, or other external available documentation for a project._

Location: module/project/publication.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
authors | A list of authors associated with the publication. | array | yes |  | Authors |  | Doe JD
title | The title of the publication. | string | yes |  | Publication title |  | Study of single cells in the human body.
doi | The publication digital object identifier (doi) of the publication. | string | no |  | Publication DOI |  | 10.1016/j.cell.2016.07.054
pmid | The PubMed ID of the publication. | integer | no |  | Publication PMID |  | 27565351
url | A URL for the publication. | string | no |  | Publication URL |  | https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5667944/
official_hca_publication | Has the publication been accepted as an official HCA publication, according to the process described in https://www.humancellatlas.org/publications/ ? | boolean | no |  | Official HCA Publication? |  | yes; no

## Human-specific<a name='Human-specific'></a>
_Information specific to a donor that is a human (Homo sapiens)._

Location: module/biomaterial/human_specific.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
body_mass_index | The body mass index of the donor. | number | no |  | Body mass index |  | 36.4
ethnicity | Ethnicity of the donor. | array | no | [See module  ethnicity_ontology](module.md/#ethnicity_ontology) | Ethnicity |  | 

## Growth conditions<a name='Growth conditions'></a>
_Information relating to how a biomaterial was grown and/or maintained in a laboratory setting._

Location: module/biomaterial/growth_conditions.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
passage_number | The number of passages that the biomaterial has been through. | integer | no |  | Passage number |  | 22
growth_medium | The solid, liquid, or semi-solid medium used to support growth. | string | no |  | Growth medium |  | human placental cord serum; RPMI 1640 + 2mM Glutamine + 10-20% FBS
culture_environment | Cell culture environment in which cells are grown. | string | no |  | Culture environment |  | Adherent cell culture; Suspension cell culture
mycoplasma_testing_method | The method by which the biomaterial was tested for mycoplasma contamination. | string | no |  | Mycoplasma testing method | Direct DNA stain, Indirect DNA stain, Broth and agar culture, PCR, Nested PCR, ELISA, Autoradiography, Immunostaining, Cell-based assay, Microbiological assay | Should be one of: Direct DNA stain, Indirect DNA stain, Broth and agar culture, PCR, Nested PCR, ELISA, Autoradiography, Immunostaining, Cell-based assay, or Microbiological assay.
mycoplasma_testing_results | Whether the biomaterial passed or failed the mycoplasma test. | string | no |  | Mycoplasma testing results | pass, fail | Should be one of: pass, or fail.
drug_treatment | Description of drugs added to the growth medium. | string | no |  | Drug treatment |  | 100 ug/mL ampicillin; 15 ug/mL tetracycline
feeder_layer_type | Type of feeder layer cells on which biomaterial was grown. | string | no |  | Feeder layer type | feeder-free, feeder-dependent, JK1 feeder cells, feeder-dependent, SNL 76/7 feeder cells, feeder-dependent, human marrow stromal cells, feeder-dependent, bovine embryonic fibroblast cells, feeder-dependent, mouse embryonic fibroblast cells, feeder-dependent, mouse fibroblast STO cells, feeder-dependent, mouse bone marrow stromal cells, feeder-dependent, mouse yolk sac-derived endothelial cells, feeder-dependent, human foreskin fibroblast cells, feeder-dependent, human newborn fibroblast cells, feeder-dependent, human fetal lung fibroblast cells, feeder-dependent, human uterine endometrial cells, feeder-dependent, human breast parenchymal cells, feeder-dependent, human embryonic fibroblast cells, feeder-dependent, human adipose stromal cells, feeder-dependent, human amniotic epithelial cells, feeder-dependent, human placental fibroblast cells, feeder-dependent, human umbilical cord stromal cells, feeder-dependent, human fetal muscle cells, feeder-dependent, human fetal skin cells, feeder-dependent, human fetal liver stromal cells, feeder-dependent, human fallopian tubal epithelial cells, feeder-dependent, human amniotic mesenchymal cells | feeder-free; feeder-dependent, mouse embryonic fibroblast cells

## Preservation and storage<a name='Preservation and storage'></a>
_Information relating to how a biomaterial was preserved and/or stored over a period of time._

Location: module/biomaterial/preservation_storage.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
storage_method | The method by which a biomaterial was stored after preservation or before another protocol was used. | string | no |  | Storage method | ambient temperature, cut slide, fresh, frozen at -70C, frozen at -80C, frozen at -150C, frozen in liquid nitrogen, frozen in vapor phase, paraffin block, RNAlater at 4C, RNAlater at 25C, RNAlater at -20C | frozen in liquid nitrogen; fresh
storage_time | Length of time the biomaterial was stored for in Storage time units. | number | no |  | Storage time |  | 5
storage_time_unit | The unit in which Storage time is expressed. | object | no | [See module  time_unit_ontology](module.md/#time_unit_ontology) | Storage time unit |  | 
preservation_method | The method by which a biomaterial was preserved through the use of chemicals, cold, or other means to prevent or retard biological or physical deterioration. | string | no |  | Preservation method | cryopreservation in liquid nitrogen (dead tissue), cryopreservation in dry ice (dead tissue), cryopreservation of live cells in liquid nitrogen, cryopreservation, other, formalin fixed, unbuffered, formalin fixed, buffered, formalin fixed and paraffin embedded, hypothermic preservation media at 2-8C, fresh | cryopreservation in liquid nitrogen (dead tissue); fresh

## Death<a name='Death'></a>
_Information relating to the death of an organism._

Location: module/biomaterial/death.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
cause_of_death | Conditions resulting in death. | string | yes |  | Cause of death |  | Hypoxic brain damage; Sudden cardiac arrest
cold_perfused | Whether perfusion with cold fluid was used to help preserve tissues before heart stopped. | boolean | no |  | Cold perfused |  | Should be one of: yes, no.
days_on_ventilator | Number of days on ventilator before death occurred. | number | no |  | Number of days on ventilator |  | 4
hardy_scale | Value on 4-point Hardy scale cause of death classification. | integer | no |  | Value on Hardy scale |  | 0
time_of_death | Date and time when death was declared. | string | no |  | Time of death |  | 2016-01-21T00:00:00Z; 2016-03
organ_donation_death_type | Type of death preceding organ donation. | string | no |  | Organ donation death type | Donation after circulatory death (DCD), Donation after brainstem death (DBD) | Should be one of: Donation after circulatory death (DCD), or Donation after brainstem death (DBD).
normothermic_regional_perfusion | Whether entire body was perfused with warm oxygenated blood. | string | no |  | Normothermic regional perfusion | yes, no, unknown | Should be one of: yes, no, or unknown.

## Familial relationship<a name='Familial relationship'></a>
_Information about other organisms that this organism is related to._

Location: module/biomaterial/familial_relationship.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
parent | The individual's parent. | string | no |  | Parent |  | 
child | The individual's child. | string | no |  | Child |  | 
sibling | The individual's sibling. | string | no |  | Sibling |  | 

## Medical history<a name='Medical history'></a>
_Information about the medical history of a donor._

Location: module/biomaterial/medical_history.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
alcohol_history | Estimated amount of alcohol consumed per day. | string | no |  | Alcohol history |  | 3-6 alcohol units/day; 1 drink per day
medication | Medications the individual was taking at time of biomaterial collection. | string | no |  | Medications |  | Naproxen 500mg/day; Citalopram 20mg/day
smoking_history | Estimated number of cigarettes smoked per day. | string | no |  | Smoking history |  | 20 cigarettes/day for 25 years, stopped 2000
nutritional_state | Nutritional state of individual at time of biomaterial collection. | string | no |  | Nutritional state | normal, fasting, feeding tube removed | Should be one of: normal, fasting, or feeding tube removed.
test_results | Results from medical tests performed on the individual. | string | no |  | Test results |  | lipid panel shows normal level of LDL (124 mg/dL); HIV, HBV, HCV: Negative
treatment | Treatments the individual has undergone prior to biomaterial collection. | string | no |  | Treatments |  | Patient treated with antibiotics for a urinary tract infection; Patient treated with chemotherapy (Epirubicin, cisplatin, capecitabine) to treat stomach cancer

## Cell morphology<a name='Cell morphology'></a>
_Information relating to pathological and morphological features of cells._

Location: module/biomaterial/cell_morphology.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
cell_morphology | General description of the morphology of cells. | string | no |  | Cell morphology |  | adherent cells; form single layer colonies
cell_size | Size of cells in Cell size unit. | string | no |  | Cell size |  | 15; 20-30
cell_size_unit | The unit in which the Cell size is expressed. | object | no | [See module  length_unit_ontology](module.md/#length_unit_ontology) | Cell size unit |  | 
percent_cell_viability | Percent of cells determined to be viable. | number | no |  | Percent cell viability |  | 98.7
cell_viability_method | The method by which cell viability was determined. | string | no |  | Cell viability method |  | Fluorescein diacetate hydrolysis; ATP test
cell_viability_result | Result of the cell viability test. | string | no |  | Cell viability result | pass, fail | Should be one of: pass, fail
percent_necrosis | Percent of cells identified to be necrotic. | number | no |  | Percent necrotic cells |  | 10

## State of specimen<a name='State of specimen'></a>
_State of specimen at time of collection._

Location: module/biomaterial/state_of_specimen.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
autolysis_score | State of tissue breakdown due to self-digestion. | string | no |  | Autolysis score | none, mild, moderate | Should be one of: none, mild, or moderate.
gross_description | Color, size, and other aspects of specimen as visible to naked eye. | string | no |  | Gross description |  | focal wedge shaped region of tan-orange discoloration; cystic
gross_images | List of filenames of photographs of specimen without magnification. | array | no |  | Gross image |  | my_gross_image_file.jpg
ischemic_temperature | Whether specimen experienced warm or cold ischemia. | string | no |  | Ischemic temperature | warm, cold | Should be one of: warm, or cold.
ischemic_time | Duration of time, in seconds, between when the specimen stopped receiving oxygen and when it was preserved or processed. | integer | no |  | Ischemic time |  | 7200
microscopic_description | How the specimen looks under the microscope and how it compares with normal cells. | string | no |  | Microscopic description |  | Mixture of different cell sizes apparent; Dead cells are quite faint on microscope
microscopic_images | List of filenames of photographs of specimen under microscope. | array | no |  | Microscopic image |  | my_microscopic_image_file.jpg
postmortem_interval | Duration of time between when death was declared and when the specimen was preserved or processed. | integer | no |  | Post-mortem interval |  | 2400

## Timecourse<a name='Timecourse'></a>
_Information relating to a timecourse._

Location: module/biomaterial/timecourse.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
value | The numerical value in Timecourse unit associated with a time interval used in the experiment. | string | yes |  | Timecourse value |  | 2; 5.5-10.5
unit | The unit in which the Timecourse value is expressed. | object | yes | [See module  time_unit_ontology](module.md/#time_unit_ontology) | Timecourse unit |  | 
relevance | Relevance of the Timecourse value/unit to the experiment. | string | no |  | Timecourse relevance |  | Collection after tumor cells injected into the mammary gland; Time tissue underwent liberase digestion

## Mouse-specific<a name='Mouse-specific'></a>
_Information specific to an organism that is a mouse (Mus musculus)._

Location: module/biomaterial/mouse_specific.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
strain | The name of the mouse strain. | array | no | [See module  strain_ontology](module.md/#strain_ontology) | Mouse strain |  | 

## Purchased reagents<a name='Purchased reagents'></a>
_Information describing purchased kits or reagents used in a protocol._

Location: module/process/purchased_reagents.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
retail_name | The retail name of the kit/reagent. | string | no |  | Retail name |  | SureCell WTA 3' Library Prep Kit; CytoTune iPS 2.0 Sendai Reprogramming Kit
catalog_number | The catalog number of the kit/reagent. | string | no |  | Catalog number |  | 20014279
manufacturer | The manufacturer of the kit/reagent. | string | no |  | Manufacturer |  | Illumina; ThermoFisher Scientific
lot_number | The batch or lot number of the kit/reagent. | string | no |  | Batch/lot number |  | 10001A
expiry_date | The date of expiration for the kit/reagent. | string | no |  | Expiry date |  | 2018-01-31; 2018-01
kit_titer | Appropriate titer and volume recommendations found in kit/reagent Certificate of Analysis. | string | no |  | Titer |  | 3.0x10^7

## INSDC experiment<a name='INSDC experiment'></a>
_Information relating to an INSDC experiment._

Location: module/process/sequencing/insdc_experiment.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
insdc_experiment_accession | An International Nucleotide Sequence Database Collaboration (INSDC) experiment accession. | string | yes |  | INSDC experiment accession |  | SRX0000000

## Barcode<a name='Barcode'></a>
_Information about barcodes used in a protocol._

Location: module/process/sequencing/barcode.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
barcode_read | The read in which the barcode is found. | string | yes |  | Barcode-containing read | Read 1, Read 2, i7 Index, i5 Index | Should be one of: Read 1, Read 2, i7 Index, or i5 Index.
barcode_offset | The 0-based offset of start of barcode in read. | integer | yes |  | Barcode offset |  | 0
barcode_length | Length of barcode in nucleotides. | integer | yes |  | Barcode length |  | 28
white_list_file | Name of file containing legitimate barcode sequences. | string | no |  | White list barcode file |  | barcode_whitelist_file.txt

## 10x-specific<a name='10x-specific'></a>
_Information specific to 10x experiments._

Location: module/process/sequencing/10x.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
fastq_method | Method used for the generation of fastq files from bcl files. | string | no |  | Fastq creation method |  | Cellranger mkfastq; bcl2fastq2
fastq_method_version | Version of the program used for fastq generation. | string | no |  | Fastq creation method version |  | Cellranger 2.1.1; v2.20
pooled_channels | The number of channels pooled within a sequencing lane. | number | no |  | Pooled channels |  | 4
drop_uniformity | Whether drop uniformity was achieved as a result of visual inspection of emulsion after a 10x run. | boolean | no |  | Drop uniformity |  | Should be one of: yes, or no.

## Plate-based sequencing<a name='Plate-based sequencing'></a>
_Information specific to plate-based sequencing experiments._

Location: module/process/sequencing/plate_based_sequencing.json

Property name | Description | Type | Required? | Object reference? | User friendly name | Allowed values | Example 
--- | --- | --- | --- | --- | --- | --- | --- 
plate_label | A label or name for the plate on which the well is located. | string | yes |  | Plate label |  | 2217
well_label | A label or name for the well in which the cell is located. | string | no |  | Well label |  | A1
well_quality | Quality of well if imaged before sequencing. | string | no |  | Well quality | OK, control, 2-cell well, control, empty well, low quality cell | Should be one of: 'OK', 'control, 2-cell well', 'control, empty well', or 'low quality cell'.

