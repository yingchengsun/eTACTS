# eTACTS: Eligibility Tag Cloud-based Clinical Trial Search Engine (COVID-19 Version) #

This is an updated version of the system focusing solely on COVID-related trials. The original eTACTS is developed by Dr. Riccardo Miotto, see https://github.com/riccardomiotto/etacts

## eTACTS Website ##

Search engine for clinical trials allowing users to refine the results of an initial search through cloud of tags automatically extracted from the eligibility criteria.

This copy is for local testing only and does not include the update of the clinical trial repository. The up to date version of the system is only available online at: https://apex.dbmi.columbia.edu/dquest-flask/etacts/etacts.

This work was done at Columbia University, New York, USA and supported by grants R01LM009886 and R01LM010815 from the National Library of Medicine. For more details, see:

Miotto, R., Jiang, S., Weng, C. (2013) eTACTS: A Method for Dynamically Filtering Clinical Trial Search Results. Journal of Biomedical Informatics, in press.

Please cite this paper if you use this code or the online system.

Requirements: Python 2.7, flask, flask-wtf, flask-cache

Browsers: the code is optimized to work on recent versions of Chrome, Mozilla Firefox, and Safari. It has not been tested on any version of Internet Explorer.

Setup:
install the required libraries
execute: python run.py
browse: http://127.0.0.1:5000/etacts

### The instructions below are for developers ###
==============================================

## NCT Engine ##

NCT engine generates resource files that eTACTS website needs to load. 
1)	Run ”tag-mining.sh” to generate “cvocab.csv” first. You can modify the “get_clinical_trials” function in “ctgov.py” to create your own clinical trial candidate list. 
2)	Run “indexing.sh” to generate “nctec-cindex.pkl”, and rename it to “semantic-idx.pkl”.
3)	Run “arule-mining.sh” to generate “tags-arule.pkl”. 
“semantic-iidx.pkl” is generated by “semantic-idx.pkl” when the eTACTS website is loaded at the first time. 

## UMLS processor ##

Given the input files “cui-semantic-types.csv”, “preferred-cui-rank.csv” and “umls-strings.csv”, “umls processor” program will generate the “umls-dictionary.csv” file that "NCT engine" needs as input. 

## Database operations ##

To generate files used by “umls processor”
1) Install UMLS Knowledge Sources to your computer first following the instruction in UMLS official website:
https://www.nlm.nih.gov/research/umls/implementation_resources/metamorphosys/help.html
2) Install a database, such as MySQL or MSSQL.  
3) Create tables needed and load the data to the database. There are a couple of “.RRF” files offered by UMLS, but only three of them are necessary to be loaded to the database: MRSTY.RRF, MRRANK.RRF and MRCONSO.RRF. 
4) Use SQL statement to select data from tables and export to CSV format files. Since there will be comma or quotation mark within the medical terms, it is better to dump the data with CSV files separated by semicolon.

More details are shown in the "ETACTS Program Development Document.pdf"
