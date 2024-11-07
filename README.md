# cis4400-homework
This is my CIS 4400 Homework assignmnet. Below in this readme you will find the Business Requirements, Functional Requirements, Data Requirements, Data Sourcing, Information Architecture, and finally the Data Architecture


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
- Data Dictionary: cis4400_homework_data_dictionary
- The data will be sourced through a connection to a Data Store/Cloud Storage. Specifically, Google Cloud Storage. 

## Information Architecture
![Information Architecture](https://github.com/user-attachments/assets/86408ac6-b99a-4ff6-ae2e-6fbfe6fd1c11)

First, we have our Data Source, which is located in. (https://mengtingwan.github.io/data/goodreads.html#datasets). From this source, we will gather the data and put it in a temporary storage. The data is very large, so any interruptions during extraction and transformation will result in significant time loss as the process would need to be restarted. The temporary storage will alleviate this. After temporary storage, the data will be cleaned, then finally be stored in the Data Warehouse.
Users will simply get access to reports generated from the Data Warehouse and will not get access to the Data Warehouse itself. 

## Data Architecture
![Data Architecture](https://github.com/user-attachments/assets/dee7a8a3-a8b0-43da-bc56-f470263559d0)

The Data Source contains multiple JSON files that include data and metadata about books from Goodreads.com. This data will then be moved into temporary storage, then into a Datamart, and finally it will be used there to create visualizations. 
