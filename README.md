# IIoT Threat Detection using PySpark

**University Project**: DC-DSE Assignment 2025/26 

**Author**: Mattia Di Luca (ID: 5213177) 

## Overview
As Industry 4.0 drives the exponential growth of IIoT devices, it simultaneously introduces critical security risks . This project aims to build a Machine Learning process to identify and classify malicious activity within these networks. To handle the high dimensionality and massive volume of network traffic, the project utilizes PySpark's distributed computing framework.

## Dataset
* **Name**: The project utilizes the Edge-IIoTset dataset.
* **Size**: The dataset is 1.22 GB.
* **Dimensions**: The data contains 2,219,201 rows and 63 columns.
* **Composition**: The dataset captures normal behavior and 14 types of complex attacks, including DDoS and SQL Injection.
* **Distribution**: The data exhibits a significant class imbalance with 72.8% Normal traffic versus 27.2% Attack traffic.

## Methodology
### 1. Data Processing and Cleaning
* Extracted 9 key features including TCP/HTTP/MQTT payloads and port information.
* Imputed missing values with 0.0.
* Computed new columns such as `Unified_Payload` and `Binary_Label` for further computation.

### 2. Exploratory Data Analysis
* Conducted data distribution and traffic volume analysis to identify class imbalances.
* Identified mechanical generation patterns in DDoS UDP and Port Scanning attacks due to zero payload volatility.
* Discovered extreme payload size and variance anomalies in MITM attacks, confirming active interception.

### 3. Supervised Classification
* Built a PySpark ML Pipeline utilizing `StringIndexer`, `VectorAssembler`, `StandardScaler`, and `LogisticRegression`.
* Achieved an overall Accuracy of 80.68%.
* Achieved a Weighted F1-Score of 73.80%.
* Concluded that the model is robust in filtering legitimate traffic but struggles with low-volume threats due to the dataset imbalance.

## Performance Evaluation
The PySpark application was executed in three configurations to evaluate scalability and resource utilization:
* **Local [1]**: Single-core execution timed out during the computational load of the ML task.
* **Local [*]**: Multi-core execution completed the full pipeline in approximately 231 seconds.
* **Cluster (YARN)**: Distributed execution completed the full pipeline in approximately 241 seconds.
* **Conclusion**: While the cluster provided faster raw computing power for the ML phase, the local multi-core setup was slightly faster overall due to the network overhead and data transfer latency associated with distributed environments.
