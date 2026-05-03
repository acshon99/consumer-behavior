# Consumer Shopping Behavior & Preference Study (2026)

This repository showcases an in-depth analysis of consumer shopping behavior and preferences, utilizing a simulated dataset that combines demographic information, digital habits, shopping patterns, and other relevant factors. The study aims to explore trends in the rapidly growing e-commerce landscape, understanding how consumers choose between online, physical stores, or a hybrid approach.

## Dataset Overview

The dataset consists of 11,789 records and 25 features, providing a rich source of information for understanding consumer choices. Key features include:

-   **Demographics:** `age`, `monthly_income`, `gender`, `city_tier`
-   **Digital Habits:** `daily_internet_hours`, `smartphone_usage_years`, `social_media_hours`, `online_payment_trust_score`, `tech_savvy_score`
-   **Shopping Patterns:** `monthly_online_orders`, `monthly_store_visits`, `avg_online_spend`, `avg_store_spend`
-   **Behavioral Scores:** `discount_sensitivity`, `return_frequency`, `delivery_fee_sensitivity`, `free_return_importance`, `product_availability_online`, `impulse_buying_score`, `need_touch_feel_score`, `brand_loyalty_score`, `environmental_awareness`, `time_pressure_level`
-   **Target Variable:** `shopping_preference` (Online, Store, Hybrid)

### Data Preprocessing

-   No missing values were identified.
-   Categorical features (`gender`, `city_tier`, `shopping_preference`) were one-hot encoded for machine learning compatibility.

## Exploratory Data Analysis (EDA)

The EDA phase involved visualizing distributions, correlations, and segmenting consumers based on their shopping preferences. Key findings include:

-   **Consumer Characteristics by Shopping Preference:**
    -   "Store" shoppers constituted the largest group.
    -   "Online" shoppers exhibited higher tech-savviness, online payment trust, and online spending.
    -   "Store" shoppers showed a preference for physical interaction.
    -   Age and income had only minor variations across shopping preference groups.

-   **Influence of Demographics on Spending:**
    -   Age, monthly income, and city tier showed minor impacts on average online or in-store spending, suggesting they are not strong primary predictors.

-   **Digital Engagement & Buying Behaviors:**
    -   Negligible linear correlations were found between digital engagement metrics (`daily_internet_hours`, `social_media_hours`) and `impulse_buying_score` or `online_payment_trust_score`.

-   **Key Factor Variation:**
    -   Online shoppers were less sensitive to discounts and returns but more sensitive to delivery fees.
    -   Variations across city tiers were generally minor.

-   **Behavioral Scores & Demographics:**
    -   Younger consumers (18-24) scored higher in tech-savviness, impulsivity, and environmental awareness.
    -   Brand loyalty peaked within middle-aged demographic groups.

**Visualizations:** The analysis includes various plots such as histograms of key numerical features, scatter plots showing spending patterns by shopping preference, correlation heatmaps, and bar plots illustrating average spending and behavioral scores by age, income, and city tier.

## K-Means Clustering for Consumer Segmentation

K-Means clustering was applied to identify natural groupings among consumers. After scaling the features, the Elbow Method suggested 3 or 4 clusters as potentially optimal.

-   **Evaluation:** Both `k=3` and `k=4` models resulted in low Silhouette Scores (around 0.028) and high Davies-Bouldin Indices, indicating poor cluster separation and significant overlap. This was further reinforced by PCA visualizations.
-   **Conclusion:** While some average characteristics could be observed per cluster, the segments were not distinctly separated, suggesting the current feature set may be insufficient for robust customer segmentation.

## Regression Models

Regression models (Linear Regression and Random Forest Regressor) were developed to predict various spending and frequency metrics.

### 1. Predicting Average Online Spend

-   **Outcome:** Both models performed poorly, yielding negative R-squared values, indicating they were less effective than predicting the mean. `monthly_income` and `avg_store_spend` were identified as important features by Random Forest, but were insufficient for accurate predictions.

### 2. Predicting Total Monthly Spend

-   A new target `total_monthly_spend` (`avg_online_spend + avg_store_spend`) was created.
-   **Outcome:** Linear Regression achieved an R-squared of 0.1277, and Random Forest 0.1129. This indicates a modest predictive capability, but a significant amount of variance remains unexplained.

### 3. Predicting Total Monthly Purchase Frequency

-   The target `total_purchase_frequency` (`monthly_online_orders + monthly_store_visits`) was introduced.
-   **Outcome:** Both models performed very poorly, with R-squared values near zero or negative, indicating an inability to effectively predict purchase frequency with the given features.

### 4. Predicting Customer Lifetime Value (CLTV) Proxy

-   A simplified CLTV proxy was defined as `total_monthly_spend * total_purchase_frequency`.
-   **Outcome:** Regression models showed very poor performance with negative R-squared values, suggesting that this CLTV proxy cannot be reliably predicted by the current feature set.

## Conclusion & Recommendations

The dataset proves valuable for **descriptive analysis** and **hypothesis generation**, offering valuable insights into consumer characteristics and behaviors. However, its current features are **insufficient for robust predictive modeling** or distinct customer segmentation using the explored methodologies.

### Potential Missing Features:

To improve predictive capabilities and segmentation accuracy, the following additional features would be beneficial:

-   Granular purchase history (items bought, categories, timestamps)
-   Psychographic data (values, attitudes, interests, lifestyles)
-   Detailed behavioral data (website clicks, app usage, browsing patterns)
-   External factors (economic conditions, seasonal trends, marketing campaigns)

### Actionable Recommendations:

1.  **Marketing Strategy:**
    -   Target "Online" shoppers with personalized digital campaigns emphasizing convenience and product availability.
    -   Engage "Store" shoppers with in-store experiences and tailored recommendations based on their preference for physical interaction.

2.  **Product Development:**
    -   Leverage insights into tech-savviness, impulse buying, and environmental awareness across different age groups to customize product features and messaging.

3.  **Data Strategy:**
    -   Prioritize enhancing data collection to include more granular purchase data, comprehensive psychographic profiles, and detailed digital behavioral metrics. This will significantly improve the accuracy of predictive models and the effectiveness of customer segmentation.
