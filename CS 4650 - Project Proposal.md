Improving Resume–Job Matching with Text Embeddings
## Aniya Pauling, Huang Tian, Andre Koga, Kishan Patel

## 1. Problem Description
Finding relevant job postings is a time-intensive task for job seekers, who must manually sift
through hundreds of listings to find roles that match their background. We address this by
building an automatic resume-to-job ranking system: given a candidate's resume, the system
scores and ranks a pool of job descriptions by compatibility — without any human input.
This mirrors real-world job recommendation platforms such as LinkedIn's "Jobs you may be
interested in." The core research question is whether dense semantic text embeddings (SBERT)
produce meaningfully better job rankings than sparse keyword-based similarity (TF-IDF).
Keyword methods break down when a resume and job description use different but equivalent
terminology. For example, a resume listing "statistical modeling" may not score well against a
job requiring "data analysis," despite significant skill overlap. We hypothesize that sentence-level
embeddings capture this semantic equivalence more effectively.

## 2. Dataset
We will use the 0xnbk/resume-ats-score-v1-en dataset from Hugging Face. It contains 6,370
resume-job description pairs, each annotated with a continuous ATS compatibility score ranging
from 0 to 100, alongside a 3-class label (Fit / Partial Fit / No Fit). The dataset is pre-split into
5,100 training rows and 1,270 validation rows. Each row stores the resume and job description in
a single "text" field separated by a SEP token.
Why this dataset?
- Continuous ATS scores (0–100) provide fine-grained ground truth for ranking, making
evaluation metrics such as NDCG more meaningful than coarse 3-class labels alone.
- The dataset is explicitly designed for training and evaluating sentence transformers on
resume-job semantic similarity.
- Pre-split train/validation sets allow consistent, reproducible evaluation.

## 3. Baseline Method
Our primary baseline is TF-IDF cosine similarity. After parsing the SEP-separated text, each
resume and job description is represented as a sparse TF-IDF vector over a shared vocabulary.
For each resume in the validation set, all associated job descriptions are scored by cosine


similarity and ranked. We will additionally implement a Naive Bag-of-Words (NBOW) classifier
as a secondary baseline.

## 4. Proposed Method
We plan to improve the baseline method by using SBERT to generate sentence embeddings of
the dataset texts. Each resume will be turned into a vector representation and cosine similarity
will be used to measure how well the resumes and job descriptions match. Based on the
similarity scores, job descriptions will be ranked for each resume. Then, we will compare the
results of this approach with the TF-IDF baseline method.

## 5. Evaluation Plan
To evaluate our model, we will compare the ranking performance of the TF-IDF baseline method
and the SBERT model on a test dataset. Top-k accuracy will be used to measure whether the
correct job appears within the top k results, and Mean Reciprocal Rank (MRR) will measure how
high the correct matches are ranked. We will also examine the results of correct and incorrect job
matches to better understand how the model performed.

## 6. Expected Contribution
The goal of this project is to show that semantic embeddings can improve resume–job matching
compared to the usual keyword-based methods. We expect that transformer-based models will
capture contextual meaning in text better than other models. We will also highlight the strengths
and limitations of using automated systems for resume matching.