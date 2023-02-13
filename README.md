# <div align="center">TIKI DATA MINING</div>

### Web Scraping

Step1: Crawling all information about product ID and categories Id from Tiki main page

Step2: Crawling the data following product ID

Step3: From one categories, we continue crawl the relate product ID

### Data Cleaning
🔆 After scraping the data, I needed to clean it up so that it was usable for our model. I made the following changes and created the following variables:
- Remove the data which have exist in database
- Detect the data in same store from **seller** and allow it **null**
- Flatten the nested feild in the data


### 💡The Process to automatic Minint the data and insert to database:

![alt text](https://github.com/DungNguyen0209/Crawling_Product_Data_From_Tiki/blob/main/Assert/Presentation1.jpg?raw=true)

🔻***Main Thread:*** Two array categories_id and product_id is the common resource among the multi threads
    -> The process stop when the categories is empty 

🔻***Product_id Thread:*** Get the first element in categories list to crawl all product id and add it to product_id list in Main thread

🔻***Product Data Thread:***
    
   - Task1: Cleaning and insert into 3 DataFrame: product, categories và seller.
    
   - Task2: Import each DataFrame to  MySQL. Because we share resource between threads so the import thread have to be locked until the process done.
