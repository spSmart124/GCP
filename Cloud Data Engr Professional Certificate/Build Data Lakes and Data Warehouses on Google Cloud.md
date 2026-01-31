# Build Data Lakes and Data Warehouses on Google Cloud
## Chapter 1
### Introduction to Modern Data Engineering on Google Cloud
#### The classics: Data lakes and data warehouses
For years, organizations have relied on two primary methods for large-scale data storage: data lakes and data warehouses.

They serve different purposes and are optimized for different kinds of data and workloads. To understand them, let's consider the example of Cymbal, a major e-commerce company.

##### Data lakes
Think of a data lake as a vast reservoir of data. It stores enormous amounts of raw data in its native format. You can pour any kind of data into it; structured, semi-structured, and unstructured.

For Cymbal, this means storing:
1. Structured data, like transaction tables from its sales database.
1. Semi-structured data, like JSON logs from its web servers.
1. Unstructured data, like customer-submitted product images, videos, and text reviews.

Data lakes are created on the premise of "store everything now, figure out how to use it later." With this approach, you apply a structure to the data when you read it (schema-on-read), not when you store it.

This makes data lakes ideal for data exploration, machine learning, and big data processing. Cymbal's data scientists, for example, need access to original, unaltered clickstream data to build a new recommendation engine.

###### Advantages of data lakes
1. Flexibility: Stores all data types.
1. Agility: Fast to ingest data.
1. Scalability: Can grow to exabyte scale.
1. Cost-effectiveness: Uses low-cost object storage.
1. Support for advanced analytics: Ideal for AI/ML model training.

###### Disadvantages of data lakes
1. Risk of becoming a "data swamp": Without proper governance, it can become a disorganized collection of unusable data.
1. Management complexity: Requires significant overhead to maintain.
1. Time-consuming analysis: Data often needs to be cleaned and wrangled before it is usable.
1. Security risks: Raw data formats can increase security and compliance risks.

#### The modern approach: Data lakehouse
A **data lakehouse** architecture combines the low-cost storage of a data lake with the management features and query performance of a data warehouse. The goal is to create a single, unified platform that can support traditional BI, modern data science, and AI workloads without moving or duplicating data.

A lakehouse achieves this by implementing a metadata and governance layer on top of open-format files stored in low-cost object storage, like Google Cloud Storage. This gives you the best of both worlds.


For Cymbal, a lakehouse solves a key challenge: breaking down data silos. Previously, its sales data was in a warehouse and its customer review data was in a data lake.

The two could not be analyzed together easily. With a lakehouse, Cymbal can now run a single query to correlate customer sentiment from text reviews with sales trends from its transaction database.

##### Key feautures of a Google Cloud data lakehouse
1. Support for most data formats
1. Flexible schema-on-read or schema-on-write
1. Access for all types of data users
1. Cost flexibility based on needs
1. Unified data governance
1. ACID transaction support

Google Cloud implements **data lakehouses** through BigLake technology. BigLake allows you to apply Google Cloud’s governance and query capabilities to data stored in Google Cloud or even in other major clouds. You can manage and query your data where it lives, using open formats like Parquet, ORC, and Avro, while benefiting from BigQuery's powerful and flexible query engine.

Data lakehouses solve many challenges by unifying data storage and access.
The benefits include:

* Reduced data redundancy
* Unified governance
* Broken-down data silos
* Improved flexibility and scalability