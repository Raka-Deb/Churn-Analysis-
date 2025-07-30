# Telecom Churn Analysis Report

## Project Overview
This report summarizes the findings from a comprehensive churn analysis conducted using Power BI on a telecom dataset. The primary objective was to understand customer churn behavior, identify key patterns, and provide actionable insights to reduce churn rates. Churn, in this context, refers to customers leaving the telecom provider for competitors (e.g., switching from Vodafone to Airtel due to better offers) or reducing their engagement (e.g., switching from postpaid to prepaid plans). The analysis encompasses business problem understanding, exploratory data analysis (EDA), data cleaning, and dashboard creation to visualize critical insights.


![image alt](https://github.com/Raka-Deb/Churn-Analysis-/blob/c725e10c043bdb76b9344a90a316d6f9efb0d27e/telecom%20churn.png)




The dataset used is a clean telecom churn dataset, designed for classification tasks with a binary churn indicator (churn vs. non-churn). The analysis focuses on both the overall customer population and the churned subset to uncover distinct characteristics and drivers of churn.

## Business Problem
Churn is a critical issue across industries, particularly in telecom, where customers may leave due to better competitor offers, dissatisfaction, or changing needs. The goal is to:
- Identify why customers churn (e.g., tariff plan changes, service dissatisfaction, or budget constraints).
- Quantify churn rates (e.g., a 10% monthly churn rate, with a target to reduce it to 5-6%).
- Provide insights to inform retention strategies, such as targeted offers or improved services.

### Types of Churn Identified
- **Competitor Churn**: Customers switching to another provider (e.g., from Vodafone to Airtel).
- **Tariff Plan Churn**: Moving from a higher-value plan (e.g., $500) to a lower-value plan (e.g., $100) due to budget constraints or alternative services like Wi-Fi.
- **Service Churn**: Discontinuing specific services, such as caller tunes or weekly subscriptions.
- **Product Churn**: Transitioning from postpaid to prepaid, reducing guaranteed revenue for the company.
- **Usage Churn**: Decreased service usage, potentially indicating a precursor to complete churn.

### Customer Decision Cycles
Customers were categorized based on their churn behavior:
- **Inert Subscribers**: Customers who consider churning but remain due to complex processes or inertia.
- **Unconditionally Loyal**: Customers who stay because they are satisfied with the provider.
- **Contract-Bound**: Customers who cannot churn due to contractual obligations.
- **Conditionally Loyal**: Customers who have considered churning but stay to evaluate future offers.
- **Conditional Churners**: Customers who churn due to changing needs or better offers.
- **Lifestyle Migrators**: Customers who frequently switch providers due to dissatisfaction or preference for novelty.
- **Unsatisfied Churners**: Customers who leave due to poor experiences or unmet expectations.

### Data Science Approach
The churn analysis followed a structured data science workflow:
1. **Capture and Analyze**:
   - Collect and clean data.
   - Conduct EDA to identify patterns and data quality issues.
   - Aggregate and standardize data for analysis.
2. **Report and Predict**:
   - Create visualizations and dashboards in Power BI to communicate insights.
   - Build predictive models to identify potential churners (e.g., predicting 150 out of 200 churners in a month).
3. **Engage and Act**:
   - Collaborate with sales and management teams to design retention strategies.
   - Perform cost analysis and calculate Customer Lifetime Value (CLV) to balance offer costs with retention benefits.
   - Track Key Performance Indicators (KPIs) to monitor churn drivers.

## Dataset Description
The dataset includes customer attributes such as:
- **Customer ID**: Unique identifier for each customer.
- **Gender**: Male or Female.
- **Senior Citizen**: Binary indicator (Yes/No).
- **Partner, Dependents**: Family-related attributes.
- **Tenure**: Duration of customer relationship with the company.
- **Monthly Charges, Total Charges**: Financial metrics.
- **Contract Type**: Contract terms (e.g., month-to-month, one-year).
- **Payment Method**: Payment types (e.g., electronic check, credit card).
- **Churn**: Binary outcome (Yes/No).

The dataset is clean but contains some missing values (e.g., three empty fields in `Total Charges`). In real-world scenarios, data collection may involve challenges like:
- Scattered data across multiple teams or databases.
- Need for web scraping or API integration.
- Raw data in multiple Excel sheets requiring cleaning and standardization.

## Data Cleaning
Data cleaning was performed in Power BI's Power Query Editor due to the assumption that Python is unavailable. Key steps included:
- **Column Quality Check**: Enabled column distribution, profile, and quality checks to identify errors and missing values.
- **Handling Missing Values**:
  - Identified three empty fields in `Total Charges` (numerical column).
  - Imputed missing values with the mean of `Total Charges` (2283) using DAX:
    ```dax
    Average of Total Charges = AVERAGE('Telco Churn'[Total Charges])
    ```
  - Replaced null values in `Total Charges` with 2283 via Power Query's "Replace Values" function.
- **Categorical Columns**: No missing values were found, but mode imputation was noted as an option for categorical columns if needed.

## Exploratory Data Analysis (EDA)
EDA was conducted to understand customer characteristics and churn patterns, focusing on both univariate and bivariate analyses.

### Univariate Analysis (Categorical Features)
- **Gender**:
  - Overall population: Approximately 50% male (3555) and 50% female.
  - Churned population: Also ~50% male and ~50% female, indicating no significant gender-based churn disparity.
  - Insight: Gender alone does not strongly influence churn.
- **Senior Citizen**:
  - Overall population: 13% senior citizens (1142) vs. 87% non-seniors (7043 total customers).
  - Churned population: 20% senior citizens (476 out of 1869 churners).
  - Insight: Senior citizens have a higher churn rate (476/1142 ≈ 41%) compared to non-seniors, suggesting they are more likely to churn, possibly due to health issues, reduced usage, or other factors.
- **Payment Method**:
  - Churned population: Predominantly electronic check users.
  - Insight: Customers using electronic checks are more likely to churn, possibly due to dissatisfaction with payment processes or related services.

### Bivariate Analysis
- **Gender and Payment Method**:
  - Overall population: Similar ratios for males and females across payment methods.
  - Churned population: Females using credit cards show a higher churn rate (57% of credit card churners are female vs. 43% male).
  - Insight: Female customers using credit cards are more likely to churn, indicating a potential interaction between gender and payment method.
- **Numerical Features (Monthly Charges vs. Total Charges)**:
  - Scatter plot analysis showed a weak linear relationship between `Monthly Charges` and `Total Charges`.
  - Insight: No clear correlation pattern, requiring further investigation into numerical feature relationships.

## Dashboard Creation
The Power BI dashboard was designed to present insights clearly and interactively, resembling a website with multiple pages, tooltips, and navigation features. Key elements include:

### Visualizations
- **Gender Distribution**:
  - Bar chart showing ~50% male and ~50% female for both overall and churned populations.
  - Formatted with data labels and transparent background for clarity.
- **Senior Citizen Churn**:
  - Bar chart comparing senior citizen churn (20%) vs. non-senior churn, highlighting the 41% churn rate among seniors.
- **Payment Method Funnel**:
  - Funnel chart visualizing churn by payment method, emphasizing electronic check users as high churners.
- **Numerical Analysis**:
  - Scatter plot of `Monthly Charges` vs. `Total Charges`, though no strong pattern was observed.
- **KPIs**:
  - Card displaying total customer count (7043) using DAX:
    ```dax
    Total Count = COUNTROWS('Telco Churn')
    ```
  - Card for churned customer count with a filter applied for `Churn = Yes`.

### Dashboard Design
- **Background Image**:
  - Created using Snapa.com with a light shade for better readability.
  - Included text ("Customer Dashboard") and shapes to enhance aesthetics.
  - Applied as a page background in Power BI with adjusted transparency.
- **Tooltips**:
  - Created a separate tooltip page with a card for `Count of Customer ID`.
  - Configured as a tooltip in Page Information and linked to main dashboard visuals.
  - Adjusted page size to optimize tooltip display.
- **Navigation**:
  - Added a homepage with a blank button for page navigation (e.g., to the main dashboard).
  - Included a text box labeled "Summary" for user-friendly navigation.
- **Ask a Question Feature**:
  - Utilized Power BI’s inbuilt Q&A feature by double-clicking on the canvas to enable natural language queries.

### Best Practices
- Created a blank query to store DAX measures (e.g., mean of `Total Charges`).
- Used lighter background shades for professional appearance.
- Hid tooltip pages in the published dashboard to maintain a clean interface (e.g., appearing as three pages instead of four).
- Ensured all important features (gender, senior citizen, payment method, tenure) were represented in the dashboard.

## Key Insights
1. **Senior Citizens**: 41% of senior citizens churn, significantly higher than the overall churn rate (~10%), indicating a need for targeted retention strategies for this group.
2. **Payment Method**: Electronic check users are more likely to churn, suggesting potential issues with payment processes or customer experience.
3. **Gender**: No significant difference in churn rates between males and females overall, but females using credit cards show a higher churn tendency (57%).
4. **Numerical Features**: Weak correlation between `Monthly Charges` and `Total Charges`, requiring further analysis to uncover numerical predictors of churn.
5. **Churn Rate**: Assuming a 10% monthly churn rate (100 out of 1000 customers), reducing it to 5-6% is feasible through targeted interventions based on these insights.

## Recommendations
- **Retention Strategies**:
  - Offer tailored plans for senior citizens, addressing potential barriers like health-related usage declines or cost sensitivity.
  - Improve electronic check payment processes to enhance customer satisfaction and reduce churn.
  - Provide incentives for female credit card users to retain them, as they show higher churn rates.
- **Predictive Modeling**:
  - Develop models to predict churn based on senior citizen status, payment method, and tenure.
  - Use CLV calculations to prioritize high-value customers for retention efforts.
- **Cost Analysis**:
  - Evaluate the cost of retention offers vs. the revenue loss from churn (e.g., offering discounts to 150 predicted churners, knowing only 80 may actually churn).
- **Dashboard Enhancements**:
  - Add more interactive elements like drill-throughs for detailed customer segment analysis.
  - Incorporate predictive model outputs (e.g., churn probability scores) into the dashboard if available.

## Future Work
- **Live Data Connectivity**: Transition from static data (e.g., 6-12 months of historical data) to live database connectivity for real-time insights.
- **Advanced Modeling**: Build predictive models to identify churners with higher accuracy and integrate them into the dashboard.
- **Cross-Industry Application**: Adapt the churn analysis framework for other domains (e.g., banking, gaming) by mapping churn types and customer decision cycles.
- **Additional Features**: Explore more bivariate relationships (e.g., tenure vs. payment method) and incorporate them into the dashboard.

## Conclusion
This telecom churn analysis provides a robust foundation for understanding customer behavior and reducing churn rates. By leveraging Power BI for EDA and visualization, key insights were derived regarding senior citizens, payment methods, and gender-based patterns. The dashboard offers an intuitive, website-like interface for stakeholders to explore these findings. Future efforts should focus on live data integration, predictive modeling, and tailored retention strategies to achieve a target churn reduction from 10% to 5-6%.
