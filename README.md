# **Healthkart-Dashboard**

## **Overview**

This project demonstrates how to simulate data for influencer marketing campaigns and build an interactive **Power BI Dashboard** to track key performance metrics such as **Total Revenue**, **Total Spend**, **Return on Ad Spend (ROAS)**, and more. The dashboard provides insights into the effectiveness of influencer campaigns across various platforms and products.

## **Objective**

The goal of this project is to:

* **Generate synthetic data** for influencer campaigns, posts, tracking data, and payouts.
* **Analyze the data** using Power BI to track **ROI (ROAS)**, **performance over time**, and **influencer effectiveness**.
* **Generate insights** such as top influencers, most purchased products, and influencer payouts.

---

## **Project Structure**

1. **Data Generation**: The data is simulated using **Python** and the **Faker** library. Synthetic data includes influencers, their posts, campaign performance data, and payout details.
2. **Power BI Dashboard**: The data is then imported into **Power BI**, where relationships are set up, and key performance metrics are calculated using DAX. Interactive visualizations show trends, insights, and comparisons.
3. **Dashboard Insights**: The final dashboard presents metrics such as:

   * Total Revenue
   * Total Spend
   * Incremental ROAS
   * Top Influencers by Revenue
   * Most Purchased Products

---

## **Data Generation**

### **Data Generation with Python**

The dataset is generated using Python, with the following key attributes:

* **Influencers**: Simulated with attributes like ID, name, category, gender, follower count, and platform.
* **Posts**: Each influencer has posts with details like platform, date, URL, reach, likes, and comments.
* **Tracking Data**: Contains data such as source, campaign, product, orders, and revenue for each influencer's post.
* **Payouts**: Simulated payouts based on posts or orders, showing the total payout per influencer.

### **Dependencies**

To run the Python data generation script, install the required dependencies:

```bash
pip install faker pandas
```

### **Python Code to Generate Data**

```python
from faker import Faker
import pandas as pd
import random

# Initialize Faker instance
fake = Faker()

# Generate Influencers
influencers = []
for i in range(1, 11):
    influencers.append({
        'influencer_id': i,
        'name': fake.name(),
        'category': fake.word(),
        'gender': random.choice(['Male', 'Female']),
        'follower_count': random.randint(50000, 1000000),
        'platform': random.choice(['Instagram', 'YouTube', 'Twitter'])
    })

influencers_df = pd.DataFrame(influencers)

# Generate Posts
posts = []
for influencer in influencers:
    for i in range(1, 4):
        posts.append({
            'influencer_id': influencer['influencer_id'],
            'platform': influencer['platform'],
            'date': fake.date_this_year(),
            'URL': fake.url(),
            'caption': fake.sentence(),
            'reach': random.randint(10000, 20000),
            'likes': random.randint(200, 500),
            'comments': random.randint(50, 150)
        })

posts_df = pd.DataFrame(posts)

# Generate Tracking Data
tracking_data = []
for influencer in influencers:
    for i in range(1, 4):
        tracking_data.append({
            'source': random.choice(['Facebook', 'Instagram', 'YouTube']),
            'campaign': f'Campaign {random.choice(["A", "B", "C", "D"])}',
            'influencer_id': influencer['influencer_id'],
            'user_id': random.randint(100, 200),
            'product': random.choice(['MuscleBlaze', 'HKVitals', 'Gritzo']),
            'date': fake.date_this_year(),
            'orders': random.randint(1, 50),
            'revenue': random.randint(1000, 5000)
        })

tracking_df = pd.DataFrame(tracking_data)

# Generate Payouts
payouts = []
for influencer in influencers:
    payouts.append({
        'influencer_id': influencer['influencer_id'],
        'basis': random.choice(['post', 'order']),
        'rate': random.randint(100, 500),
        'orders': random.randint(10, 30),
        'total_payout': random.randint(1000, 10000)
    })

payouts_df = pd.DataFrame(payouts)

# Save data to CSV
influencers_df.to_csv('influencers.csv', index=False)
posts_df.to_csv('posts.csv', index=False)
tracking_df.to_csv('tracking_data.csv', index=False)
payouts_df.to_csv('payouts.csv', index=False)
```

---

## **Power BI Dashboard**

### **1. Import Data into Power BI**

* Open **Power BI Desktop**.
* Go to **Home** > **Get Data** > **Text/CSV**.
* Import the following CSV files:

  * `influencers.csv`
  * `posts.csv`
  * `tracking_data.csv`
  * `payouts.csv`
* Click **Load** to load the data into Power BI.

### **2. Create Relationships**

* Go to the **Model** view and create relationships between the tables based on `influencer_id`:

  * **Influencers** <-> **Posts**
  * **Influencers** <-> **Tracking Data**
  * **Influencers** <-> **Payouts**

### **3. Create Calculated Measures**

* **Total Revenue**:

  ```DAX
  Total Revenue = SUM(TrackingData[revenue])
  ```
* **Total Spend**:

  ```DAX
  Total Spend = SUMX(Payouts, Payouts[rate] * Payouts[orders])
  ```
* **ROAS**:

  ```DAX
  ROAS = DIVIDE([Total Revenue], [Total Spend])
  ```

### **4. Create Visualizations**

* **Bar Charts** for **Top Influencers by Revenue** and **Most Purchased Products by Users**.
* **Line Chart** for **ROAS over Time**.
* **Pie Charts** for **Performance by Platform** and **Influencers by Gender**.
* **KPIs** to display **Total Revenue**, **Total Spend**, and **Incremental ROAS**.

---

## **Insights from the Dashboard**

### **Top Influencers by Revenue**

This visualization ranks influencers based on the total revenue they generated. Key insights include identifying the top-performing influencers, like **Christina Camacho** and **Julia Bennett**, who drive the most revenue.

### **ROAS Over Time**

This line chart helps track the efficiency of campaigns by comparing **ROAS** over several months. It shows trends in campaign effectiveness, helping identify opportunities to improve return on ad spend.

### **Most Purchased Products by Users**

By analyzing the number of orders for each product, this chart reveals which products are driving the most sales. **Gritzo** emerged as the top-performing product.

### **Influencer Payout Analysis**

This table provides a detailed analysis of payouts per influencer based on posts or orders. **Brian Johnson** and **Chelsea Murray** stand out in terms of payout, with a higher number of orders or posts.

### **Platform Performance**

This pie chart breaks down campaign performance across platforms (e.g., **YouTube** vs **Twitter**), helping marketers decide where to allocate future resources.

### **Gender Distribution of Influencers**

This chart shows the gender distribution of influencers. The analysis can help ensure diversity in future campaigns and reveal any skewed trends toward male or female influencers.

---

## **Links to Project Resources**

* **Power BI Dashboard**: [Dashboard Link](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/Healthkart%20Dashboard.pdf)
* **CSV Files**:

  * [Influencers Data](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/influencers.csv)
  * [Posts Data](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/posts.csv)
  * [Tracking Data](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/tracking_data.csv)
  * [Payouts Data](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/payouts.csv)
* **Data Model**: [Data Model Explanation](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/Data%20Model.png)

---

### **Conclusion**

This project showcases how to simulate influencer campaign data and build a Power BI dashboard for actionable insights on campaign performance, influencer effectiveness, and product sales. The dashboard provides valuable tools to optimize future influencer marketing strategies.

---
