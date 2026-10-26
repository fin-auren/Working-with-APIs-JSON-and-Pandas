# Summary of Notebook: Working with APIs, JSON, and Pandas

This notebook demonstrates how to interact with REST APIs, parse JSON structures (including nested data), and clean/normalize data using the Python `pandas` library.

## Table of Contents
1. **Basic Python Dictionaries (JSON Representation)**
2. **Requests and API Interaction**
3. **Analyzing and Parsing Nested JSON**
4. **Data Normalization & Cleaning with Pandas**
5. **API Queries with Query Parameters**

---

### 1. Basic Python Dictionaries (JSON Representation)
* **Simple Dictionaries (`O7txgzrtc2th`, `Yc-sBRRPjb5L`)**: Demonstrates how to access key-value pairs, lists (using indices), and nested structures within dictionary variables.
* **Nested Structures (`6fO3SCl1iyx-`)**: Illustrates accessing lists of dictionaries (such as transaction records) and specific nested attributes.

### 2. Requests and API Interaction
* **Fetching User Profiles (`gJIu2bYUkamE`, `UaXj4PsCsDL-`, `2u8Q81GosT3j`)**:
  * Requests multiple user objects from `https://jsonplaceholder.typicode.com/users` using `requests.get()`.
  * Uses `.json()` to parse responses directly.
  * Verifies response safety via `.status_code`.
* **Single Profile Retrieval (`VFbeZRJkrsk9`)**: Fetches details for a single user ID.

### 3. Analyzing and Parsing Nested JSON
* **Pretty Printing (`nSBQ508UqxJV`)**: Utilizes `json.dumps(data, indent=2)` to easily inspect complex, nested JSON objects.
* **Iterating through Data (`4qMGfraHsi95`)**: Demonstrates looping through a parsed API JSON response list to extract and display specific values (e.g., Name, Email, and City).

### 4. Data Normalization & Cleaning with Pandas
* **Standard DataFrame conversion (`76vBmrc0s3kl`)**: Creates a DataFrame directly from nested dictionaries, leaving complex dictionaries inside the cells.
* **Flattening Data (`MMR0wohFtkAy`)**: Uses `pandas.json_normalize()` to flatten nested JSON structures (like `address` and `company`) into individual, separate columns.
* **DataFrame Cleaning and Renaming (`GOamTnCiuzM2`, `TC_ANAFMwf_7`, `K0v-fPPxw3dt`)**:
  * Filters relevant columns.
  * Renames columns to match snake_case conventions.
  * Formats UNIX timestamps into readable Datetime objects using `pd.to_datetime()`.

### 5. API Queries with Query Parameters
* **Bitcoin Market Charts (`qP_Siv24xOUy`, `KMt8kx-iyWtc`)**:
  * Performs a GET request using query parameters (`params`) to retrieve the 30-day historical chart of Bitcoin prices via CoinGecko's API.
  * Extracts main JSON keys (`prices`, `market_caps`, `total_volumes`).
 
# 📋 Reconciliation Notebook Summary

This notebook demonstrates a **Payment Reconciliation Process** between an **Internal Ledger** (what our system recorded) and a **Gateway Export** (what the external payment gateway reported).

---

## 🔍 1. Data Generation & Setup
* **Internal Ledger Generation (`internal_ledger`):** Generated a synthetic dataset of **100 transactions** (`TXN01001` to `TXN01100`) with various transaction amounts, payment methods (UPI, CC, Wallet, NetBanking), timestamps, and a status of `'SUCCESS'`.
* **Gateway Export Simulation (`gateway_export`):** Created by duplicating the internal ledger and introducing anomalies to simulate real-world discrepancies:
  1. **Missing Transactions:** Removed 5 random transactions.
  2. **Amount Mismatches:** Deducted arbitrary fees (₹10, ₹20, ₹50, or ₹100) from 3 random transactions.
  3. **Extra Transactions:** Appended 2 unrecognized dummy transactions (`TXN99901` and `TXN99902`).
  4. **Status Mismatches:** Changed the status of 2 transactions from `'SUCCESS'` to `'FAILED'`.

---

## 🛠️ 2. Reconciliation & Discrepancy Analysis

By comparing the two datasets, we identified and isolated three major classes of discrepancies:

### A. Missing Transactions in Gateway
* **Identified:** 5 transactions exist in our internal ledger but are missing from the gateway report:
  * `TXN01006`, `TXN01038`, `TXN01056`, `TXN01071`, `TXN01098`
* **Financial Risk:** Total value at risk is **₹3,095**.

### B. Amount Mismatches
* **Identified:** 3 transactions where the recorded amount does not match the settled gateway amount due to transaction fees:
  * `TXN01066` (₹599 vs. ₹549 | Diff: ₹50)
  * `TXN01077` (₹699 vs. ₹689 | Diff: ₹10)
  * `TXN01084` (₹699 vs. ₹689 | Diff: ₹10)
* **Discrepancy Total:** **₹70.0**

### C. Status Mismatches (Critical)
* **Identified:** 2 transactions that our system marked as `SUCCESS` but the gateway marked as `FAILED`:
  * `TXN01004` (₹799)
  * `TXN01050` (₹349)

---

## 🎯 Summary Comparison
| Metric | Internal Ledger | Gateway Export |
| :--- | :--- | :--- |
| **Transaction Count** | 100 | 97 |
| **Total Amount** | ₹51,450 | ₹48,285 |
