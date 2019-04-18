# InclusionCriteria
Instructions Creators: Xiaoru Dong, Linh Hoang <br/>
Preparation date: 2018-12-14, last updated 2019-04-18 <br/>
Manuscript working title: Machine classification of inclusion criteria from Cochrane systematic reviews <br/>
Manuscript authors: Xiaoru Dong, Jingyi Xie, Linh Hoang, and Jodi Schneider <br/>

# INSTRUCTIONS

## Description:
These instructions describe the steps needed to replicate the results in the manuscript. 

## 1. Python program:
- Programming Language: Python (version 3.0)

- Please make sure that you have the following programs on your machine in order to run the scripts:
  - Python 3.0: https://www.python.org/downloads/
  - Jupyter Notebook: http://jupyter.org/install 

- The Python scripts are used to generate features and to create the Weka input files corresponding to the 3 feature extraction and selection approaches that we implemented in this study: 
	- Features generated by the bag of words feature extraction strategy.
	- Features selected by the information gain feature selection strategy. 
	- Features selected by a manual analysis feature selection strategy.

### Python script to generate features by the bag of words feature extraction approach:

  - Step 1: Download the script: https://github.com/infoqualitylab/InclusionCriteria/blob/master/bag_of_words_feature_extraction.ipynb

  - Step 2: Download the input file “Inclusion_Criteria_Annotation.csv” (one of the study’s data files), which is available at: https://doi.org/10.13012/B2IDB-5958960_V2. Note where you store the file.

  - Step 3: Open the script in Jupyter Notebook. Change the “path” variable in the script to the path of your own folder where you stored the input file. 

  - Step 4: Run the script to get two output files: "AllWords.csv" and "AllWords_weka_input.arff"
  
  - Step 5: Use the "AllWords_weka_input.arff" file as the input in order to run the classification model in Weka (for how to run classification model in Weka, please read the Weka section below)
  

 ### Python script to generate features by the information gain feature selection approach:
 
  - Step 1: Download the first script: 
  https://github.com/infoqualitylab/InclusionCriteria/blob/master/generate_no_redundant_Weka_input.ipynb

  - Step 3: Open the script in Jupyter Notebook. Change the “path” variable in the script to the path of your own folder where you stored the input file. 

  - Step 4: Run the script to get two output files: "AllWord_Noredundant.csv" and "AllWord_Noredundant_weka_input.arff"
  
  - Step 5: Use the "AllWord_Noredundant_weka_input.arff" file as input in order to run information gain in Weka (for how to run information gain in Weka, please read the Weka section below). After running information gain in Weka, save the "InformativeWords" from Weka to the same folder.
  
  - Step 6: Download the second script: 
  https://github.com/infoqualitylab/InclusionCriteria/blob/master/information_gain_feature_selection.ipynb
  
  - Step 7: Open the script in Jupyter Notebook. Change the “path” variable in the script to the path of your own folder where you stored the input file. 

  - Step 8: Run the script to get two output files: "WordsSelectedByInformationGain.csv" and "WordsSelectedByInformationGain_weka_input.arff"
  
  - Step 9: Use the "WordsSelectedByInformationGain_weka_input.arff" file as input in order to run classification model in Weka (for how to run classification model in Weka, please read the Weka section below)
  
 ### Python script to generate features by the information gain feature selection approach:

  - Step 1: Download the script: https://github.com/infoqualitylab/InclusionCriteria/blob/master/manual_analysis_feature_selection.ipynb

  - Step 2: Download the input file “WordsSelectedByManualAnalysis.csv” (one of the study’s data files), which is available at: https://doi.org/10.13012/B2IDB-8659314_V1. Note where you store the file.

  - Step 3: Open the script in Jupyter Notebook. Change the “path” variable in the script to the path of your own folder where you stored the input file. 

  - Step 4: Run the script to get one output file: "WordSelectedbyManualAnalysis_weka_input.arff"
  
  - Step 5: Use the "WordSelectedbyManualAnalysis_weka_input.arff" file as input in order to run classification model in Weka (for how to run classification model in Weka, please read the Weka section below)


## 2. Weka program:

- Please make sure that you have Weka on your machine in order to implement the classifiers: https://www.cs.waikato.ac.nz/ml/weka/downloading.html 

### Run classification in Weka:
  - Step 1: Open Weka on your machine, select “Explorer” mode. 
  - Step 2: On the “Preprocess” tab: <br/>
  --> Click “Open file” and select the Weka input file that you want to implement classification with. For example: if you want to implement a classifier with all features, select the “AllWords_weka_input.arff” Weka input file as shown in the screenshot below. <br/>
  ![1](https://user-images.githubusercontent.com/34040989/50197129-6aa17300-030b-11e9-9180-1f0baa518fa3.png) <br/>
  --> Click “All” to choose all of the words and use them as features to train the classifier as shown in the screenshot below. <br/>
  ![2](https://user-images.githubusercontent.com/34040989/50197245-e00d4380-030b-11e9-9bb6-1f9fa53a6d02.png) <br/>
  - Step 3: On the “Classify” tab: <br/>
  --> Click “Choose” to select the algorithm that you want to run. NOTE: We used three algorithms: Random Forest, J48 and Naïve Bayes. For example: if you want to run a classifier using “Random Forest” algorithm, select RandomForest as shown in the screenshot below: <br/>
  ![3](https://user-images.githubusercontent.com/34040989/50197249-e3083400-030b-11e9-844d-c7e4254a5a64.png) <br/>
  --> Click “Percentage split” in the “Test options” and put 90% (this means we want to get 90% of our data set for training, 10% for testing). <br/>
  --> Click “More Options...” and set the seed to 3. <br/>
  --> Click “Start” to run the classifier: <br/>
  ![4](https://user-images.githubusercontent.com/34040989/50197252-e56a8e00-030b-11e9-8f5f-cdf8304ab4ea.png) <br/>
  - Step 4: Get the classifier results. Three measurements were reported in our manuscript: Precision, Recall and F-Measure as shown in the screenshot below. <br/>
  ![5](https://user-images.githubusercontent.com/34040989/50197255-e7cce800-030b-11e9-9fb0-8a062e72e822.png) <br/>

### Run information gain o Weka:
  - We also used Weka to run Information Gain feature selection. To do so: <br/>
  -->  On the “Preprocess” tab: Click “Open file” and select the Weka input file AllWord_Noredundant_weka_input.arff <br/>
  --> On the “Select attributes” tab: <br/>
  Click “Choose” and select “InfoGainAttributeEval” as shown in the screenshot below. <br/>
  ![6](https://user-images.githubusercontent.com/34040989/50197256-e8fe1500-030b-11e9-84e8-2b842452cc2d.png) <br/>
  Click “Start” to run the Information Gain feature selection. <br/>
  --> Weka generated a list of informative words selected by Information Gain feature selection strategy. We then used the python script (above) to generate the data file “WordsSelectedByInformationGain.csv” and the Weka input file “WordsSelectedByInformationGain_weka_input.arff” accordingly. <br/>


**For any questions about the instruction, please contact: <br/>
Linh Hoang - lhoang2@illinois.edu.**
