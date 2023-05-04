# Allo Protocol Beta Rounds Analysis
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

The notebook is available here: [Beta-Grant-Analysis.ipynb](https://github.com/poupou-web3/GGR-beta-analysis/blob/main/jupyter/Beta-Grant-Analysis.ipynb)

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
The CSV file [flagged_grants.csv](https://github.com/poupou-web3/GGR-beta-analysis/blob/main/flagged_grants.csv) contains the list of grants that were flagged by the algorithm.

The CSV file [grants_and_scores.csv](https://github.com/poupou-web3/GGR-beta-analysis/blob/main/grants_and_scores.csv) is the raw file containing all grant data the scores and the boolean.

The Excel file [beta-flagged-grants-analysis.xlsx](https://github.com/poupou-web3/GGR-beta-analysis/blob/main/beta-flagged-grants-analysis.xlsx) contains the list of flagged grants with the detailed manual analysis.
The analysis was a manual review trying to understand if the grant was fraudulent or not. This process was done by a single person and is not perfect and very subjective.

## Conclusion
The projects flagged as suspicious or Sybil from the flagged project is subjective. Nonetheless, a large number of projects extracted by the originality and ai boolean look fraudulent or suspiciously fraudulent. The drawback of that method is that it requires to pay for the API. It cost me $20 to run on all beta rounds. An interesting test for a future analysis would be to run the analysis on the alpha round to see if the flagged projects were indeed fraudulent or rejected by manual review from Gitcoin. The other flags tend to flag many projects. Yet having a low description length or a low readability score does not mean that the project is fraudulent. It may be a good indicator to prioritize the manual review and should probably be completed by other indicators.

## Other ideas to facilitate the grant reviewing process
A manual review will always be required to accept grants that need funds and that are safe for the community.
From reviewing around 100 projects manually, I listed the following legos that could be built to facilitate the process using only application data.

- website
    - latest article
    - activity
    - functional
    - Fork?
    - does it match the description?
    - When was it published?
    - Is the person on Twitter matching the person on the website
- Twitter
    - how many followers
    - What's the growth of the followers
    - How old is the account?
    - Is it active in the last month and before?
    - Is it showing interest in the grant round and bragging about it?
    - Is it relayed by other relevant accounts (for example eth lima retweeting a project grant in Latino America)*
    - Is there an official Twitter account with a similar name?
- GitHub
    - is the repository active
    - how many people contribute to the project?
    - How active is the person behind the account
    - How big is the repo
- Then is the project impersonating another person?
    - look at the address
    - brag on Twitter about it as the official account?


## How to run the analysis
Requirements: Python 3.10 or higher

1. Clone the repository
2. Install the requirements
`pip install -r requirements.txt`
3. Create a .env file with the following variables
```ORIGINALITY_API_KEY='<you originality ai API KEY>```
    This calls a paid API.
4. Put the data files in the data folder following the hierarchy below
5. Run the notebook [Beta-Grant-Analysis.ipynb](https://github.com/poupou-web3/GGR-beta-analysis/blob/main/jupyter/Beta-Grant-Analysis.ipynb)

## Tree structure of the repository
```
C:.
├───data
│   └───all-rounds.csv
│   └───Beta-applicants-projects.csv
├───GGR-beta-analysis
    └───jupyter
        └───Beta-Grant-Analysis.ipynb
```
