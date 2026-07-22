# Stephane-Maarek-Udemy-course---Cloud-associate
Course notes
AWS Certified Solutions Architect Associate - Course Synopsis (Sections 1–7)
Overview
This repository contains notes, code snippets, and hands-on lab summaries covering the foundational and core infrastructure modules of the Ultimate AWS Certified Solutions Architect Associate course. Below is a detailed synopsis of the first seven sections.

Section 3: Getting Started with AWS
AWS Global Infrastructure: Explored the layout of AWS Regions, Availability Zones (AZs), Data Centers, and Edge Locations designed for high availability and low latency.

Console Navigation: Mastered the AWS Management Console UI layout, resource grouping, and global vs. regional service scopes.

Section 4: IAM & AWS CLI
Identity and Access Management (IAM): Configured users, groups, and managed/inline policies following the principle of least privilege.

Security Hardening: Implemented Multi-Factor Authentication (MFA) and enforced secure password policies.

Roles vs. Users: Created IAM roles for AWS services to securely delegate permissions without sharing long-term credentials.

AWS Access & Tooling: Configured programmatic access using Access Keys, set up the AWS CLI locally across environments, and utilized AWS CloudShell for shell-based cloud management.

Section 5: EC2 Fundamentals
Elastic Compute Cloud (EC2) Basics: Launched, configured, and terminated EC2 instances utilizing custom User Data scripts to bootstrap web servers.

Instance Types & Families: Evaluated compute, memory, and storage optimized classes to match workload demands.

Networking & Security: Secured instances using Security Groups, managed inbound/outbound rules, and established secure remote shell connections via SSH and EC2 Instance Connect.

Purchasing Options: Analyzed cost efficiencies across On-Demand, Reserved Instances, Savings Plans, Spot Instances, and Spot Fleets.

Section 6: EC2 - Solutions Architect Associate Level
IP Addressing: Differentiated between Public IP addresses, Private IP addresses, and static Elastic IPs.

Advanced Placement: Deployed EC2 Placement Groups (Cluster, Spread, and Partition) to optimize high-performance computing, fault tolerance, and workload isolation.

Network & State Management: Configured Elastic Network Interfaces (ENIs), secondary private IPs, and utilized EC2 Hibernate to preserve in-memory state during stop/start cycles.

Section 7: EC2 Instance Storage
Amazon EBS (Elastic Block Store): Explored block-level storage volumes, persistent snapshots, and multi-attach capabilities.

EBS Volume Types: Evaluated performance characteristics across General Purpose SSD (gp2/gp3), Provisioned IOPS SSD (io1/io2), and Throughput Optimized HDD (st1).

Storage Alternatives: Compared ephemeral EC2 Instance Store performance with shared file systems using Amazon EFS (Elastic File System) via NFS.

AMIs (Amazon Machine Images): Built and packaged custom golden images for rapid environment scaling and disaster recovery.Section 8: High Availability and Scalability - ELB & ASG Recap
Here is a comprehensive recap of the core concepts, load balancer variations, and scaling mechanisms covered in this section of your course:

1. High Availability & Scalability Foundations
High Availability (HA): Ensuring your system is continuously operational and accessible with minimal downtime, typically achieved by spreading resources across multiple Availability Zones (AZs).

Scalability: The ability of an architecture to handle increased workloads by scaling out/in (adding or removing instances dynamically) or scaling up/down (changing instance sizes).

2. Elastic Load Balancing (ELB) Overview
ELB automatically distributes incoming application traffic across multiple targets, such as EC2 instances, containers, and IP addresses, across multiple Availability Zones.

Key Benefit: Enhances fault tolerance and ensures single points of failure are avoided.

Health Checks: Load balancers continuously monitor the health of registered targets and route traffic only to healthy instances.

3. Load Balancer Types & Use Cases
Load Balancer Type	OSI Layer	Key Features & Use Cases
Application Load Balancer (ALB)	Layer 7 (Application)	
• Best for HTTP/traffic routing.


• Supports advanced path-based and host-based routing (e.g., routing /users to one target group and /api to another).


• Supports WebSockets and SNI for multiple SSL certificates.

Network Load Balancer (NLB)	Layer 4 (Transport)	
• Ultra-high performance, capable of handling millions of requests per second with extremely low latency.


• Best for TCP, UDP, and TLS traffic.


• Retains the client's source IP address.

Gateway Load Balancer (GWLB)	Layer 3/4 (Network)	• Designed for deploying, scaling, and managing third-party virtual appliance security fleets (e.g., firewalls, deep packet inspection).
4. Advanced ELB Features
Sticky Sessions (Session Affinity): Binds a user's session to a specific target instance so that all requests from that user during the session are routed to the same backend server.

Cross-Zone Load Balancing: Ensures that load balancers distribute incoming traffic evenly across all registered targets across all enabled Availability Zones, regardless of how many instances are in each zone.

SSL/TLS Certificates & ACM: Integrates with AWS Certificate Manager (ACM) to terminate HTTPS traffic at the load balancer level, enabling secure communication and allowing HTTP-to-HTTPS redirects.

Connection Draining (De-registration Delay): Gives existing in-flight requests a configurable window of time to complete safely before an instance is deregistered or terminated for maintenance or scaling down.

5. Auto Scaling Groups (ASG)
Auto Scaling Groups ensure you have the correct number of EC2 instances running to handle the load of your application.

Core Components: Minimum capacity, maximum capacity, and desired capacity.

Self-Healing: Automatically replaces unhealthy instances detected by ELB health checks or EC2 status checks.

Launch Templates / Configurations: Defines the blueprint for new instances spawned by the ASG (AMI, instance type, security groups, key pairs).

6. ASG Scaling Policies
Target Tracking Policy: The simplest and most efficient policy; you specify a target metric (like maintaining an average CPU utilization or request count at 50%), and AWS manages the scaling adjustments automatically.

Simple & Step Scaling Policies: Triggered by CloudWatch alarms, allowing you to manually define exact adjustment steps (e.g., add 2 instances if CPU exceeds 80%).

Scheduled Scaling: Scales your ASG based on predictable time-based patterns (e.g., scale up every Monday morning at 8:00 AM).

8.Aurora Databases

I have scientific "databases" in mind, as in rows and collumns in excel

That makes perfect sense. When you are dealing with scientific data, you can absolutely think of a relational database like Aurora as a massive, highly structured Excel workbook. The tables are your spreadsheets, the columns are your variables, and the rows are your individual observations or sensor readings.

Here is how the Aurora Writer and Reader instances work together in a heavy scientific context.

The Scenario: Ecological Data Logging
Imagine you are maintaining a massive environmental database. Your "spreadsheet" has columns for Timestamp, Location, Observation_Type (e.g., water flow rate, temperature, or species sighted), and Value.

Over a 21-month research period, this table accumulates millions of rows of data.

1. The Writer Instance (The Data Logger)
In a scientific setup, you often have a constant stream of incoming data. You might have automated sensors pushing seasonal temperature changes and fixed flow rates into the database 24/7, while you are also manually appending new rows when you log a Cape Skink sighting or note the physical dimensions of a spindly 1mm red spider.

Its only job: The Writer instance acts like a person whose sole responsibility is to continuously scroll to the very bottom of your massive Excel sheet and type in new rows as fast as possible.

It does not analyze the data; it just catches the incoming telemetry and saves it to Aurora's underlying storage volume.

2. The Reader Instance (The Analyst)
Now, you need to analyze this data. You want to run a massive "pivot table" (a complex SQL SELECT query) to calculate the correlation between seasonal temperature shifts and nutrient uptake over an 11-month window.

Crunching millions of rows takes a massive amount of CPU and memory. If you ran this heavy analytical query on the Writer instance, the server could get overwhelmed. It might freeze up and drop incoming sensor data—meaning you lose valuable research data.

The Aurora Solution: You spin up a Reader instance.

Because Aurora uses a shared storage volume, the Reader instance looks at the exact same "Excel file" sitting on the hard drive as the Writer instance.

The Reader instance uses its own dedicated CPU and memory to crunch those millions of rows, apply your complex filters, and spit out the seasonal averages.

Why this architecture matters for science
If you need to run even heavier computations—say, cross-referencing your local biodiversity log against a decade of regional weather patterns—you don't have to upgrade your main database. You simply spin up three or four more Reader instances to divide up the analytical workload.

The Writer instance remains completely untouched, happily and safely appending new rows of data at the bottom of the sheet without ever slowing down.

OK, how wouldyou structure a writer database in a retail environment, or banking, or construction company. How many different types of databases does a company typically use

1. Structure of a Writer Database in Different Industries
In a production environment, the Writer Database (often called the Primary or Transactional database) handles the heavy lifting of OLTP (Online Transaction Processing)—meaning fast, concurrent inserts, updates, and deletes where data integrity is paramount.

Here is how a writer database is structured across different sectors:

Retail (e.g., E-Commerce / Inventory):

Structure: Highly normalized relational structure (3NF) to prevent data anomalies during high-velocity transactions.

Core Tables: Customers, Products, Orders, Order_Items, and Inventory_Stock.

Writer Focus: When a customer clicks "Buy," the writer database instantly opens a transaction, locks the specific stock row to prevent overselling, decrements the inventory count, creates the order record, and commits the payment status.

Banking (e.g., Core Ledger):

Structure: Exceptionally strict relational design bound by ACID (Atomicity, Consistency, Isolation, Durability) guarantees.

Core Tables: Accounts, Transactions, Ledger_Entries, and Customers.

Writer Focus: If money moves from Account A to Account B, the writer database ensures a strict dual-entry ledger transaction: it debits one and credits the other simultaneously. If any step fails, the entire transaction rolls back completely to prevent financial corruption.

Construction (e.g., Project & Resource Management):

Structure: Hybrid structure balancing relational operational data with document storage.

Core Tables: Projects, Subcontractors, Daily_Site_Logs, Material_Orders, and Invoices.

Writer Focus: Handles continuous operational data entry from field engineers logging daily material deliveries, equipment usage, or milestone sign-offs.

2. How Many Different Types of Databases Does a Company Typically Use?
A modern mid-to-large enterprise rarely relies on just one database. Instead, they use a polyglot persistence architecture—deploying several specialized database types tailored to specific workloads. A typical company uses 4 to 6 distinct database categories:

Relational Databases (SQL - e.g., PostgreSQL, MySQL, Amazon Aurora):

Purpose: The core system of record for structured business transactions (user accounts, orders, financial ledgers).

Key-Value / In-Memory Stores (e.g., Redis, Memcached):

Purpose: Ultra-fast, low-latency caching for session management, real-time leaderboards, or shopping cart states to take the load off the main writer database.

Document Databases (NoSQL - e.g., MongoDB, DynamoDB):

Purpose: Storing unstructured or semi-structured data where schemas change rapidly, such as user profile preferences, product catalogs with varying attributes, or IoT device telemetry logs.

Data Warehouses (e.g., Amazon Redshift, Snowflake, Google BigQuery):

Purpose: Analytical engines (OLAP) optimized for heavy reporting. Companies copy data from their transactional writer databases into the warehouse to run massive business intelligence queries without impacting daily customer-facing operations.

Search Engines (e.g., Elasticsearch, OpenSearch):

Purpose: Powering complex text searches, auto-complete features, and log analytics across massive text datasets.

Which companies are using this

Amazon Aurora is widely used by global enterprises across retail, finance, automotive, and technology to handle high-throughput workloads. Notable examples include:

Samsung: Migrated 1.1 billion user accounts across three continents from a legacy Oracle monolith to Amazon Aurora to support microservices and handle tens of thousands of requests per second.

BMW: Utilizes Amazon Aurora to scale its global customer messaging system (BMW Messages), processing millions of vehicle transaction logs and notifications during peak periods.

DoorDash: Adopted Amazon Aurora to scale its database infrastructure and manage massive order growth surges across its last-mile logistics platform.

Alloy: Employs Amazon Aurora Serverless to power its identity verification and fraud prevention platform, handling heavy transaction volume fluctuations for banks and financial tech companies.

Experian: Replaced legacy relational systems with Amazon Aurora to improve application performance, accelerate credit report refreshes, and cut replication lag.

Section 9: AWS Fundamentals: RDS + Aurora + ElastiCache
This section focuses on the core managed relational database and in-memory caching services available on AWS, detailing their architectures, scalability options, security mechanisms, and use cases for the Solutions Architect exam.

🔑 Key Architectural Concepts
1. Amazon RDS (Relational Database Service)
Overview & Engines: Fully managed relational database service supporting MySQL, PostgreSQL, MariaDB, Oracle, and Microsoft SQL Server.

RDS Read Replicas vs. Multi-AZ:

Read Replicas: Used for vertical read scalability. Operates via asynchronous replication to offload read workloads. Replicas can span cross-region for disaster recovery.

Multi-AZ: Used strictly for High Availability (HA) and Disaster Recovery (DR). Operates via synchronous replication to a passive standby instance in a different Availability Zone. The standby cannot accept active traffic.

RDS Custom: Provides administrative OS-level access and customization privileges for Oracle and Microsoft SQL Server to support legacy applications, custom patching, and specialized software configurations.

RDS Proxy: An elegant connection pooling solution that minimizes database connection overhead, increases application resiliency during database failovers, and bypasses poor application reconnection logic.

2. Amazon Aurora
Cloud-Native Design: AWS's custom, fully managed relational database engine featuring high-speed open-source compatibility (specifically MySQL and PostgreSQL).

Advanced Concepts & Scaling:

Aurora Serverless: Automatically starts up, scales compute capacity up or down based on unpredictable or intermittent traffic loads, and shuts down entirely when completely unused to maximize cost efficiency.

Aurora Database Cloning: Uses a copy-on-write protocol to instantly provision a new, independent, and writeable duplicate of a production cluster without copying physical data blocks, ideal for isolated testing environments.

3. Amazon ElastiCache
In-Memory Performance: Managed caching layer used to deliver sub-millisecond latencies for high-throughput workloads.

Engine Distinctions:

Redis: Highly available caching architecture supporting replication, multi-AZ configurations, persistence, and complex, native data types (e.g., Sorted Sets, which are the gold standard for real-time gaming leaderboards).

Memcached: Simple, multi-threaded key-value memory object store designed strictly for non-persistent caching without native data sorting or multi-AZ replication features.

🛡️ Security, Backup, & Operations
RDS Security: Managed via IAM Database Authentication (using short-lived tokens instead of permanent passwords), database security groups, and KMS keys for data at rest.

Encryption Migration: Database encryption status must match its underlying architecture. An unencrypted database cannot have encrypted replicas. Forcing encryption requires taking a manual snapshot, copying it with encryption enabled via KMS, and restoring a new instance.

Backup Strategy:

Automated Backups: Designed for short-term point-in-time recovery with a strict maximum retention ceiling of 35 days.

On-Demand Backups (Snapshots): Manual storage snapshots that persist indefinitely until explicitly deleted, serving compliance, multi-year auditing, and long-term DR archiving.
