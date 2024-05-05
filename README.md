# GenoVardis Competition - ProfNER-ST Baseline 1 - Lookup

## Introduction
This system serves the purpose of extracting information from a set of annotated documents and subsequently verifying whether these extracted annotations are present in a new set of documents. This system is established as a baseline for the **GenoVardis shared task**. For evaluation, please refer to the competition on CodaLab: [GenoVardis Competition](https://codalab.lisn.upsaclay.fr/competitions/17733).

#### Steps: 
1. Extract annotations from tab-separated file and tokenize them.
2. For a new text, tokenize words. 
3. Get the intersection between tokens in annotations and tokens in words.
4. For a token in the intersection, check surroundings of every occurrence in the text, to confirm whether there is a match with any annotation.
5. Repeat step 4 for every token in the intersection.
6. Repeat steps 2-5 for every file in the directory.

#### Input format
+ Gold standard: a tab-separated file with annotations. Format (contains headers):
```
pmid	filename	mark	label	offset1	offset2	span
```

+ A tab-separated file where predictions will be made, with the following format:
```
pmid	filename	text
```

#### Output format
+ Tab-separated file with annotations. Format:
```
pmid	filename	label	offset1	offset2	span
```

**IMPORTANT!** `pmid` and `filename` (will be `.ann`, not `.txt`) are the unique document identifiers (see for instant, `train_annotations.tsv`), `label` is the name of entity type in the annotation, `offset1` and `offset2` are the beginning and end offsets of the annotation span in the text document, and `span` is the actual text of the span.

## Getting Started

Scripts are written in `Python 3.10.12`, over `Ubuntu 22.04.4 LTS` distribution.

### Prerequisites

Ensure you have Python 3.10 installed along with its base libraries, plus:
+ pandas
+ unicodedata2
+ spacy

### Installing

```
git clone <repo_url>
pip install -r <repo_name>/requirements.txt
```

## Usage

Both scripts accept the same two parameters:
+ --gs_path (-gs) specifies the path to the Gold Standard file.
+ --data_path (-data) specifies the path to the text files.
+ --out_path (-out) specifies the path to the output predictions file.

+ --gs_path (-gs) specifies the path to the Gold Standard file.
+ --gs_path2 (-gs2) specifies the path to an additional GS file (not mandatory parameter).
+ --data_path (-data) specifies the path to the tab-separated file (text records to predict).
+ --out_path (-out) specifies the path to the output predictions file.
+ --sub_track (-t) allways 2, for NER.

Example:
```
python lookup.py -gs train_annotation.tsv -data dev_text.tsv -out lookup_dev_predictions.tsv -t 2
```

## Submission
Participants' submissions are expected to be a .zip file containing a .tsv file with a format analogous to the annotations file, except without the `mark` colum.

**Note:** Codalab requires that each submission is inside a .zip file.

## Contact
Marvin M. Agüero-Torales (marvinmatias.aguerotorrales@fujitsu.com)
Antonio Miranda (antoniomiresc@gmail.com)
```