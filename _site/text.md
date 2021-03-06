## Abstract 

It is common knowledge that women’ speech contains more uncertainties (e.g., “We think this may be correct”) compared to men (e.g., “I know it is correct”). As a result, this project aims at comparing speech behaviours related to uncertainty between genders. For our data, we use citations from _Quotebank_, an open corpus of more than 1 million quotations from 2015 to 2020, as well as the open-source information from wikidata to have access to the speakers' information. The classification of the quotes is done using an uncertainty detection classifier, based on the statistical analysis of multiple lexical and syntactic features. Specifically, we analyze differences in communicative acts in relation to gender within and between professional areas. Furthermore, we emphasise the roles of nationality, culture/tradition, and education in determining those differences. Finally, we also observe whether there is a possible change over time between 2015 and 2020.

## Research questions 

We are interested in using this dataset to answer the following question: Do speech behaviours related to confidence and uncertainty vary between men and women?

To answer this question, we'll go through the following points:

1. To what extent can we observe the differences in communicative acts in relation to gender within a professional area? Are there noticeable differences between those professional areas?

2. What are the roles of nationality, culture/tradition (religion, ethnic groups), and education (whether the speaker obtained an academic degree) in determining those differences in speech between men and women? How are the lines drawn between the language we use and the environment around us?

3. Has there been a possible change over time (from 2015 to 2020)?

## Proposed additional datasets and tools
To complement the _Quotebank_ dataset, we use the open-source stored data on Wikidata, as well as a classifier.

#### Wikidata
It is an open-source dataset (https://www.wikidata.org/wiki/Wikidata:Main_Page).

#### Uncertainty Detection Classifier
To classify the quotes according to the uncertain lexical and syntactic features, we use the public uncertainty detection classifier from the paper "P. A. Jean, S. Harispe, S. Ranwez, P. Bellot, and J. Montmain, “Uncertainty detection in natural language: A probabilistic model” ACM Int. Conf. Proceeding Ser., vol. 13-15-June, no. June, 2016, doi: 10.1145/2912845.2912873". It is available for download at: https://github.c-om/pajean/uncertaintyDetection. As this was created on python2, we had to adapt it to run on python3.

The data from _Wikidata_ and the adapted classifier can be found on this public drive: https://drive.google.com/drive/folders/1UgvnLUFhs14NDcZYH6NuZx2f_YC5i06N. More instructions are provided within the notebook.


## Methods

1. #### Pre-processing of the data

We started by cleaning the data by removing rows containing missing values on mandatory features for our study, like the speaker's identity and gender. We also checked that there were no duplicate data (no duplicate quotes in _Quotebank_ and speaker id in _Wikidata_). Additionally, only the quotes where the speaker's probability was greater than 0.5 in _Quotebank_ were kept.
  
Then, we did some exploratory data analysis, at first on the distribution of genders and then on the language of the quotes. We observed a vast distribution of 31 genders. Still, to simplify our study, we only kept the "female" and "male" genders, the others representing less than 0.03% of the data. Concerning the language of the quotes, we found that some quotes are not in English. We will further investigate how to only keep the one in English in Milestone 3.

2. #### Creation of the lists of similar professions

To be able to avoid the bias of different backgrounds between males and females, we sub-divided our data into 4 professional fields: artists, scientists, economists, and politicians.  

In order to do that, we had to merge _Quotebank_ and _Wikidata_. We merged on the ‘label’ for _Wikidata_ and ‘speaker’ in _Quotebank_. Since speakers can have the same name, we had the condition that the id of the speaker, which is unique, should be the first one in the potential speaker for the quotes (‘Qids’). To achieve the separation, we searched for the speaker’s occupation of each quote with the help of _Wikidata_. Then hand-picked the professions to look for as strings and returned them in separate pickle files for each field. This allows us to be able to hold comparisons between genders in the same category of professions. 


3. #### Classification of the quotes

To be able to use the classifier, we first needed to create text files with only the quotes and their index. Then, we ran the classifier on these files and it returned the uncertainty quotes for each file. More instructions are in the notebook to know how to run it.

4. #### Statistical-analysis

We started by analysing the gender's distribution per each professional field (artists, scientists, economists, and politicians). As our speakers are mostly males, we had to normalize our uncertain speakers by the total number of speakers of each gender.
 
To extend our research on the question of gender speech uncertainty, we investigated how do culture and education shape the way men and women speak. We based this study on the `nationality`, `ethnic_group`, `religion` and `academic_degree` columns of the speaker. This allows each time to remove the bias of the cultural, educational and environmental influence and to compare the gender speech.

Finally, we investigated a possible change from 2015 to 2020, for each professional field.

5. #### Interpretation of results & Conclusion
We concluded on our observations and proposed further extensions on the project.

## Proposed timeline 

Upcoming steps in milestone 3:
- Remove non-English quotations
- Optimization of the classifier (increase the number of features)
- Analyse differences between professions using the 6 years' datasets
- Analyse a possible cultural influence using the 6 years' datasets
- Analyse a possible change from 2015 to 2020 (using the 6 years' datasets)
- Hypothesis testing


## Organization with the team

All the members of the team worked on all "Method" steps. Still, these are the main steps that each team member worked on:

- Coralie Grobel: 1, 2, 3
- Assia Ouanaya: 2, 4
- Clement Chaffard: 1
- Fannie Kerff: 3, 4

