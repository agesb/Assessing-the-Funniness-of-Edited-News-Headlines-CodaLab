# Assessing-the-Funniness-of-Edited-News-Headlines-CodaLab
Group NLP Coursework, Spring 2020

Entry for Task 1 of CodaLab's "Assessing the Funniness of Edited News Headlines" challenge

In this repo, we share our experiments to analyse and predict the funniness of news headlines. 
As of May 2021, our best-performing algorithm ranks 2nd on CodaLab's leaderboard (entry name "sn914")

https://competitions.codalab.org/competitions/20970#results

Team members:


- Hanna Behnke
- Jamie Salter
- Sneha Naik

The report details our experimental methods, results and conclusions.

The notebook is structured into the following 6 sections and is self-contained:

- Setup
- Data Exploration
- Shared Functions
- Approach 1 (using pre-trained embeddings / models)
- Approach 2 (without pre-trained embeddings / models)
- Additional Experiments

We will describe each of them in turn.

---

**Setup**

We import all required libraries, check for a GPU for PyTorch and import 5 different datasets:
- **Training dataset:** used for W2V and regression model training
- **Validation dataset:** used for hyperparameter tuning
- **Test dataset:** used for final tests, remains untouched during hyperparameter tuning
- **Funlines dataset:** additional training data which has the same structure as the training data (*Source: https://www.cs.rochester.edu/u/nhossain/funlines.html*)
- **News Category dataset:** ca. 200k headlines with a broad range of topics, used to train a more comprehensive W2V model (*Source: https://www.kaggle.com/rmisra/news-category-dataset*)


---

**Data Exploration**

We explore our datasets to get a better understanding of the problem at hand as well as the data distribution. We exclude headlines with a particularly high standard deviation of the votes from our training set. 

---

**Shared Functions**

This section includes a set of training and evaluation methods which are used both for approach 1 and 2. All cells have to be excecuted to re-run the regression experiments. 

---

**Approach 1**

In this section we implement and run a BiLSTM and Transformer model.  To replicate results, run all cells in the "Setup" and "Shared functions" section described above.

For the BiLSTM, run all cells in "Model 1: BiLSTM" and for a transformer run all cells in "Model 2: Transformer".  Hyperparameters have already been chosen, but to modify them to trial a particular set of parameters use the penultimate cell in each subsection.  A description of each hyperparameter is described in each cell.

---

**Approach 2**

For approach 2, we first implemented a flexible data pre-processing pipeline. Next, we experimented with Bag of Words which yielded mediocre results on the regression task. Thus, we trained two Word2Vec models, one on the original training corpus and one on an augmented dataset (209k headlines). We then trained several Scikit-learn models and one LSTM based on the W2V models. 

Please ensure that the sections "Setup" and "Shared Functions" are executed before running all the cells in Approach 2 to ensure all required functions and datasets are loaded. Approach 2 is largely self-contained, however, to run the LSTM, it is necessary to initialise the class BiLSTM(nn.Module) in the Section "Approach 1, Model 1: BiLSTM".

---

**Additional Experiments**

This section includes experiments which we did not include in our final training approaches.
1. Manual byte pair encoding – turned out to be too computationally complex and difficult to retrieve useful tokens. We used FastText instead.
2. Manual word embedding training – too slow, we used Gensim's functions instead.
