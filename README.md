# cis4400-homework
This is my CIS 4400 Homework assignmnet. This is roughly a semester long solo project that explores data warehousing. Below in this readme you will find the following... 
- Business Requirements
- Functional Requirements
- Data Requirements
- Data Sourcing
- Information Architecture
- Data Architecture.
- Technical Architecture
- Citations

The creator of this dataset is Mengting Wan, and her github can be found here: https://github.com/MengtingWan. If you are interested in learning more about who gathered this dataset, please visit her GitHub. Citations for her work can be found at the bottom of this readme.


## Business Requirements
1. Do users who write reviews rate differently on average from those who give ratings but no reviews?

## Functional Requirements
1. Number of users who have given ratings.
2. Unique ISBN for each book to prevent duplicates.
3. Number of ratings a book receives, and the rating score.
4. The number of written reviews per book and each reviews rating score.

## Data Requirements
- Data: https://mengtingwan.github.io/data/goodreads.html#datasets

## Data Sourcing
- Data Dictionary: [cis4400_homework_data_dictionary](https://docs.google.com/spreadsheets/d/1jkoinxbfRpTWLr55Vq4RB_nFU3xyZ6ytug9vWEJ8YIY/edit?usp=sharing)
- The data will be sourced through a connection to a Data Store/Cloud Storage. Specifically, Google Cloud Storage. 

## Information Architecture
![Information Architecture](https://github.com/markpedraza/cis-4400-homework/blob/main/Images/Information%20Architecture.png)

First, we have our Data Source, which is located [here](https://mengtingwan.github.io/data/goodreads.html#datasets). From this source, we will gather the data and put it in a temporary storage. The data is very large, so any interruptions during extraction and transformation will result in significant time loss as the process would need to be restarted. The temporary storage will alleviate this. After temporary storage, the data will be cleaned, then finally be stored in the Data Warehouse.
Users will simply get access to reports generated from the Data Warehouse and will not get access to the Data Warehouse itself. 

## Data Architecture
![Data Architecture](https://github.com/markpedraza/cis-4400-homework/blob/main/Images/Data%20Architecture.png)

The Data Source contains multiple JSON files that includes metadata about books and authors from Goodreads.com. This data will then be moved into temporary storage, then into a Datamart, and finally it will be used there to create visualizations. 

## Technical Architecture
![Technical Architecture](https://github.com/markpedraza/cis-4400-homework/blob/main/Images/Technical%20Architecture.png)

Here, we can see specifically what tools we will use and how we will store everything. From the website, we will use the ExtractLoad script to extract the data and load it into our Google Cloud Storgae bucket. Then we will use the Clean script to read the data from teh bucket, clean it, then write it back out to the bucket. Once thats done, we will use the DimensionCreation script to seperate, transform, and consolidate the data to create our facts tables and dimensions. This will be loaded into BigQuery, where we can finally use Tableau to visualize the data. 

## Data Model
![DBSchema](https://github.com/user-attachments/assets/83745b5a-00d5-4450-9098-92246cc916ad)

This is the schema for the assignment, and was assembled using DBSchema. The file for this is located in the docs folder.

## Citations 

- Mengting Wan, Julian McAuley, "[Item Recommendation on Monotonic Behavior Chains](https://github.com/MengtingWan/mengtingwan.github.io/raw/master/paper/recsys18_mwan.pdf)", in RecSys'18. [[bibtex](https://dblp.uni-trier.de/rec/bibtex/conf/recsys/WanM18)]
- Mengting Wan, Rishabh Misra, Ndapa Nakashole, Julian McAuley, "[Fine-Grained Spoiler Detection from Large-Scale Review Corpora](https://github.com/MengtingWan/mengtingwan.github.io/raw/master/paper/acl19_mwan.pdf)", in ACL'19. [[bibtex](https://dblp.uni-trier.de/rec/bibtex/conf/acl/WanMNM19)]
