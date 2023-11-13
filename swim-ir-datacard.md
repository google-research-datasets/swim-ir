# DataCard of SWIM-IR
We release a synthetic multilingual retrieval training dataset, titled SWIM-IR (Synthetic Wikipedia-based Multilingual IR dataset), generated using Wikipedia and PaLM 2, including both monolingual and cross-lingual retrieval training data. The goal of releasing the data is to support and encourage work in different language settings by the academic research community and facilitate the development of novel techniques for information retrieval across a plethora of languages.

#### Dataset Link
<!-- info: Provide a link to the dataset: -->
<!-- width: half -->
SWIM-IR v1.0: http://storage.googleapis.com/gresearch/swim-ir/swim_ir_v1.tar.gz

#### Data Card Author(s)
<!-- info: Select **one role per** Data Card Author:

(Usage Note: Select the most appropriate choice to describe the author's role
in creating the Data Card.) -->
<!-- width: half -->
- **Nandan Thakur, University of Waterloo:** Owner
- **Daniel Cer, Google Research:** Owner
- **Jianmo Ni, Google DeepMind:** Contributor
- **John Wieting, Google DeepMind:** Contributor
- **Gustavo Hernandez Abrego, Google Research:** Contributor
- **Jimmy Lin, University of Waterloo:** Contributor

## Authorship
### Publishers
#### Publishing Organization(s)
<!-- scope: telescope -->
<!-- info: Provide the names of the institution or organization responsible
for publishing the dataset: -->
University of Waterloo, Google Research, Google DeepMind

#### Industry Type(s)
<!-- scope: periscope -->
<!-- info: Select **all applicable** industry types to which the publishing
organizations belong: -->
- Corporate - Tech
- Academic - Tech

### Dataset Owners
#### Team(s)
<!-- scope: telescope -->
<!-- info: Provide the names of the groups or team(s) that own the dataset: -->
SWIM-IR Team

#### Contact Detail(s)
<!-- scope: periscope -->
<!-- info: Provide pathways to contact dataset owners: -->
- **Dataset Owner(s):** Nandan Thakur, Daniel Cer
- **Affiliation:** University of Waterloo, Google Research
- **Contact:** [swim-ir-dataset@googlegroups.com](mailto:swim-ir-dataset@googlegroups.com)

#### Author(s)
<!-- scope: microscope -->
<!-- info: Provide the details of all authors associated with the dataset:

(Usage Note: Provide the affiliation and year if different from publishing
institutions or multiple affiliations.) -->
- Nandan Thakur, PhD Student, University of Waterloo (Work done as a student researcher at Google Research)
- Daniel Cer, Research Scientist, Google Research
- Jianmo Ni, Software Engineer, Google DeepMind
- Gustavo Hernandez Abrego, Software Engineer, Google Research
- John Wieting, Research Scientist, Google DeepMind
- Jimmy Lin, Professor, University of Waterloo

## Dataset Overview
#### Data Subject(s)
<!-- scope: telescope -->
<!-- info: Select ***all applicable**** subjects contained the dataset: -->
- Synthetically generated data

#### Dataset Snapshot
<!-- scope: periscope -->
<!-- info: Provide a snapshot of the dataset:<br><br>(Use the additional notes
to include relevant information, considerations, and links to table(s) with
more detailed breakdowns.) -->
SWIM-IR is a synthetic multilingual retrieval training dataset. It contains training pairs for both settings: monolingual, i.e. within language and cross-lingual, i.e. across language. The dataset is useful to fine-tune state-of-the-art (SoTA) synthetic monolingual and cross-lingual neural retrievers across diverse languages.


Category | Data
--- | ---
Size of Dataset | ~6-7 GB
Number of Instances | 28,265,848
Number of Fields | 6
Labeled Classes | 33*
Number of Labels | 1

**Above:** Dataset statistics comprises both in language and cross-language settings. Classes above denote a language.

**Additional Notes:** (*) Classes denote the languages we cover in the SWIM-IR dataset. Here is a list of the 18 languages and their ISO codes listed in the alphabetical order: Arabic (ar), Bengali (bn), German (de), English (en), Spanish (es), Persian (fa), Finnish (fi), French (fr), Hindi (hi), Indonesian (id), Japanese (ja), Korean (ko), Russian (ru), Swahili (sw), Thai (th), Yoruba (yo),
Chinese (zh) and rest 15 Indo-European Languages: Assamese (as), Bhojpuri (bho), Konkani (gom), Gujarati (gu), Kannada (kn), Maithili (mai), Malayalam (ml), Manipuri (mni), Marathi (mr), Odia (or), Punjabi (pa), Pashto (ps), Sanskrit (sa), Tamil (ta), Urdu (ur).

#### Content Description
<!-- scope: microscope -->
<!-- info: Provide a short description of the content in a data point: -->
A paragraph is sampled from the Wikipedia corpus which describes an entity. The question arising from the Wikipedia
paragraph is generated using a large language model (LLM). In our work, we used the PaLM 2-S (small) model to generate
synthetic queries across **33 languages**, covering 11 distinct scripts, 10 language families comprising over 3 billion speakers in the world.

The SWIM-IR dataset contains about **28 million** Wikipedia synthetic query-paragraph training pairs with a multilingual query for each passage generated using PaLM 2 (small), for both cross-lingual and monolingual retrieval settings.

**Additional Notes:**
- The dataset creation follows a specific procedure which involves `summarize-then-ask` prompting technique inspired by chain-of-thought prompting (Wei et al. 2022).
- PaLM 2 uses **summarize-then-ask promping** containing 5-shot exemplars for cross-lingual and 3-shot exemplars for monolingual query generation. The prompt contains the original paragraph, human-generated summary and a question translated from English using Machine Translation (MT) for cross-lingual generation, whereas for randomly sampled training dataset pairs, and summaries generated using BARD for monolingual generation. PaLM 2 generates an extractive summary which is used as a proxy to help understand the document and highlight relevant sections within the document. Finally, the model generates a question in the target language (different in cross-lingual or same in monolingual) which can be answered using the input paragraph.

### Sensitivity of Data
#### Sensitivity Type(s)
<!-- scope: telescope -->
<!-- info: Select ***all applicable*** data types present in the dataset: -->
- None

#### Field(s) with Sensitive Data
<!-- scope: periscope -->
<!-- info: List fields in the dataset that contain S/PII, and specify if their
collection was intentional or unintentional.

Use additional notes to capture any other relevant information or
considerations. -->
**Intentional Collected Sensitive Data**
No sensitive data was intentionally collected.

**Unintentionally Collected Sensitive Data**
S/PII, violent, abusive or toxic text containing racial slurs were not explicitly collected as a part of the dataset creation
process. Sensitive subject and adult content was automatically filtered using the method described in (Thakur et al. 2023).

#### Security and Privacy Handling
<!-- scope: microscope -->
<!-- info: Summarize the measures or steps to handle sensitive data in this
dataset.

Use additional notes to capture any other relevant information or
considerations. -->

We used algorithmic methods and relied on other classifiers for data filtration. Specifically we (1) did a human inspection of text samples, with the questions automatically translated to English; (2) our observations motivated using a classifier to filter text containing sensitive subject and adult content.

## Example of Data Points
#### Primary Data Modality
<!-- scope: telescope -->
<!-- info: Select **one**: -->
- Text Data

#### Data Fields
<!-- scope: microscope -->
<!-- info: List the fields in data points and their descriptions.

(Usage Note: Describe each field in a data point. Optionally use this to show
the example.) -->

| Field name | Datapoint Example | Description |
| --------- | -------- | -------- |
| `lang` | String | The language of the generated question |
| `code` | String | The ISO-Code for the language |
| `query` | String | The generated query using PaLM 2 |
| `_id` | String | unique ID denoting the training pair |
| `title` | String | Title of the Wikipedia article |
| `text` | String | Paragraph of the Wikipedia article 

#### Typical Data Point
<!-- width: half -->
<!-- info: Provide an example of a typical data point and describe what makes
it typical.

**Use additional notes to capture any other relevant information or
considerations.** -->
Example of (English -> Japanese) datapoint from our
cross-lingual dataset on the topic of “The Roki Tunnel” from the
English Wikipedia.

```
{'lang': 'Japanese',
'code': 'ja',
'query': 'The Roki Tunnel は、北オセチア自治共和国と南オセチア共
和国の間を通る唯一の道路ですか?',
'_id': '1234',
'title': 'The Roki Tunnel',
'text': "The Roki Tunnel (also called Roksky Tunnel, ; Ossetic:
Ручъы тъунел; ) is a mountain tunnel of the Transkam road
through the Greater Caucasus Mountains, north of the village
Upper Roka. It is the only road joining North Ossetia–Alania in
the Russian Federation into South Ossetia, a breakaway
republic of Georgia. The road is manned at the town of Nizhny
Zaramag in North Ossetia and is sometimes referred to as the
Roki-Nizhny Zaramag border crossing. The tunnel, completed
by the Soviet government in 1984, is one of only a handful of
routes that cross the North Caucasus Range."}
```

Example of Hindi (hn) datapoint from our monolingual dataset
on the topic of “Aryabhata” from the Hindi Wikipedia

```
{'lang': 'Hindi',
'code': 'hn',
'query': 'आर्यभर्य ट केरल के कि स स्थान के नि वासी थे ?',
'_id': 'hindi_8987#4',
'title': 'आर्यभर्य ट',
'text': "एक ताजा अध्ययन के अनसु ार आर्यभर्य ट, केरल के
चाम्रवत्तम (१०उत्तर५१, ७५पर्वू ४र्व ५) के नि वासी थे। अध्ययन के अनसु ार
अस्मका एक जनै प्रदेश था जो कि श्रवणबेलगोल के चारों तरफ फैला
हुआ था और यहाँके पत्थर के खम्बों के कारण इसका नाम अस्मका
पड़ा। चाम्रवत्तम इस जनै बस्ती का हि स्सा था, इसका प्रमाण है
भारतापझु ा नदी जि सका नाम जनै ों के पौराणि क राजा भारता के नाम
पर रखा गया है। आर्यभर्य ट ने भी यगु ों को परि भाषि त करते वक्त राजा
भारता का जि क्र कि या है- दसगीति का के पांचवें छंद में राजा भारत
के समय तक बीत चकुे काल का वर्णनर्ण आता है। उन दि नों में
कुसमु परुा में एक प्रसि द्ध वि श्ववि द्यालय था जहाँजनै ों का नि र्णा यक
प्रभाव था और आर्यभर्य ट का काम इस प्रकार कुसमु परुा पहुँच सका और
उसे पसदं भी कि या गया।"}
```

#### Atypical Data Point
<!-- width: half -->
<!-- info: Provide an example of an outlier data point and describe what makes
it atypical.

**Use additional notes to capture any other relevant information or
considerations.** -->
The dataset does not contain atypical data points as far as we know.

## Motivations & Intentions
### Motivations
#### Purpose(s)
<!-- scope: telescope -->
<!-- info: Select **one**: -->
- Research

#### Domain(s) of Application
<!-- scope: periscope -->
<!-- info: Provide a list of key domains of application that the dataset has
been designed for:<br><br>(Usage Note: Use comma-separated keywords.) -->
`Multilingual Dense Retrieval`, `Synthetic Dataset`

## Provenance
### Collection
#### Method(s) Used
<!-- scope: telescope -->
<!-- info: Select **all applicable** methods used to collect data: -->
- Artificially Generated
- Taken from other existing datasets

#### Methodology Detail(s)
<!-- scope: periscope -->
<!-- info: Provide a description of each collection method used.

Use additional notes to capture any other relevant information or
considerations.

(Usage Note: Duplicate and complete the following for collection method
type.) -->
**Collection Type**

**Source:** TyDI-QA dataset which provided the English Wikipedia dataset for SWIM cross-lingual IR dataset. MIRACL
provided the language specific Wikipedia datasets for monolingual SWIM-IR datasets.

**Is this source considered sensitive or high-risk?** [Yes/**No**]

**Dates of Collection:** TyDI-QA [unknown - 01/02/2019], MIRACL [unknown - 01/02/2023], XTREME-UP [unknown - 01/02/2023]

**Primary modality of collection data:**
- Text Data

**Update Frequency for collected data:**
- Static

#### Source Description(s)
<!-- scope: microscope -->
<!-- info: Provide a description of each upstream source of data.

Use additional notes to capture any other relevant information or
considerations. -->
- **TyDI-QA:**  TyDi-QA (Clark et al. 2020) provided the English Wikipedia passages which have been split into 100 word long paragraphs. It contains around 18.2M passages from the complete English Wikipedia. We selected passages with a maximum of 1M pairs for each language pair (for 17 languages) at random for the preparation of our cross-lingual SWIM-IR dataset.
- **MIRACL:** MIRACL (Zhang et al. 2022) provides language-specific paragraphs from the Wikipedia Corpus. The paragraphs were generated by splitting on the “\n\n” delimiter. The MIRACL dataset provides corpora for 18 languages. We selected passages with a maximum of 1M pairs for each language at random for the preparation of our mono-lingual SWIM-IR dataset.
- **XTREME-UP:** XTREME-UP (Ruder et al. 2023) provides a 120K sample of the TyDi-QA (Clark et al. 2020) English Wikipedia passages which have been split into 100 word long paragraphs. This sample has been used in the original dataset for cross-language question answering.

#### Collection Cadence
<!-- scope: telescope -->
<!-- info: Select **all applicable**: -->
**Static:** Data was collected once from single or multiple sources.

#### Data Integration
<!-- scope: periscope -->
<!-- info: List all fields collected from different sources, and specify if
they were included or excluded from the dataset.

Use additional notes to
capture any other relevant information or considerations.

(Usage Note: Duplicate and complete the following for each upstream
source.) -->
**TyDi-QA (XOR-Retrieve and XTREME-UP)**

**Included Fields**
The English Wikipedia title, text and `_id` fields were taken from the TyDi-QA dataset which was originally provided as a tsv file containing all fields.

**Excluded Fields**
Rest of the metadata apart from the fields mentioned above were excluded from our SWIM dataset. We do not use any training data provided from the TyDI-QA dataset.

**MIRACL**

**Included Fields**
The Language Wikipedia title, text and `_id` fields were taken from the MIRACL dataset which was originally provided as a jsonlines file containing all fields.

**Excluded Fields**
Rest of the metadata apart from the fields mentioned above were excluded from our SWIM dataset. We do not use any training data provided from the MIRACL dataset.

#### Data Processing
<!-- scope: microscope -->
<!-- info: Summarize how data from different sources or methods aggregated,
processed, or connected.

Use additional notes to capture any other
relevant information or considerations.

(Usage Note: Duplicate and complete the following for each source OR
collection method.) -->
All data is coming directly from the TyDI-QA and MIRACL datasets without any preprocessing.

### Collection Criteria
#### Data Selection
<!-- scope: telescope -->
<!-- info: Summarize the data selection criteria.

Use additional notes to capture any other relevant information or
considerations. -->
For the Cross-lingual SWIM-IR dataset, we use a stratified sampling technique to select a subset of passages from the English Wikipedia corpus. We use to generate questions for SWIM-IR. We ensure all languages have relatively an equal amount of training samples, wherever possible. Our Wikipedia corpus contains entities which are sorted alphabetically (A-Z). We then compute inclusion threshold $I_{th}$, which is defined as $I_{th} = D_{sample} / D_{total}$, where $(D_{sample})$ is number of passages required to sample and $(D_{total})$ is the total numbers of passages in corpus. Next, for each passage ($p_i$) in the corpus, we randomly generate an inclusion probability $\hat{p_i} \in [0,1]$. We select the passage ($p_i$) if $p_i \leq I_{th}$. This ensures uniform sampling of passages with Wikipedia entities between all letters (A-Z).

For the Monolingual SWIM-IR dataset, the language selection criteria was dependent on the Wikipedia corpora availability for the monolingual task. Hence, we chose to fix on the 18 languages provided in MIRACL. To complete the dataset, we included the same languages for the cross-lingual task.

#### Data Inclusion
<!-- scope: periscope -->
<!-- info: Summarize the data inclusion criteria.

Use additional notes to capture any other relevant information or
considerations. -->
We include all data available in TyDi-QA English Wikipedia Corpus (maximum of 1M training pairs per language pair), which we use to generate our cross-lingual SWIM-IR dataset. We use the language-specific MIRACL Wikipedia corpora to generate our monolingual queries in SWIM-IR.

#### Data Exclusion
<!-- scope: microscope -->
<!-- info: Summarize the data exclusion criteria.

Use additional notes to capture any other relevant information or
considerations. -->
We removed data classified as containing sensitive subject and adult content using the method described in (Thakur et al. 2023). No additional filters were applied for data exclusion from MIRACL or TyDi-QA. 

The TyDi-QA English paragraph data has been
splitted originally with a maximum of up to 100 tokens. However, MIRACL used the “\n\n” delimiter to segment
paragraphs from the Wikipedia articles.