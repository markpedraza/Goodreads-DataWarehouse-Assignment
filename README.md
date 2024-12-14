# cis4400-homework
This is my CIS 4400 Homework assignmnet. This is roughly a semester long solo project that explores data warehousing. All images you see in this readme are located in the [images](https://github.com/markpedraza/cis-4400-homework/tree/main/Images) folder. Below in this readme you will find the following... 
- Business Requirements
- Functional Requirements
- Data Requirements
- Data Sourcing
- Data Architecture
- Information Architecture
- Technical Architecture
- Data Model
- Visualizations
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

## Solution to requirements
We will create the data architecture, information architecture, and technical architecture to lay out our plan to how to store the data. The tools we will use to accomplish this are Google Cloud Storage with Google Dataproc. PySpark will be used with Dataproc and jupyternotebook will be used when creating our scripts. We will also use Google BigQuery when we eventually create our visualizations. 

## Data Sourcing
- Data Dictionary: [cis4400_homework_data_dictionary](https://docs.google.com/spreadsheets/d/1jkoinxbfRpTWLr55Vq4RB_nFU3xyZ6ytug9vWEJ8YIY/edit?usp=sharing)
- The data will be sourced through a connection to a Data Store/Cloud Storage. Specifically, Google Cloud Storage. 

## Data Architecture
![Data Architecture](https://github.com/markpedraza/cis-4400-homework/blob/main/Images/Data%20Architecture.png)

The Data Source contains multiple JSON files that includes metadata about books and authors from Goodreads.com. This data will then be moved into temporary storage, then into a Datamart, and finally it will be used there to create visualizations. 

## Information Architecture
![Information Architecture](https://github.com/markpedraza/cis-4400-homework/blob/main/Images/Information%20Architecture.png)

First, we have our Data Source, which is located [here](https://mengtingwan.github.io/data/goodreads.html#datasets). From this source, we will gather the data and put it in a temporary storage. The data is very large, so any interruptions during extraction and transformation will result in significant time loss as the process would need to be restarted. The temporary storage will alleviate this. After temporary storage, the data will be cleaned, then finally be stored in the Data Warehouse.
Users will simply get access to reports generated from the Data Warehouse and will not get access to the Data Warehouse itself. 

## Technical Architecture
![Technical Architecture](https://github.com/markpedraza/cis-4400-homework/blob/main/Images/Technical%20Architecture.png)

Here, we can see specifically the tools and types of files we will be dealing with. All scripts mentioned here are located in the [Scripts](https://github.com/markpedraza/cis-4400-homework/tree/main/Scripts) folder. From the website with the data, we will use the ExtractLoad script to extract the data and load it into our Google Cloud Storgae bucket. Then we will use the Clean script to read the data from teh bucket, clean it, then write it back out to the bucket. Once thats done, we will use the DimensionCreation script to seperate, transform, and consolidate the data to create our facts tables and dimensions. This will be loaded into BigQuery, where we can finally use Tableau to visualize the data. 

## Data Model
![DBSchema](https://github.com/markpedraza/cis-4400-homework/blob/main/Images/DBSchema.png)

This is the schema for the assignment, and was assembled using DBSchema. The file for this is located in the docs folder.

For the most part, all features in this schema are already available to us in our data, just not organized in this way. Some of it has been flattened, such as genres which was nested with extra data, and needed to be extracted by itself. However, the biggest change here is how the authors are set up. Authors in the original dataset include other roles such as illustrators and editors, so they arent purely authors. Also, there can be many authors per book. So in the data, each book has an authors array that details their author_id and role they had in creating the boook. So the that sinlge authors column can be fairly complicated. I would've liked to have flattened this data to only include authors who wrote the books, but due to time constraints, I had to do a faster method. 
 
Instead, I took the first 3 values from the authors array and discarded the roles they were assigned, then flattened these values. This leaves us with 3 new columns (author_1_id, author_2_id, author_3_id) that each give the author_id for the authors that worked on a book. Obviously though, not all books have 3 authors, so there will be null values columns following the first. But also, some books could have more than 4 authors, so unfortunately that data was lost in this modified dataset. However, although not perfect, this data will still be useful for us if we wish to make general visualizations for authors. 

## Visualizations
Once all the steps above are completed, we can move our data to Google BigQuery and visualize it with Tableau. Below are those visualizations.

###

## Citations 

- Mengting Wan, Julian McAuley, "[Item Recommendation on Monotonic Behavior Chains](https://github.com/MengtingWan/mengtingwan.github.io/raw/master/paper/recsys18_mwan.pdf)", in RecSys'18. [[bibtex](https://dblp.uni-trier.de/rec/bibtex/conf/recsys/WanM18)]
- Mengting Wan, Rishabh Misra, Ndapa Nakashole, Julian McAuley, "[Fine-Grained Spoiler Detection from Large-Scale Review Corpora](https://github.com/MengtingWan/mengtingwan.github.io/raw/master/paper/acl19_mwan.pdf)", in ACL'19. [[bibtex](https://dblp.uni-trier.de/rec/bibtex/conf/acl/WanMNM19)]
