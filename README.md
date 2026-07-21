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
