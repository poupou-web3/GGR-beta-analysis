# GGR-beta-analysis
Analysis of Allo beta rounds run in April 2023

The goal of the analysis is to flag projects submitted in the allo protocol that may be fraudulent.
In that repository, we explore the project description to automatically flag projects that may be fraudulent.
A manual review is then performed to confirm the flagging.
The final list with the detailed analysis is available in the file beta-flagged-grants.xlsx



## Data
The data used was provided by the OpenData Community the details are here: [hackathon_data_faq.md](https://github.com/OpenDataforWeb3/Resources/blob/main/docs/hackathon_data_faq.md)

The two files used are 
- [all-rounds.csv](https://ipfs.io/ipfs/QmVhLowGhiPBd2VAk2JQdZ9U9RoTUUKtJSokv2yEDM5hoG?filename=all_rounds.csv)
- [Beta-applicants-projects.csv](https://ipfs.io/ipfs/QmYhkts3SkESdnwA1gjiKQDuTCtWnQyDQtiJhQ8BBpPGem?filename=beta_projects.csv)

## Analysis

The analysis was performed in a jupyter notebook in Python.

The notebook is available here: Beta-Grant-Analysis.ipynb

### Flagging algorithm
#### 1. Low Description length
If the description length is less than 100 characters the project is flagged as suspicious.
#### 2. Low Readability score
The readability scores are computed using the Python library [readability](https://pypi.org/project/readability/).
Then using the distance to the mean value of the readability for each readability metric we compute a boolean if more than 2 readability metrics are more than 2 standard deviations away from the mean.
#### 3. Low Originality and AI score
The originality and ai scores are computed using the [originality.ai](https://www.originality.ai/) API.
The originality API is a paid API that rated if a text was written by a human or an AI.

### Final flag
The final flag is triggered if any flag is triggered.

## Output
The CSV file flagged_grants.csv contains the list of grants that were flagged by the algorithm.
The CSV file grants_and_scores.csv is the raw file containing all grant data the scores and the boolean.

## How to run the analysis
Requirements: Python 3.10 or higher

1. Clone the repository
2. Install the requirements
`pip install -r requirements.txt`
3. Create a .env file with the following variables
```ORIGINALITY_API_KEY='<you originality ai API KEY>```
    This calls a paid API.
4. Put the data files in the data folder following the hierarchy below
5. Run the notebook Beta-Grant-Analysis.ipynb

## Tree
```
C:.
├───data
│   └───all-rounds.csv
│   └───Beta-applicants-projects.csv
├───GGR-beta-analysis
    └───jupyter
        └───Beta-Grant-Analysis.ipynb
```