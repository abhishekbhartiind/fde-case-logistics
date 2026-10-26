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
- Legacy systems and SOPs (Standard Operating Procedure) are shared by clients. (Given in data)
- Is our data structures 
    => No (images, videos, pdf etc..)
    => Yes (tables, rows, columns) => Relational DB (MSSQL) / tools / API for usual analytics (dashboard)
- Is our SOPs => Text stored in DB in document format.
- If yes, We have ask what works here ? RAG ? Api for visual analytics 
    => if "Api for visual analytics" => it means we have to write api for sql queries (we can take help of LLM) and give response from API (we can plot it on dashboard) and also follow the same SOPs to get the data for dashboard. and also provide chat bot.  
- If no, Follow RAG based approach (for unstructured data)

## Query Details
-------------
```bash
1. Based on location
2. Based on coordinate
3. Based on perishable items
4. Based on seasonal heat spikes
5. Based on weather conditions
6. Based on combinations from above
7. Based on SOPs
```

- based on location they can query => based on country, based on city, based on zip code, based on state, based on latitude/longitude or coordinates
- based on coordinate they can query => what is the distance between two coordinates ? what is the closest warehouse to this coordinate ? what is the furthest warehouse from this coordinate ? Within the range of coordinate how many shipments are going which has high risk etc, they will able to query dashboard via coordinates.
- based on perishable => perishable items are more likely to spoil if not stored or transported under the right conditions. what is the list of perishable items ? what is the percentage of perishable items in my inventory ?
- based on seasonal heat spikes => temperature / refrigration based question -> Usually when we are doing shipment we sometimes get unseasonal heat spikes. Is refrigated shipment going on correctly or not ? (Check temperature inside refrigated container is 4 degree celsius)
- based on weather conditions, whether if it is raining, snowing, hurricane etc => Is there any weather condition that can affect my supply chain ?  
- based on combinations from above => what is the percentage of perishable items in my inventory that are currently in transit and are in a region that is experiencing heat spikes ?  
- based on SOPs => SOPs (what is our return policy ? what is our replacement policy ? what is our warranty policy ? Query based on SOPs. Fresher / Intern joined the company, ask queries for SOPs to understand SOPs. "I want to know how to raise a ticket for damaged goods" etc..)

## Security
- Agent doesn't not *insert / delete* the data, only select/fetch the data from DB. Agent should not modify, insert or delete data from DB.
- Agent should not able to access user credentials in anyhow. They should not be able to see or fetch user credentials. Like user.id / user.password etc.. or interacted with unknown tables if not asked. (i.e. system tables, other tables etc..)

### What does it takes to build system with *security* in mind ?

```bash

Agent => Unnessary command => Actions will be performed
              |
              V
            Find ? => Database => Create multiple users      user.id / user.password [user, password]
                                   | 
                                   V
                                Restrict Access => Only CRUD(Select) operations on required tables

```
We are going to use same credentials (new access without insert/delete), we are blocking the access from core from software


Data Sources
- Relational DB
- Knowledge from SOPs


Relational DB
- Can see grow ? YES (data will forsure grow)

To exract the data we can use
- API (For dashboard)
- MCP (Model Context Protocol) (For agentic solution) => We can extract data from MCP and through MCP we can create custom tools which agent can use to extract data from DB.

if we want to expose an MCP to an AI Agents, so it can use this tools and give us the answers and that anwers we can passed it to agents and agent will be interacting with MCP.

We can create a tools ? How many tools ? => We need to ask from clients and based on that we can create tools, so they can use this tools and 

- Instead of MCP, we can use **test2SQL** or **MISTRAL SQL MODEL** to create tools which can be used to extract data from DB.

**test2SQL** => can generate SQL queries for given prompt (But it is not much efficient for this case as it will generate queries which can be very costly)

If AI Agent is asking i want to get these data, then our AI Agent writes SQL script and we are going to use the dynamic SQL that SQL that AI has created and run the SQL => get the data => pass it to LLM => LLM process it => give final answer to user. (and we will ask from user that does this query is correct or not ?)

**MISTRAL SQL MODEL** => can generate SQL queries for given prompt (And it is much more efficient for this case as it will generate queries which can be very optimized)

If AI Agent is asking i want to get these data, then our AI Agent writes SQL script => pass it to **MISTRAL SQL MODEL** => it generate query => execute on DB => get data => pass it to LLM => LLM process it => give final answer to user. (and we will ask from user that does this query is correct or not ?)

**Note** -
- We can also use LangChain SQL Agent.
- We can also create a MCP for this if we want to provide more better and optimized experience. (Depends on client) 

**Custom tools** => How many tools ? 
- We have to ask from clients and based on that we can create tools, so they can use this tools and 



# Presentation
# Coding/Implementation
