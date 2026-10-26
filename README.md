# Problem Statement

Let's suppose there is this logistic company that stores their supply chain data in one of their legacy system over cloud. And the problem statement is they want to talk to their data.

Clients ───▶  Data in cloud ───▶ Chat with the data

Data Source => 
- legacy system => MS-SQL 2022 (Server Name)
- They will provide (ID, Password)

Chat with data => Dashboard
1. Dashboard => have multiple APIs which fetch data from DB with UI with many type of charts to display data and menu, learning curves etc.. Thier SOPs (Standard Operating Procedures)

2. Agentic AI Solution based chatbot 

I want to get the supply chain logistic data for year 2024 month January and date between 01 that is 1st till 15th of January. 
Give me the analytics and you can directly ask that I'm looking for so so so matric and when you pass that your chatbot or your agentic solution it is going to go into the database trying to retrieve the data and then once it has the data it will try to make sense of the data and provide you the final answer. 

So here usually we have much lesser steps as compared to dashboard and the learning curve is you just need to know the language 


## Legacy System

1. Data Ingestion/Extraction:
    -legacy system => MS-SQL Server 2022 => Docker Container => AWS S3 Bucket 
    
2. Data Storage/Processing:
    -AWS S3 Bucket 
    -AWS EC2 Instance (C7i-flex.large) => Linux Based OS (Ubuntu) => Docker Container
    
3. Data Analysis:
    -AWS EC2 Instance (C7i-flex.large) => Linux Based OS (Ubuntu) => Docker Container
    
4. Data Visualization:
    -AWS EC2 Instance => Linux Based OS (Ubuntu) => Docker Container => AWS S3 Bucket => 


# Solution Discussion

**What do we mean by "Talk to our data" ?**
- Legacy systems and SOPs are shared by clients.
- Is our data structures 
    => No (images, videos, pdf etc..)
    => Yes (tables, rows, columns) => Relational DB (MSSQL)
- Is our SOPs => Text stored in DB in document format.
- If yes, We have ask what works here ? RAG ? Api for visual analytics 
    => if "Api for visual analytics" => it means we have to write api for sql queries (we can take help of LLM) and give response from API (we can plot it on dashboard) and also follow the same SOPs to get the data for dashboard. and also provide chat bot. 
- If no, Follow RAG based approach

Query Details
-------------

- based on location => based on country, based on city, based on zip code, based on state, based on latitude/longitude or coordinates 
- based on coordinate => what is the distance between two coordinates ? what is the closest warehouse to this coordinate ? what is the furthest warehouse from this coordinate ? 
- perishable => perishable items are more likely to spoil if not stored or transported under the right conditions. what is the list of perishable items ? what is the percentage of perishable items in my inventory ?
- seasonal heat spikes => temperature / refrigration based question 
- weather conditions => Is there any weather condition that can affect my supply chain ?  
- combinations from above => what is the percentage of perishable items in my inventory that are currently in transit and are in a region that is experiencing heat spikes ?  
- query from SOPs => SOPs (what is our return policy ? what is our replacement policy ? what is our warranty policy ?

Security
- Agent doesn't not insert / delete the data, only select/fetch the data from DB.

what does it takes to build security in mind ?

```bash

Agent => Unnessary command => Actions
              |
              V
            Find ? => Database => Create users      user.id / user.password [user, password]
                                   | 
                                   V
                                Restrict Access

```

Data Sources
- Relational DB
- Knowledge from SOPs


# Presentation
# Coding/Implementation
