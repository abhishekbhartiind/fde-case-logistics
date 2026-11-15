- SOP Ingestion

## data/policy 
- can have multiple files => (.md / .txt / .csv / .pdf / .xlsx)
- we should have different chunking logincs

#### MD
- Split headers -> 
- Section  -> 
- Text splitters -> 
- Chunks for data -> 

#### TXT
- directly use splitters -> chunks

#### PDF
- Page wise => 
- Split Page first, then from page
- we have to split the contents
- pages is going into the text splitters
- chunks

#### csv / xlsx
- convert to data frame (panda data frame)
- each data frame i will extract row
- row i will convert to dictionary
- then each dictionary i am converting string kind of format
- then i will ingest one by one 
- string -> text splitter => chunks
