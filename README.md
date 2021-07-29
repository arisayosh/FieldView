# Topic Modeling PubMed's Articles Using LDA and BERT


This repository contains the jupyter notebooks and requirements used for my project on topic modeling PubMed's 9000+ articles about 'stem cell therapies'. The notebooks are numbered in the order they have been used. 


### 0_WebScraping_PubMed.ipynb


I used Selenium with Chrome Driver and Beautiful Soup to scrape 1000 search result pages on PubMed for the search term 'stem cell therapy'. The resulting dataframe contained 9926 rows and 12 columns, each columns holding information about an article that a user can find in PubMed in the order of relevance (deemed by PubMed):

- `article_id`: PubMed ID for the article
- `title`: article's title
- `publication_type`: the type of publication
- `abstract`: the article's abstract
- `journal_title`: the title of the journal the article was published in
- `citation`: citation key
- `n_authors`: number of authors
- `affiliations`: author affiliations (universities, company, country, etc)
- `n_affiliations`: the number of affiliations associated with the article
- `n_citations`: the number of times the publication was cited
- `keywords`: keywords linked to publication by PubMed
- `n_references`: the number of references used in the publication


### 1_InitialCleaningEDA.ipynb


This was my first look at the dataset. I removed duplicated rows, extracted certain features, reformatted the text data, and imputed missing data. Here I took a look at the change in the number of publications and keywords throughout the years. 


### 2_FurtherEDAClassification.ipynb


To further the data exploration, I decided to fit classification models to the dataset to predict the 'influence' of a publication based on the number of citations. I used Scikit-Learn's extensive library to perform multiple grid search pipelines for feature engineering, hyper parameter optimization, model selection and evaluation. 


### 3_TopicModeling_LDA.ipynb


I used Scikit-Learn's Latent Dirichlet Allocation (LDA) model to begin Topic Modeling with my dataset. For this, I preprocessed the data from scratch, extracting only the titles and abstracts, transforming them into lowercase, and removing punctuations. Using TF-IDF, I vectorized the resulting text data and fitted the LDA model to generate 10 topics. Based on the results, I optimized the topic extraction by adjusting the parameters for the vectorization, adding stop words and stemming the words. 


### 4_TopicModeling_BERT.ipynb (Google Colab)


Heavily influenced by Maarten Grootendorst's [work](https://maartengr.github.io/BERTopic/index.html), I used BERT for my Topic Model. For this task, I used Google Colab as it allowed me to use the GPU for model fitting. I leveraged [allenai-specter](https://huggingface.co/allenai/specter), a sentence transformer pre-trained on 146K Semantic Scholar query results that learned document relatedness based on citation graphs. The dimension of the resulting embeddings were reduced using UMAP and clustered by HBDSCAN into topics. Then the entire text data from each topic was vectorized to extract the top 10 most important words within the topic. The model resulted in ~50 various topics. I performed the same task in a few lines using BERTopic, Maarten Grootendorst's specialized package for Topic Modeling with BERT. 


### 5_ModelEvaluations.ipynb


In this final notebook, I attempted to evaluate the Topic Models based on the resulting topics from LDA and BERTopic. I looked at the similartiy of documents in each topic by calculating the average number of unique keywords in a sample of 100 articles. Finally I did a manual check on the sensibility of some of the common topics from both models by looking at the top 5 most cited publications in these topics.


### Requirements.txt


This file contains all of the libraries used throughout this project and can be used to create an environment using:


`$ conda create --name <env> --file <this file>` 


### Data files


All of the data files generated and used in this repository can be found [here](https://drive.google.com/drive/folders/1VLU09gOTQHR48h4kmPOfvEc4wQrrf4f4?usp=sharing). If following this repository froms start to finish, it is not strictly necessary to download these files. However, certain files will be required if you wish to skip ahead to a specific part of the project.
