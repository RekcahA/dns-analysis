# DNS-Based Malware Detection via Statistical Analysis

This project presents a approach to differentiating malicious DNS traffic from benign traffic using statistical techniques on parameters such as TTL, RTT, entropy, and TLD distribution. Built upon real-world datasets and robust preprocessing methods, this research offers actionable insights for cybersecurity operations and incident response.

---

## Table of Contents

- [Overview](#overview)
- [Abstract](#abstract)
- [Features](#features)
- [Methodology](#methodology)
- [Installation](#installation)

---

## Overview

Malware has evolved to exploit even the most unassuming network protocols—DNS being a prime example. While most network protocols are now encrypted, DNS remains an open protocol that malware often uses for covert command-and-control (C&C) communication. This project leverages statistical analysis of DNS query parameters to identify behavioral differences between malicious and benign traffic.

By analyzing key variables such as:
- **Time To Live (TTL)**
- **Round Trip Time (RTT)**
- **Information Entropy**
- **Top-Level Domain (TLD) patterns**

we provide a framework that can help cybersecurity professionals develop proactive detection mechanisms against malware, botnets, and DGA-based attacks.

---

## Abstract

The research analyzes DNS query characteristics collected over a six-year period from two datasets:
- **Malware Dataset:** Derived from 1,000 malware-related PCAP files resulting in 256,449 DNS queries.
- **Normal Dataset:** Comprised of 1 Million benign DNS queries from the Cisco Umbrella Popularity List.

By comparing statistical behaviors such as TTL, entropy, and TLD distribution, the study identifies key indicators that differentiate malware-induced DNS traffic from benign traffic. The findings lay the groundwork for refined detection techniques that avoid computationally expensive deep packet inspection while leveraging the inherent transparency of DNS traffic.

---

## Features

- **Statistical Analysis:** Evaluate DNS traffic based on TTL, RTT, entropy, and response codes.
- **Data Preprocessing:** Convert raw PCAP files into structured JSON format using Zeek and Python.
- **PySpark Integration:** Utilize Apache Spark for large-scale data cleaning and analysis.
- **DGA Detection:** Compute domain information entropy to distinguish algorithmically generated domains from human-readable ones.
- **Visualization:** Generate before-and-after cleaning plots and analysis graphs.

---

## Methodology

The project follows a multi-step approach:

1. **Data Collection:**
   - **Malware Dataset:** PCAP files from [malware-traffic-analysis.net](https://malware-traffic-analysis.net).
   - **Normal Dataset:** 1 Million most-queried domains from Cisco Umbrella’s Popularity List.
   
2. **Data Preprocessing:**
   - **Zeek Processing:** Extract DNS transaction details into JSON.
   - **TLD Extraction:** Use `icannTLD` Zeek plugins and the Python library `tldextract` to accurately parse FQDN components.
   - **Entropy Calculation:** Compute the entropy for each DNS query to differentiate DGA traffic from normal traffic.
   
3. **Data Cleaning and Analysis:**
   - Use **PySpark** to merge, clean, and analyze the datasets.
   - Remove duplicates and queries present in both datasets to isolate distinctive characteristics.
   - Split the cleaned data into separate DataFrames for TTL, RTT, and entropy analysis.
   
4. **Statistical Evaluation:**
   - Compare median ranges, quartiles, and other statistical measures to establish classification criteria for future DNS queries.

The Python code in this repository implements these steps to produce actionable insights for distinguishing malicious from benign DNS traffic.

---

## Installation

### Prerequisites

- **Python 3.8+**
- **Apache Spark** (with PySpark)
- **Zeek Network Security Monitor**
- **Required Python Libraries:**
  - `pyspark`
  - `tldextract`
  - `matplotlib` (for plotting)
  - `numpy`
  - `pandas`
  
### Setup Instructions

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/dns-malware-detection.git
   cd dns-malware-detection
   ```

2. **Create a Virtual Environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate
   ```

3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure Zeek:**
   - Ensure Zeek is installed and properly configured to process your PCAP files.
   - Customize the Zeek scripts if necessary to enable JSON output and entropy calculations.
