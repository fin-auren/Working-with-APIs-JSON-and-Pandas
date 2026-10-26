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
