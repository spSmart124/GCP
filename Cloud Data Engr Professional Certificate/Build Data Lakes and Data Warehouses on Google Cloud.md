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

#### Choosing the right architecture
While a data lakehouse is the newest approach, a data lake or a data warehouse might be a better fit for your specific needs. Let’s consider when each approach might be the best choice for Cymbal.

Consider a data warehouse, like BigQuery, when the primary need is high-speed, interactive BI on structured business data, such as for Cymbal's finance department.

Consider a data lake, using Cloud Storage, for the initial, low-cost storage of massive volumes of raw data. This is ideal for Cymbal's AI/ML research and development where the data's final use is not yet defined.

Adopt a data lakehouse architecture with BigQuery and BigLake when you need to do it all: support BI, AI, and data science on a single, governed copy of your data, providing a holistic view for the entire company.

## Chapter 2
### Building a data lake foundation
From customer purchase history and website clicks to supply chain logistics and marketing campaign performance, Cymbal generates massive amounts of diverse data. A robust data architecture is essential to make informed business decisions, personalize customer experiences, and optimize operations.

A data lakehouse combines the key features of data lakes and data warehouses. It offers the flexibility and scalability of a data lake for storing raw, unstructured, or structured data, with the schema enforcement and query performance of a data warehouse. This hybrid approach allows organizations like Cymbal to handle all their data needs in one unified system.

Google Cloud provides a powerful set of tools to build this unified architecture. The primary storage for your data lakehouse is Cloud Storage. Cloud Storage is a massively scalable, highly durable, and cost-effective object storage service. Cymbal can use it to store almost any type of data file, regardless of its size or format. However, you are not limited to using Cloud Storage. If your strategy is multi-cloud, you can keep your data in another major provider's cloud storage.

One of the biggest advantages of Cloud Storage is its ability to store multimodal data. This means you can store data in various formats and structures in one place. For Cymbal, this is incredibly valuable.

#### Structured Data Files
Structured data is information that is highly organized into a predefined format, much like a spreadsheet with clear rows and columns. At Cymbal, this includes essential data like customer lists, product catalogs, and sales transactions. Because it has a predictable model, this data is easy for computers to search, analyze, and process.

#### Semi-Structured Data Files
Semi-structured data is a blend of structured and unstructured data, as it doesn't have a rigid, predefined model but contains tags or other markers to create a hierarchy of records and fields. For example, Cymbal might receive order details as a JSON file, which has a consistent overall structure but allows for variations in the specific information included for each product.

#### Unstructured Data Files
Unstructured data is information that doesn't have any predefined organizational structure. For Cymbal, this includes a wealth of valuable information like the text from customer product reviews, support chat logs, and product images. While this data is more complex to process, it holds key insights that can be unlocked with modern analytics and AI tools.


Cloud Storage can handle all of these data types. It provides the flexibility to store raw, unprocessed data as it arrives, without needing to define its structure beforehand. This is crucial for Cymbal as they continuously collect new types of data and want to analyze it later without immediate transformations.

### Introduction to Apache Iceberg open table format
While Cloud Storage is excellent for storing raw files, a data lakehouse needs a way to bring structure and performance to this data. This is where open table formats come into play, and Apache Iceberg is a leading example.

Imagine Cymbal has millions of customer orders stored as files in Cloud Storage. If they want to query these orders efficiently, for example, to find all orders placed in the last week by customers in a specific region, traditional file-based queries would be slow. They would have to scan every file to find the relevant information.

Apache Iceberg solves this by adding a layer of metadata and structure on top of the files in Cloud Storage. It does not move your data; it organizes and manages it, acting as an index and catalog for your data files.

#### Features of Apache Iceberg
##### Schema evolution
Cymbal's data requirements change constantly. Iceberg lets them evolve their data schemas, such as adding new columns or renaming existing ones, without disrupting existing data or applications.

##### Hidden partitioning
Iceberg automatically manages how data is partitioned for efficient querying, which means Cymbal's analysts do not need to worry about the underlying file organization.

##### Time travel
This feature allows Cymbal to query past versions of their data. If a report was run last month, they can reproduce the exact data state from that time, which is invaluable for auditing and debugging.

##### Atomic transactions
Iceberg enables reliable, concurrent operations on the data, ensuring that multiple processes can read and write to the same tables without data corruption.

By using Apache Iceberg with Cloud Storage, Cymbal can treat their collection of data files as performant, queryable tables, bringing the benefits of a data warehouse to their flexible data lake.