# Logistics_Assistant
An end-to-end real-time event logistics assistant with Kafka, Spark Streaming, and Airflow, integrating traffic APIs and automated workflows to dynamically adjust user participation in events


<img width="1243" height="336" alt="image" src="https://github.com/user-attachments/assets/e3c3769c-40bb-45a5-857a-0929b2bcd6e4" />


# Real-Time Event Assistant

This project simulates a system that helps users manage events and meetings based on live traffic conditions. The goal is to demonstrate how streaming data pipelines and workflow orchestration can be used to make automated decisions in real time.

## Architecture Overview

The pipeline is designed around three main steps:

1. **Streaming ingestion and processing** of traffic data and user trip details.
2. **Workflow decisions** triggered when a user is predicted to be late.
3. **Notifications and storage** so the system can react in real time and keep a record for later analysis.

### Components

* **Users and Traffic API**
  Users provide their current location, event details, and start times. A traffic API (Google Maps, HERE, or mocked data) supplies live traffic updates.

* **Kafka (Event Stream)**
  Acts as the ingestion layer for both user trips and traffic events. This creates a continuous stream of data rather than one-off batch jobs.

* **Spark Structured Streaming**
  Consumes events from Kafka and calculates ETAs for each user. It flags cases where the predicted arrival time exceeds the scheduled start time.

* **Airflow (Workflow Decisions)**
  Orchestrates the downstream logic. When a late arrival is detected, Airflow checks event metadata to see if an online variant exists. Based on this, it either sends the user a meeting link or notifies the organizer.

* **Event Metadata Database**
  Stores information about each event, such as whether an online variant is available and the relevant link.

* **Notifications**
  If the event has an online variant, the system emails or messages the user. If not, the organizer receives a reschedule request.

* **Warehouse and Dashboard**
  All processed ETAs and outcomes are stored in a warehouse (e.g., Postgres, BigQuery). A dashboard (Superset, Grafana) provides visibility into user trips, on-time arrivals, and late cases.

## Why This Project

The intent here is not to create a production-ready scheduling service but to showcase end-to-end data engineering skills:

* Building a real-time streaming pipeline with Kafka and Spark.
* Designing workflow branching with Airflow.
* Integrating external APIs and notification systems.
* Exposing processed data for monitoring and analysis.

The system shows how data engineering tools can be combined to solve real-time, user-facing problems.
