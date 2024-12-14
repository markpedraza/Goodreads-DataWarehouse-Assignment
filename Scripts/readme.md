# Scripts

I used Google Cloud Platform for my project and made all my scripts using Google Dataproc and PySpark. The data was large, so a cluster was needed to process all the data, specifically when cleaning and creating dimensions. All scripts also assume we have a bucket created in Google Cloud Storage named _goodreads_bucket_ that has the folders _landing_, _cleaned_, and _dim_ready_. The landing folder stores the intial extracted raw data, the cleaned folder stores all cleaned data, and the dim_ready folder stores the data that can be easily transported to Google BigQuery. Below is a quick description of each script below


## ExtractLoad

This scirpt is essentially the same as the one provided by the creator of our data, Mengting Wan. She has kindly provided a script to download her data in her GitHub. The link for the original script is [here](https://github.com/MengtingWan/goodreads/blob/master/download.ipynb). Without her script, finding out how to extract this data would have been significantly more difficult for me, so please check her work. 

My own script is a modified version of the original. This script downloads the data locally to the computer, then uploads that local data to the landing folder of googreads_bucket. Remember, we are not using our actual local machines here, but instead a Dataproc cluster, so its downloading to the "cloud" computer then uploading to a bucket. This script also automatically unzips the downloaded files and uploads only extracted files. 

## Clean

Loads in our data from the landing folder of the goodreads_bucket, then cleans it, and writes it out to the cleaned folder of the same bucket. The data is mostly clean to begin with, so not much cleaning was required.

## DimensionCreation

Loads in the cleaned data. Then, it seperates the data in such a way as to follow our schema that we created in DBSchema. The script creates the facts tables and dimensions as PySpark dataframes, then writes those individual dataframes out to the dim_ready folder. However, since we are writing out our data as parquet files, they need to be stored in their own folder or else all the facts and dimensions will write over each other. To solve this, the script automaticaly creates any folder necessary inside the dim_ready folder for each dataframe that is written out. They are also named appropriately.
