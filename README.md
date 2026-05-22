# 🚀 JMeter Performance Testing for Dmoney API

[![JMeter](https://img.shields.io/badge/Apache%20JMeter-5.6.3-C73A3A.svg?style=flat-square&logo=apachejmeter)](https://jmeter.apache.org/)
[![Java](https://img.shields.io/badge/Java-JDK%208+-007396.svg?style=flat-square&logo=openjdk)](https://oracle.com/java)
[![GitHub](https://img.shields.io/badge/Repository-GitHub-181717.svg?style=flat-square&logo=github)](https://github.com/Fahadhossain99/jmeter-performance-testing)
[![SQA](https://img.shields.io/badge/SQA-Performance%20Testing-blue.svg?style=flat-square)](https://github.com/Fahadhossain99/jmeter-performance-testing)

A comprehensive **JMeter Performance Testing Suite** for the simulated digital wallet **Dmoney API**. This project evaluates system stability, throughput, and latencies under concurrent thread loads, mimicking real-world customer and agent transaction flows.




## ⚙️ Performance Test Scenarios

The suite simulates high-traffic transaction flows using dynamic CSV datasets, random transaction variables, and automated verification flows.

### 👥 Thread Groups & Load Profile

All scenarios are executed concurrently with the following thread configuration:

| Scenario Name | Target flow description | Threads (Users) | Ramp-Up (Sec) | Loop Count | Dataset Source |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **1. Agent Deposit** | Agent logins, OTP validation, and deposit into customer accounts. | `5` | `120` | `2` | [`deposit.csv`](Resources/deposit.csv) |
| **2. Send Money** | Customer logins, OTP verification, and money transfer to other customers. | `5` | `120` | `2` | [`sendMoney.csv`](Resources/sendMoney.csv) |
| **3. Merchant Payment**| Customer logins, OTP verification, and merchant payment transactions. | `5` | `120` | `2` | [`payment.csv`](Resources/payment.csv) |

---

## 📊 Summary of Performance Metrics (Run Statistics)

Based on the performance metrics extracted from the test run execution (`Reports/statistics.json`):

| Transaction Name | Samples | Success Rate | Mean Latency (ms) | Min Latency (ms) | Max Latency (ms) | Throughput (req/sec) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Customer Login** | `10` | `100%` | `61.00 ms` | `19.0 ms` | `212.0 ms` | `0.092 / sec` |
| **Payment Amount** | `10` | `0%` | `7.30 ms` | `2.0 ms` | `52.0 ms` | `0.098 / sec` |
| **Verify OTP Request** | `10` | `0%` | `21.50 ms` | `5.0 ms` | `53.0 ms` | `0.097 / sec` |
| **Read OTP from Gmail** | `10` | `0%` | `0.00 ms` | `0.0 ms` | `0.0 ms` | `0.097 / sec` |
| **Total Suite** | **40** | **25%** | **22.45 ms** | **0.0 ms** | **212.0 ms** | **0.330 / sec** |

> [!NOTE]
> *The 100% error rate observed in OTP reading, OTP verification, and Payment Amount transactions is expected due to the test environment sandbox token limits and the simulation of OTP configurations.*

---

## 📊 Performance Testing Dashboards

Visual representations of test executions generated directly by the JMeter HTML Report Generator:

### 📈 HTML Report Dashboard Overview
*Aggregated success ratios and transactional breakdown:*

![HTML Report Dashboard](screenshots/HTML%20Reports.JPG)

### 📊 Summary Report
*Execution metrics including standard error rates and throughput:*

![Summary Report](screenshots/Summary%20Report.JPG)

### 📉 Aggregate Report
*High-precision latency analysis showing standard percentiles (90%, 95%, 99% response lines):*

![Aggregate Report](screenshots/Aggregate%20Report.JPG)

---

## 🛠️ Installation & Execution Guide

Follow these instructions to clone, open, and execute the performance suite locally.

### 📋 Prerequisites
* **Java**: JDK 8 or higher installed and configured in system path.
* **JMeter**: [Apache JMeter 5.6.x](https://jmeter.apache.org/download_jmeter.cgi) or higher.

### 🏃 Running via JMeter GUI
1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/Fahadhossain99/jmeter-performance-testing.git
   ```
2. Open **Apache JMeter**.
3. Go to `File` > `Open` and select the `dmoney.jmx` file from the root folder.
4. Click the **Start (Green Triangle)** button to run the test suite. All CSV configurations use relative paths and will load automatically.

### 🖥️ Running via Command Line (CLI Mode)
To avoid GUI resource overhead and get high-accuracy performance measurements, run the test plan from your terminal:

```bash
jmeter -n -t dmoney.jmx -l report.jtl -e -o Reports/
```

* **`-n`**: Specifies non-GUI mode.
* **`-t`**: Path to the source `.jmx` test plan.
* **`-l`**: Name of the JTL file to log results.
* **`-e`**: Generates a rich HTML report dashboard after execution.
* **`-o`**: Output folder where the dashboard will be written.

---

## 🛡️ License
Distributed under the MIT License. See `LICENSE` for more information.
