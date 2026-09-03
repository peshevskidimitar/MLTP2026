# Day 4 Data Sources

Every file in this directory derives from one published dataset, which is cited
and licensed below. Nothing here was generated, and nothing was collected for
this workshop.

## The Source Dataset

- **Title:** Dataset of anonymized discharge summaries of sepsis patients from
  a Brazilian tertiary hospital for NLP applications.
- **Authors:** Rildo Pinto da Silva and Antonio Pazin-Filho, Faculdade de
  Medicina de Ribeirão Preto, Universidade de São Paulo, Brazil.
- **Repository:** Harvard Dataverse, version 2.0, released 2 May 2025.
- **DOI:** `10.7910/DVN/GWNBQQ`.
- **Licence:** Creative Commons Zero 1.0 Universal, which places the deposit in
  the public domain and attaches no condition to redistribution.
- **Citation:** Pinto da Silva, Rildo; Pazin-Filho, Antonio (2025). Dataset of
  anonymized discharge summaries of sepsis patients from a Brazilian tertiary
  hospital for NLP applications. Harvard Dataverse, V2.
  `https://doi.org/10.7910/DVN/GWNBQQ`.

The dataset accompanies one paper, which is the work to cite when writing about
results obtained from it.

- Silva, Rildo Pinto da, and Antonio Pazin-Filho. "Dataset of anonymized
  discharge summaries of sepsis patients from a Brazilian tertiary hospital for
  NLP applications." Data in Brief 61 (2025), article 111804.
  `https://doi.org/10.1016/j.dib.2025.111804`.

The licences of the deposit and of the paper differ, and the difference matters
here. The deposit is CC0, so these files may be redistributed. The paper is
Creative Commons Attribution-NonCommercial 4.0, so quoting the paper carries
conditions that using the data does not. Credit is given above in either case,
because a citation is owed to the authors whether or not a licence compels it.

## What The Source Contains

The deposit holds one workbook of three sheets and the Jupyter notebook that
documents its preparation. The workbook holds 200 anonymized discharge
summaries written in Brazilian Portuguese, each with an English translation, a
list of ICD-10 diagnoses in both languages, and five structured clinical fields
drawn from elsewhere in the hospital's record system.

The authors describe the provenance as follows. Adult admissions coded for
sepsis under the tenth revision of the International Classification of Diseases
were extracted from the electronic health record of a Brazilian tertiary
teaching hospital, beginning with 1757 patients across 1940 admissions. A
physician reviewed the text of each admission and kept those that described the
history of the illness, the physical examination, laboratory or imaging
results, and the treatment given, necessarily including antibiotic therapy and
a stated diagnosis of sepsis. That review left 387 summaries. The text was then
cleaned of layout characters, its abbreviations were expanded from a dictionary
the authors built, and it was anonymized in two automated stages, first by the
GLiNER model for personally identifying information and then by a spaCy model
the authors trained. Years appearing in dates were renumbered from 2020 onward.
A final manual review by a physician confirmed confidentiality, corrected the
structured fields, and excluded summaries unsuitable for teaching, which left
the 200 records published here.

Identifying spans were replaced in the text by a label naming what was removed,
so a bracketed word marks a redaction rather than an error. The two kinds of
bracket record the two stages of the review. The automated stage wrote square
brackets, giving `[person]`, `[organization]`, `[address]`, `[city]`,
`[phone number]`, `[postal code]`, and `[registration number]`, and it accounts
for 1650 of the labels in the English text. The manual stage wrote braces,
giving `{omitted}`, `{date of birth}`, `{city}`, `{hospital registration}`, and
a few others, and it accounts for 369.

Braces therefore mark the reviewing physician's work wherever they appear,
whether in the text or in the clinical columns described below.

## What This Directory Contains

- `discharge_summaries.csv`, holding 200 rows and 11 columns.
- `abbreviations.csv`, holding the 309 medical abbreviations the authors
  expanded, with the Portuguese expansion and its English translation.
- `icd_codes.csv`, holding the 30 ICD-10 subcategories used to identify sepsis,
  with the Portuguese description and its English translation.

The columns of `discharge_summaries.csv` are the following.

| Column | Contents |
| --- | --- |
| `record_id` | A number from 1 to 200, being this directory's own row numbering. |
| `summary_pt` | The anonymized discharge summary, in Brazilian Portuguese. |
| `summary_en` | The authors' English translation of the same summary. |
| `diagnosis_pt` | The ICD-10 diagnoses recorded for the admission. |
| `diagnosis_en` | The authors' English translation of those diagnoses. |
| `outcome_pt` | The outcome of the admission. |
| `outcome_en` | The authors' English translation of the outcome. |
| `length_of_stay` | The total length of the admission. |
| `specialties` | The number of medical specialties consulted. |
| `icu` | Whether the admission included intensive care. |
| `palliative_care` | Whether the patient was under palliative care. |

The five clinical columns are reproduced exactly as the workbook records them,
which means they are not clean. They carry the authors' own annotation marks
and their own missing-value markers, and they are left untouched here rather
than tidied, because a reader who wants the authors' data should get the
authors' data.

Anyone computing from those five columns therefore has to establish what the
annotations mean first. The workbook itself does not say, but the paper cited
above defines the notation used in the structured columns, and the notebook
included in the deposit shows how the authors treated the missing values. Both
are worth reading before the columns are used for anything.

## How These Files Were Prepared

The workbook `anotated_dataset_v2.xlsx` was downloaded from the DOI above and
converted to the three CSV files listed. Its MD5 checksum is
`e6bd34e33d79b768d7c745b9f50440d3` and its SHA-256 checksum is
`ccc9c416747478503d4036a2e708104fc52d605ce4b00233d5078074e1cb0053`, which is
what the conversion was run against.

Four changes were made, and no other.

The three sheets became three files. The sheet named `annotated_dataset` became
`discharge_summaries.csv`, `abbreviations` became `abbreviations.csv`, and
`ICD Codes` became `icd_codes.csv`.

The column headings were renamed. The workbook's headings include several
misspellings, among them `lenght of stay` and `translanted outcome`, and a
heading that names a Portuguese abbreviation rather than what the column holds,
which is `uti (intensive care unit)`. The names in the table above replace them.
No cell value was altered by the renaming.

A row number was added, being the `record_id` column, because the workbook
identifies its rows only by position and the day's notebooks need a stable name
for a record.

Empty trailing rows were dropped, along with the title row and the heading row
that sit above the data in the `ICD Codes` sheet.

Nothing was translated, corrected, cleaned, de-duplicated, or reordered. No
summary was shortened. The row order is the workbook's own.

## Network Access

The notebooks in this day read every data file from this directory, so no data
arrives over the network. The notebooks do reach the network for something
else, which is the pre-trained models they download from the Hugging Face Hub.
The day's `README.md` records which models, at which revisions, and how large
they are.

## Files The Notebooks Write

Neither notebook writes a file. No model, checkpoint, embedding, or cached
tokenisation is stored in this repository, and everything the notebooks compute
lives in memory until the kernel stops.
