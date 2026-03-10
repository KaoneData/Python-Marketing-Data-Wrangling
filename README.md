#  Python Data Wrangling: Marketing Campaign Cleaning

##  Project Overview
In real-world business environments, raw data is often "dirty"—containing typos, logical inconsistencies, and formatting errors. This project demonstrates advanced **Data Wrangling** and automation techniques using **Python (Pandas & NumPy)** to transform a messy marketing dataset into a high-integrity asset ready for ROI analysis and supply chain reporting.

---

##  Key Technical Highlights (Code Snippets)

### 1. Data Hygiene & Fuzzy Logic
I resolved categorical inconsistencies (e.g., "Gogle" vs "Google Ads") and handled mixed boolean formats ('Yes', 'Y', '1') using mapping dictionaries to ensure uniform data types.
```python
cleanup_map = {
    'Facebok': 'Facebook',
    'Gogle' : 'Google Ads',
    'Insta_gram' : 'Instagram',
    'E-mail' : 'Email'
}
df['channel'] = df['channel'].replace(cleanup_map)
```
## 2. Logical Integrity Audits
I implemented custom masks to identify "impossible" records (Clicks > Impressions) and fixed "Time Travel" errors where the end_date occurred before the start_date using automated offsets.
```python
# Fixing chronological errors using a 30-day corrective offset
time_travel_mask = df['end_date'] < df['start_date']
df.loc[time_travel_mask, 'end_date'] = df.loc[time_travel_mask, 'start_date'] + pd.Timedelta(days=30)
```
## 3. Outlier Management (Winsorization)
I calculated the Interquartile Range (IQR) to identify extreme spend outliers and capped them at the upper limit to prevent skewed averages in reporting.
```python
Q1 = df['spend'].quantile(0.25)
Q3 = df['spend'].quantile(0.75)
IQR = Q3 - Q1
upper_limit = Q3 + (3 * IQR)
df.loc[df['spend'] > upper_limit, 'spend'] = upper_limit
```
## 4. Feature Extraction (String Parsing)
Used string manipulation to extract the Season attribute from complex campaign naming conventions (e.g., extracting "Summer" from "Q1_Summer_Promo").
``` python
# Split the name by underscores and grab the second item (index 1)
df['season'] = df['campaign_name'].str.split('_').str[1]
```
### Why This is Business-Critical
**Data Integrity:** Prevents "impossible" metrics (like Clicks > Impressions) from reaching stakeholders.

**Automation:** Reduces manual data-prep time by over 80% through repeatable Python scripts.

**Reliability:** Ensures that supply chain and marketing KPIs (CTR, CPC, AOV) are based on a "Single Version of Truth".

### Project Structure
**Cleaning Script:** [View Python Notebook](marketing_data_wrangling.ipynb).

**Tech Stack:** Python 3.x, Pandas, NumPy.


## Author
**Kaone Edward**
* [LinkedIn](https://www.linkedin.com/in/kaone-edward-bbb820197/)
* [GitHub](https://github.com/KaoneData)

