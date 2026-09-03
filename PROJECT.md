# Final Projects

The final project is the part of the workshop that nobody walks you through. A
group picks a question, finds data that can answer it, builds something that
runs, and explains on the last morning what the result means and where it
cannot be trusted. The sessions before it supply the techniques, so the project
is where the judgement is added.

## The Shape Of A Project

- Groups build on Tuesday, September 8, 2026, and present on Wednesday,
  September 9, 2026, at 10:00. That is one working session and one morning, so
  the scope has to be small enough to finish and still leave time to prepare
  the presentation.
- Work in groups of three or four. Split the work so that two people are never
  blocked waiting for the third.
- Every project should draw on at least two of the days. A project that only
  fits a single day is usually a laboratory exercise rather than a project.
- Stay inside the packages the environment already provides, which are the ones
  listed in the `setup/` directory. Installing a new framework costs an hour
  that the project does not have.

## What To Hand In

- A repository or a directory containing the notebooks, the scripts, and a
  `README.md`.
- A `data/README.md` that says where every file came from and how it is
  licensed, in the same form the day directories use. Store the data itself
  only if the licence allows it, and otherwise store the script that fetches
  it.
- A notebook that runs from a clean kernel to the end. A result that only
  exists in a screenshot is not a result.
- A presentation of about ten minutes, followed by questions.

## What The Committee Looks For

- The question is stated before the model is chosen, and the model is chosen
  because it answers that question.
- The evaluation matches the question. A split that leaks time, a patient, or a
  sensor across the training and the test sets makes every number in the
  presentation meaningless, and saying so yourself is worth more than a high
  score.
- A baseline is present, and the model is compared against it. Predicting the
  mean, predicting the previous value, or predicting the majority class is
  usually enough of a baseline.
- The failure cases are shown as well as the successes.
- The limits of the data are stated. Who is missing from it, what it does not
  measure, and what conclusion it therefore cannot support.

## Choosing Data

Every suggestion below names a dataset whose licence is open, and each licence
is written next to it. Two rules govern the choice.

- Read the licence yourself before you download anything, because a licence can
  change and a copy of a dataset can carry different terms from the original.
  This is common where an aggregate is built out of parts that were licensed
  separately, and the aggregate then states a single licence that never covered
  the parts.
- Record the licence, the source, and the date you fetched the data in your
  `data/README.md`, along with any transformation you applied. A reader who has
  your repository and nothing else should be able to rebuild your inputs.

Data that requires a signed agreement, a credentialed account, or a
non-redistribution clause is best avoided for a project of this length, because
the paperwork outlasts the workshop.

## Project 1: Air Quality Nowcasting For A City

- **Days it builds on:** Day 2 and Day 6.
- **The question:** given the readings of a network of low cost sensors up to
  this hour, what will the city average be over the next six hours, and how
  wrong is that forecast likely to be?
- **The data:** the Sensor.Community archive at
  `https://archive.sensor.community/`, which publishes one file per sensor per
  day. The laboratory exercise on Day 2 uses eight Skopje sensors for January
  2024, and a project can take a longer period, a different city, or both.
  Weather is the natural second source, and the Open-Meteo historical archive
  at `https://open-meteo.com/` provides temperature, wind, and humidity for any
  coordinate.
- **The licences:** Open Data Commons Database Contents License 1.0 for
  Sensor.Community, and Creative Commons Attribution 4.0 International for
  Open-Meteo, whose free tier is restricted to non-commercial use, which a
  workshop project is.
- **What makes it hard:** the sensors disagree with each other, some of them
  are indoors, and the network changes membership from hour to hour. A forecast
  built on a city average has to define that average first, and the definition
  changes the answer.
- **A finished project:** an hourly series built from raw sensor files, a
  forecast at several horizons, a comparison against the persistence baseline,
  and an honest statement of how far ahead the model is still useful.
- **If there is time:** predict the probability of exceeding a threshold rather
  than the concentration, since that is what a public alert actually needs.

## Project 2: Land Cover From Satellite Patches

- **Days it builds on:** Day 3.
- **The question:** how well can a convolutional network name the land cover in
  a small satellite image, and what does it confuse?
- **The data:** EuroSAT, which is 27000 labelled Sentinel-2 patches in ten
  classes, published at `https://zenodo.org/records/7711810`. The RGB archive
  is 94.7 MB and the thirteen band archive is 2.1 GB, so the RGB version is the
  sensible starting point.
- **The licence:** MIT for the dataset, with the underlying Sentinel data open
  under European Union law.
- **What makes it hard:** several classes are genuinely similar, and the
  interesting part of the work is the confusion matrix rather than the
  accuracy. Patches from the same region resemble each other, so a random split
  flatters the model.
- **A finished project:** a trained classifier, a confusion matrix that is
  discussed rather than displayed, and a set of misclassified patches shown to
  the audience.
- **If there is time:** compare a small network trained from scratch against a
  pretrained backbone, and report the cost of each in training time as well as
  in accuracy.

## Project 3: Skin Lesion Triage And Its Honest Evaluation

- **Days it builds on:** Day 3.
- **The question:** can a classifier separate the lesion types in dermatoscopic
  images well enough to be worth showing a clinician, and what happens to the
  rare classes?
- **The data:** HAM10000, which is 10015 dermatoscopic images in seven
  diagnostic classes, published on Harvard Dataverse under the identifier
  `doi:10.7910/DVN/DBW86T`.
- **The licence:** Creative Commons Attribution Non-Commercial 4.0
  International. The dataset is for non-commercial use, a derived version must
  carry the same licence, and the terms have to be accepted before the files
  can be downloaded.
- **What makes it hard:** the classes are severely imbalanced, and the majority
  class alone gives an accuracy that looks respectable and means nothing. The
  dataset also contains several images of the same lesion, so a split that
  ignores the lesion identifier puts the same lesion on both sides of it.
- **A finished project:** a classifier evaluated per class, a split that keeps
  a lesion whole, and a clear statement of which classes the model cannot
  detect.
- **If there is time:** turn the classifier into a triage tool by letting it
  abstain, and measure how much accuracy the remaining decisions gain for each
  percentage point of cases handed back to a human.

## Project 4: Intent Routing For A Helpdesk

- **Days it builds on:** Day 4 and Day 5.
- **The question:** can a fine-tuned encoder route a customer message to the
  right queue, and can it recognise a message that belongs to no queue at all?
- **The data:** BANKING77, which is 13083 customer service queries labelled
  with 77 fine-grained banking intents, at
  `https://huggingface.co/datasets/PolyAI/banking77`. The out-of-scope part of
  the question needs a second source, and CLINC150 at
  `https://huggingface.co/datasets/clinc/clinc_oos` supplies 150 intents across
  ten domains together with an explicit out-of-scope label.
- **The licences:** Creative Commons Attribution 4.0 International for
  BANKING77, and Creative Commons Attribution 3.0 for CLINC150.
- **What makes it hard:** the 77 intents overlap, so the mistakes cluster in a
  few confusable groups rather than spreading evenly. Rejecting an unknown
  message is a different problem from classifying a known one, and a softmax
  that has never seen an unknown message is confident about all of them.
- **A finished project:** a fine-tuned classifier, a rejection rule with a
  threshold chosen on validation data rather than on the test set, and a report
  of what each choice of threshold costs.
- **If there is time:** put a language model behind the rejection rule, so that
  a message the classifier refuses is answered rather than dropped, and compare
  the two paths on the same messages.

## Project 5: Complaint Triage And Summarisation

- **Days it builds on:** Day 2, Day 4, and Day 5.
- **The question:** given a free text consumer complaint, can the product and
  the issue be predicted, and can a useful one paragraph summary be produced
  for a case worker?
- **The data:** the Consumer Complaint Database of the United States Consumer
  Financial Protection Bureau, at
  `https://www.consumerfinance.gov/data-research/consumer-complaints/`, which
  offers a full download and an API. Complaints carry a product, an issue, a
  company response, and, where the consumer consented, a narrative with
  personal information removed.
- **The licence:** the database is published by a United States federal agency
  as open government data and is free for anyone to use, analyse, and build on.
- **What makes it hard:** the export is large, the narratives exist for only a
  minority of complaints, and the label taxonomy has changed over the years, so
  a model trained across the whole history learns the taxonomy as much as the
  text. Summaries need an evaluation, and inventing one is part of the work.
- **A finished project:** a filtered subset defined by an explicit rule, a
  classifier over the narratives, and a summariser whose output is judged
  against a small set of examples read by hand.
- **If there is time:** measure how often the summariser states something the
  complaint does not say, since that is the failure that matters.

## Project 6: Data Quality On An Open Food Database

- **Days it builds on:** Day 1, Day 2, and optionally Day 3.
- **The question:** which nutrition facts in a crowdsourced product database
  are wrong, and can the missing ones be predicted well enough to be filled?
- **The data:** Open Food Facts at `https://world.openfoodfacts.org/data`,
  which publishes the whole database as a MongoDB dump, as compressed JSONL, as
  Parquet on Hugging Face, and as CSV through the search interface. Product
  photographs are available too.
- **The licences:** the Open Database License for the database, the Database
  Contents License for the individual records, and Creative Commons
  Attribution-ShareAlike for the photographs.
- **What makes it hard:** the data is entered by volunteers, so units are
  mixed, quantities are written in free text, and a small number of records
  claim impossible values such as more than 100 grams of fat in 100 grams of
  product. Finding those is the interesting half, and the arithmetic between
  the nutrients gives you a check that does not need a model.
- **A finished project:** a set of validation rules with the number of records
  each one rejects, a model that predicts one nutrient from the others, and a
  comparison of the model against the rules on records that are known to be
  wrong.
- **If there is time:** classify a product category from its photograph, and
  check whether the categories the image model confuses are the ones the
  nutrition values also confuse.

## Project 7: Household Electricity Demand

- **Days it builds on:** Day 2 and Day 6.
- **The question:** how far ahead can the electricity demand of a single
  household be forecast, and how much of the forecast is simply the time of
  day?
- **The data:** the individual household electric power consumption dataset at
  `https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption`,
  which is 2075259 minute-level measurements taken between December 2006 and
  November 2010, with global active power, voltage, intensity, and three
  submeters. About 1.25 percent of the readings are missing.
- **The licence:** Creative Commons Attribution 4.0 International.
- **What makes it hard:** the series is dominated by a daily and a weekly
  cycle, so a model that captures nothing else still looks accurate. Separating
  what the calendar explains from what the model adds is the whole exercise,
  and the gaps have to be handled without inventing demand.
- **A finished project:** an aggregation to a sensible resolution, a seasonal
  baseline, a model that beats it, and an evaluation that respects the order of
  time.
- **If there is time:** forecast the submeters separately and check whether the
  sum of the three forecasts beats a single forecast of the total.

## Project 8: Hospital Readmission Within Thirty Days

- **Days it builds on:** Day 1 and Day 2.
- **The question:** which diabetic inpatients are readmitted within thirty
  days, and is a model that predicts it fit to influence a discharge decision?
- **The data:** the diabetes dataset covering 130 United States hospitals for
  the years 1999 to 2008, at
  `https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008`,
  which is 101766 encounters described by 47 features.
- **The licence:** Creative Commons Attribution 4.0 International.
- **What makes it hard:** a patient can appear several times, so a random split
  puts the same person on both sides of it. Several columns are almost entirely
  missing, some codes are administrative rather than clinical, and the positive
  class is small enough that accuracy is the wrong measure.
- **A finished project:** a split grouped by patient, a model with calibrated
  probabilities, a threshold justified by the cost of each kind of error, and a
  comparison of performance across patient groups.
- **If there is time:** examine what the model relies on, and say plainly which
  of those features a hospital could act on and which merely describe how the
  hospital already behaved.

## Project 9: A Question Answering Agent Over An Open Corpus

- **Days it builds on:** Day 4 and Day 5.
- **The question:** can an agent answer questions over a document collection
  and cite the passage it used, and how often does it answer from nothing?
- **The data:** any corpus with an open licence. A subset of a Wikipedia dump
  from `https://dumps.wikimedia.org/` works well, and its text is licensed
  under Creative Commons Attribution-ShareAlike 4.0 International together with
  the GNU Free Documentation License. A structured alternative is to load an
  extract of one of the datasets above into SQLite and let the agent query it
  with the tool-calling pattern from Day 5.
- **The licence:** as stated for the corpus you choose, and recorded in your
  `data/README.md`.
- **What makes it hard:** the retrieval decides the answer, so a project that
  spends all of its time on prompts and none on retrieval will produce
  confident nonsense. Questions have to be written before the system is built,
  otherwise the evaluation is a demonstration.
- **A finished project:** a set of at least thirty questions with known
  answers, a retrieval step that is measured on its own, an agent that cites
  its sources, and a count of the answers that were unsupported.
- **If there is time:** add questions the corpus cannot answer, and measure how
  often the agent says so instead of inventing something.

## Project 10: Targeting A Marketing Campaign Under A Cost Model

- **Days it builds on:** Day 1 and Day 2.
- **The question:** which customers should a bank telephone about a term
  deposit, given that a call costs money and a subscription earns it?
- **The data:** the bank marketing dataset at
  `https://archive.ics.uci.edu/dataset/222/bank+marketing`, which records the
  telephone campaigns of a Portuguese bank, describing each contact by customer
  attributes, the history of previous contacts, and whether the deposit was
  taken.
- **The licence:** Creative Commons Attribution 4.0 International.
- **What makes it hard:** the duration of the call is the strongest column in
  the table and it is known only after the call has happened, so a model that
  uses it scores well and cannot be deployed. The campaigns also ran in a
  sequence, so a random split lets the model learn from the future.
- **A finished project:** a model trained without the columns that leak, a
  threshold chosen from an explicit cost per call and value per subscription,
  and a statement of how many calls the model saves at the same number of
  subscriptions.
- **If there is time:** show how the recommended threshold moves as the assumed
  cost changes, so that the decision can be made by somebody who knows the real
  numbers.

## Project 11: Intent Understanding Across Languages

- **Days it builds on:** Day 4.
- **The question:** how much accuracy does a multilingual model lose on a
  language it saw little of during pretraining, and does training on one
  language transfer to another?
- **The data:** MASSIVE at `https://huggingface.co/datasets/AmazonScience/massive`,
  which holds parallel virtual assistant utterances labelled with 60 intents
  across more than fifty language variants, amounting to roughly 843000 rows in
  total. Check which locales are present before you build a plan around a
  particular language, because the list does not cover every European language.
- **The licence:** Creative Commons Attribution 4.0 International.
- **What makes it hard:** the utterances are parallel across languages, so the
  comparison between languages is fair and any gap is genuinely the model
  rather than the data. Fine-tuning on all languages at once is not obviously
  better than fine-tuning on one, and finding out which is the project.
- **A finished project:** a per-language accuracy table for at least four
  languages, a zero-shot transfer result from one language to another, and an
  explanation of which intents survive the transfer and which collapse.
- **If there is time:** compare the multilingual encoder against translating
  into English first and using an English model, and count the cost of each in
  time as well as in accuracy.

## Project 12: Demand And Customer Value For An Online Retailer

- **Days it builds on:** Day 2 and Day 6.
- **The question:** how much of each product will sell next week, and which
  customers are worth keeping?
- **The data:** Online Retail II at
  `https://archive.ics.uci.edu/dataset/502/online+retail+ii`, which is 1067371
  transaction lines from a United Kingdom gift retailer between 1 December 2009
  and 9 December 2011, with an invoice number, a stock code, a description, a
  quantity, a date, a unit price, a customer identifier, and a country.
- **The licence:** Creative Commons Attribution 4.0 International.
- **What makes it hard:** cancellations appear as negative quantities and have
  to be matched against the invoices they cancel, a large share of the revenue
  comes from a handful of wholesale customers, and many lines carry no customer
  identifier at all. Every one of those decisions changes the forecast, so the
  cleaning rules are the result as much as the model is.
- **A finished project:** a weekly series per product built from documented
  cleaning rules, a forecast for the top products measured against a seasonal
  baseline, and a customer segmentation that is described in business terms
  rather than cluster numbers.
- **If there is time:** check whether the segments predict anything about the
  following quarter, since a segmentation that does not is only a description
  of the past.

## Project 13: Segmenting An Object And Measuring It

- **Days it builds on:** Day 3.
- **The question:** how accurately can a model outline an object in a
  photograph, and how does the error in the outline translate into an error in
  the measured area?
- **The data:** the Oxford-IIIT Pet dataset at
  `https://www.robots.ox.ac.uk/~vgg/data/pets/`, which is about 800 MB holding
  roughly 200 images for each of 37 breeds, annotated with the breed, a
  bounding box around the head, and a pixel level foreground and background
  segmentation.
- **The licence:** Creative Commons Attribution-ShareAlike 4.0 International,
  with the copyright in the photographs remaining with their owners.
- **What makes it hard:** pixel accuracy rewards a model that labels everything
  as background, so the metric has to be chosen before the model is trained.
  Area measured in pixels depends on how close the camera was, which means the
  measurement is only comparable between images under an assumption you have to
  state.
- **A finished project:** a segmentation model, an evaluation by intersection
  over union as well as by pixel accuracy, and a plot of measured area against
  true area with the outliers examined.
- **If there is time:** measure how much of the segmentation quality survives
  when the image is blurred, darkened, or reduced in resolution, since that is
  what separates a demonstration from a tool.

## Project 14: An Agent That Writes SQL, Evaluated Properly

- **Days it builds on:** Day 4 and Day 5.
- **The question:** how often does a language model turn a question into SQL
  that returns the right answer on a database it has never seen?
- **The data:** Spider at `https://yale-lily.github.io/spider`, which is 10181
  questions paired with 5693 SQL queries over 200 databases drawn from 138
  domains, with the databases themselves included so that a query can be run.
- **The licence:** Creative Commons Attribution-ShareAlike 4.0 International.
- **What makes it hard:** two different queries can be equally correct, so
  comparing the generated text against the reference punishes correct answers,
  and comparing the returned rows instead needs care with ordering and with
  empty results. A schema that does not fit in the prompt has to be selected
  down before the model sees it, and how you select is a large part of the
  score.
- **A finished project:** an agent that inspects the schema before answering,
  an evaluation by execution on a fixed sample of the development set, and a
  breakdown of the failures by cause rather than a single percentage.
- **If there is time:** let the agent run its query, read the error, and try
  again, then measure how many failures that recovers and how many extra calls
  it costs.

## Project 15: Multi-Label Emotion In Short Text

- **Days it builds on:** Day 4 and Day 5.
- **The question:** can a model assign several emotion labels to a short
  comment at once, and what does it do with the rare emotions?
- **The data:** GoEmotions at
  `https://huggingface.co/datasets/google-research-datasets/go_emotions`, which
  is about 58000 curated Reddit comments labelled with 27 emotions and a
  neutral category, where a comment may carry more than one label. The raw
  release keeps the individual annotators, so disagreement between them can be
  studied rather than averaged away.
- **The licence:** Apache License 2.0.
- **What makes it hard:** a multi-label problem needs one threshold per label
  rather than a single argmax, the rare emotions have few examples and are the
  ones a demonstration always shows, and the annotators genuinely disagree
  about several categories, which puts a ceiling on the achievable score.
- **A finished project:** a fine-tuned classifier with per-label thresholds
  chosen on validation data, a macro averaged score reported alongside the
  micro averaged one, and an analysis of the labels the model cannot learn.
- **If there is time:** estimate the human ceiling from the annotator
  agreement in the raw release, and compare the model against it rather than
  against a perfect score.

## The Data At A Glance

| Project | Dataset | Licence |
| --- | --- | --- |
| 1 | Sensor.Community archive. | Open Data Commons Database Contents License 1.0. |
| 1 | Open-Meteo historical weather. | Creative Commons Attribution 4.0 International. |
| 2 | EuroSAT. | MIT. |
| 3 | HAM10000. | Creative Commons Attribution Non-Commercial 4.0 International. |
| 4 | BANKING77. | Creative Commons Attribution 4.0 International. |
| 4 | CLINC150. | Creative Commons Attribution 3.0. |
| 5 | Consumer Complaint Database. | United States open government data. |
| 6 | Open Food Facts. | Open Database License, with Database Contents License for the records and Creative Commons Attribution-ShareAlike for the photographs. |
| 7 | Individual household electric power consumption. | Creative Commons Attribution 4.0 International. |
| 8 | Diabetes across 130 United States hospitals. | Creative Commons Attribution 4.0 International. |
| 9 | Wikipedia dumps. | Creative Commons Attribution-ShareAlike 4.0 International, and the GNU Free Documentation License. |
| 10 | Bank marketing. | Creative Commons Attribution 4.0 International. |
| 11 | MASSIVE. | Creative Commons Attribution 4.0 International. |
| 12 | Online Retail II. | Creative Commons Attribution 4.0 International. |
| 13 | Oxford-IIIT Pet. | Creative Commons Attribution-ShareAlike 4.0 International. |
| 14 | Spider. | Creative Commons Attribution-ShareAlike 4.0 International. |
| 15 | GoEmotions. | Apache License 2.0. |

## Bringing Your Own Topic

A group is welcome to propose something else, and the best projects usually
come from a question somebody already had. Bring three things to the proposal,
which are the question you want answered, the data that can answer it with its
licence, and the baseline you expect to beat. If the data cannot be obtained
and read within the first hour, choose a different question, because a project
that spends its only working day on downloads has nothing to present.
