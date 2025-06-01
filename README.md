# Identifying Merchants Likely to Adopt a Subscription Product

# Objective

The goal of this project is to identify **existing merchants who are not currently using the Subscriptions product** but are likely to adopt it if proactively targeted by marketing or sales campaigns.

---

# Data Sources

Two datasets were provided:

1. **Payments Dataset**  
   - Daily merchant-level volume split by product type:  
     - Subscriptions  
     - Checkout  
     - Payment Links  

2. **Merchants Dataset**  
   - Metadata about each merchant, including:  
     - Signup date  
     - Region  
     - Company size  
     - Industry  

# Filtering Criteria

After cleaning and aggregating the data, I narrowed the focus to a high-potential group of merchants based on the following logic:

- Are **active** (at least one transaction in the last 30 days)  
- Have **never used Subscriptions**  
- Show **regular engagement** (volume recorded on multiple days)  
- Have a **high average daily volume**, indicating recurring or predictable revenue  

This approach was designed to surface merchants who might already be handling repeat billing manually and could benefit from streamlining it with a subscription-based product.

---

# Analytical Approach

The solution was structured in three core phases:

### 1. Behavioral Clustering

Performed K-Means clustering to segment merchants by behavioral signals:

- `subscription_share` and `checkout_share`: Usage patterns across product types  
- `avg_volume_per_day`: Business scale  
- `active_days`: Frequency of transactions  
- `days_since_last_active`: Recency  
- `merchant_age_days`: Tenure  

**Number of clusters (K)**: 6, determined using the elbow method to balance interpretability and granularity.

---

### 2. Composite Scoring System

Created a **composite merchant score** to prioritize high-potential accounts for targeting:

| Component                           | Weight |
|------------------------------------|--------|
| Inverse of `subscription_share`    | 40%   |
| Average daily volume               | 25%   |
| Number of active days              | 20%   |
| Recency (days since last activity) | 10%   |
| Merchant tenure (age)              | 5%    |

This scoring allowed for **ranking non-subscription merchants** within each cluster.


### 3. Target Merchant Identification

From the high-scoring cluster groups, I extracted the top 50 merchants most aligned with existing subscriber behaviors, based on:

- Similar product mix  
- Stable volumes  
- Strong engagement and recency  
- No current Subscriptions usage  

These merchants represent a **qualified audience** for the Subscriptions product team to pursue with targeted outreach.

---

## 🔍 Key Takeaways

- The most subscription-ready merchants are not necessarily the largest, but the most **consistent and engaged**.  
- Behavioral clustering revealed distinct merchant profiles — some with obvious subscription needs, others with purely transactional business models.  
- The **composite scoring framework** is scalable and adaptable to future use cases (e.g., cross-sell of other digital products).

---
