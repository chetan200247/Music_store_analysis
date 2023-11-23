# Music_store_analysis
This data projects aims to provide insights into the sales performance. By analyzing the various aspects of sales data, we seek to identify trends, make data-driven recommendations,
and gain a deeper understanding of the company's performance.

### Data Source
The data source for this project are the various tables associated with the music store:

### Tools used
1. Excel-Data cleaning
2. SQL- Data analysis
3. Power BI- Data visualization
   
#### Table-------------------------------Columns
    1.Employee                    employee_id,first_name,last_name,title,reports_to,birthdate,hiredate,address,citystate,country,postal_code,phone,fax,email
    2. Customer                   customer_id,first_name,last_name,company,address,city state,country,postal_code,phone,fax,email,suppoert_report_id   
    3. Invoice                    invoice_id,customer_id,invoice_date,billing_address,billing_city,billing_state,billing_country,billing_postal_code,total
    4. Invoice_line               invoice_line_id,invoice_id,track_id,unit_price,quantity
    5. Track                      track_id,name,album_id,media_type_id,genre_id,composer,milliseconds,unit_price
    6. Playlist_track             playlist_id,track_id
    7. Playlist                   playlist_id,name 
    7. Album                      album_id,title,artist_id
    8. Artist                     artist_id,name
    9. Genre                      genre_id,name
    10. media_type                media_type_id,name

## Data cleaning and preparation
In the initial phase of the project we performed the following steps in Excel:
- Importing data and inspection
- Handling missing and duplicate values
- Formatting the tables

## Exploratory Data analysis
We will be exploring the data using SQL. For this we have to first import the tables into the database. It will consist of following steps:

### 1. Creation Of Database
CREATE DATABASE music_store;

### 2. Creating of tables before importing the data
CREATE TABLE artist(
artist_id varchar(50) PRIMARY KEY,
name varchar(120) );

CREATE TABLE album(
album_id varchar(50) PRIMARY KEY,
title varchar(120),
artist_id varchar(30) REFERENCES artist(artist_id));

We will create other tables in the same way

### 3. Importing the data
COPY artist FROM 'C:\Data science\music store data\artist.csv'
WITH (FORMAT CSV, HEADER)

COPY album FROM 'C:\Data science\music store data\album.csv'
WITH (FORMAT CSV,HEADER)

We will copy the data from the CSV files to the other tables in the same way

### 4. Exploratory Data Analysis

Q1. Who is the senior most employee in the music_store?
- SQL- select first_name,last_name , age(current_timestamp,hire_date) as Experience
     from employee order by age(current_timestamp,hire_date) desc Limit 1;
- Answer- Mohan Madan 7 years 10 mons 9 days

Q2.Who is the latest recruit in the music store?
- SQL-select first_name,last_name  
      from employee order by age(current_timestamp,hire_date) limit 1;
- Answer- Steve Johnson

Q3. Which country has the highest number of invoices?
- SQL- select billing_country, count(*) from invoice
       group by billing_country order by count(*) desc limit 1;
- Answer- USA 131

Q4. Which country has the highest invoice total?
- SQL- select billing_country, sum(total) from invoice
       group by billing_country order by sum(total) desc limit 1;
- Answer- USA 1040.48

Q5. What are the top 3 values of total invoice?
- SQL- select total from invoice order by total limit 3;
- Answer- 23.759999999999998
          19.8
          19.8
  
Q6. In which city they should throw a music festival?
- In the city with genereates the highest revenue
- SQL- select billing_city,sum(total) from invoice group by billing_city
       order by sum(total) desc limit 1;
- Answer- Prague- 273.24

Q7. Who is the most revenue generating customer?
- SQL- select c.first_name,c.last_name,sum(i.total) from customer as c
       join invoice as i on c.customer_id=i.customer_id
       group by c.customer_id
       order by sum(i.total) desc;
- Answer- R Madhav 144.54

Q8. Details of customers who listen to rock music?
- SQL- select distinct customer.first_name,customer.last_name, customer.email
       from customer
       join invoice on invoice.customer_id=customer.customer_id
       join invoice_line on invoice_line.invoice_id=invoice.invoice_id
       join track on track.track_id=invoice_line.track_id
       join genre on genre.genre_id=track.genre_id
       where genre.name= 'Rock'
       order by customer.first_name;
  
Q9. Artist who has composed maximum number of rock music?


  
  
