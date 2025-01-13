# E-Commerce Customer Analysis: Cohort Retention, Market Basket and Profitability with Tableau


## Introduction 

Many companies find it tough to hold on to their customers. Poor product quality, bad customer experiences, and lack of engagement often push customers to switch to competitors. As Data Analyst, it's essential to understand these issues and address them through data analysis and targeted strategies to reduce churn and improve retention. Cohort Analysis, Customer retention ( this is the opposite of Churn), Market Basket and Profitability are very important analyses to make business profitable

Cohort analysis groups customers by shared traits or behaviors and tracks their actions over time. Here's why it's valuable:
* a. Understanding Behavior: It shows how different customer groups act over time. For example, you can track repeat purchases based on their first purchase date.

* b. Identifying Trends: Compare groups to spot trends and make informed decisions. For instance, you might find that customers who join during a promotion stay longer.
* c. Optimizing Marketing: See how different groups respond to marketing campaigns, helping to target and engage specific customer segments.
* d. Improving Retention: Understand what affects retention, like the onboarding experience. If a group has high churn after the first month, focus on improving the onboarding process.


Customer retention is about keeping your current customers happy and engaged, so they keep doing business with you. The retention rate measures how well a company retains its customers over a specific period. It's more cost-effective to retain customers than to find new ones. Here's why:
* a. Cost-effective: Getting new customers is expensive due to marketing and sales efforts. Keeping current customers costs less since you’ve already built a relationship.
* b. Stable Revenue: Existing customers are more likely to buy again, providing steady revenue that helps your business handle market changes.
* c. Word-of-Mouth: Happy customers are likely to recommend your products or services. Positive word-of-mouth can attract new customers more cheaply than ads.
* d. Brand Loyalty: Loyal customers build a strong foundation for long-term success. They're less likely to switch to competitors and more forgiving of occasional mistakes.
* e. Feedback: Current customers can give valuable feedback that helps improve your products or services, leading to better experiences and higher retention.

Market Basket Analysis (MBA) is a technique retailers use to identify products that customers frequently buy together by analysing purchase history. This helps optimize inventory, devise marketing strategies, and improve customer engagement. For example, if paper and binder are often bought together, a store might place them nearby to encourage additional purchases. MBA also aids in cross-selling and up-selling, boosting sales and customer satisfaction.

The data used is the SuperStore Dataset


## Data Transformation


### a. For Cohort Analysis

Create the following calculated field and name them

1. Customers First Purchase Quarter: to know the first time of customer purchase in a certain quarter.
{ FIXED [Customer Name]: MIN(DATETRUNC('quarter', [Order Date]))}. Change Data Type to Date

2. Customers per First Quarter: to know the number of new customer in a certain quarter. 
{ FIXED [Customers First Purchase Quarter]: COUNTD([Customer Name])}

3. Retention Rate: to know the number of customer who continue business with company i.e number of customer divided by the number of customers per first quarter
COUNTD([Customer Name])/ SUM([Customers Per First Quarter]). Change Default Number Format to 1 Decimal Place.

4. Elapsed quarters:  to know the number of complete quarters that have passed within a certain time frame. 
DATEDIFF('quarter', [Customers First Purchase Quarter], DATETRUNC('quarter', [Order Date]))

### b. For Market Basket and Profitability 

* Create a Calculated Field as Profit Ratio: to measure profitability
SUM([Profit]) / SUM([Sales])
* Joins : Orders on Orders inner join  with order id = order id and  sub category < subcategory. This is to aid visualisation


## Visualisation

1. Cohort Retention: 
 Column: ‘Order Date’  set to Quarter (Quarter Year), and change to Discrete format
 Row: a. 'Customers 'First Purchase Quarter- set to Quarter (Quarter Year), and change to Discrete format  .  b. ‘Customers per First Quarter’
 Colour Marks: ‘Retention Rate’ as aggregated. Use heat map
 Tooltip Marks: 'Customer Name' as Count Distinct. Unhide Mark

2. Cohort Retention with Elapsed Quarter
 Column: ‘Elapsed Quarters’  set to Quarter (Quarter Year), and change to Discrete format. Hide the Column 0 in the visualisation
 Row: a. 'Customers 'First Purchase Quarter- set to Quarter (Quarter Year), and change to Discrete format  .  b. ‘Customers per First Quarter’
 Colour Marks: ‘Retention Rate’ as aggregated. Use heat map
 Tooltip Marks: 'Customer Name' as Count Distinct. Unhide Mark

3. Trend of Retention Rate
Column: Retention Rate 
Row: Elapsed Quarters as Continuous value.
Filter: Elapsed Quarter

4. Trend of Retention Rate by Segment
Column: Retention Rate 
Row: Elapsed Quarters as Continuous value.
Filter: Elapsed Quarter
Color Marks: Segment 

5. Trend of Retention Rate by Consumer Segment
Column: Retention Rate 
Row: Elapsed Quarters as Continuous value.
Color Marks: Segment 


6. Profit by Category
Row: a. Category.  b. Sub-Category
Text Marks: Profit as SUM
Filter: Segment 

7. Market Basket, Profit and Profit Ratio
Column: Sub-Category
Row: Sub-Category (Order1) from the join created
Color Marks: Order ID as Count Distinct
Text Marks: Order ID as Count Distinct
Tooltip Marks: a. Profit Ratio AS AGG. b. Profit AS SUM

8. Create Dashboard. 



## Findings

1. The retention rate is 9.4% - 22.2% after the first 6 months for new customer, this rose to 8.0- 30.8% after on year, then 17-23% after two years and 18-29% after thre years
2. Generally, retention rate experienced an increase from the second quarter after the initial/first product purchase and continued to rise until the 15th quarter by 32.8%.
3. Retention trend by segment shows highest retention in the consumer segment with 7.7%- 18.8% retention rate; Corporate 4.5-9.7% and Home office 2.5-6.35. 
4. Retention rate trend for the Consumer segment initially fluctuated in the range of 7.7%-12.4%, but afterwards increased very rapidly after entering the 14th quarter until the 16th quarter, reaching 18.8%.
5. The Office Supplies category has highest customer retention rate. 
6. Profit by category: Technology yielded the most profit $83K followed by Office supplies $58K. Furniture is underperforming $24K
7.Cross-selling opportunities with high profit: Paper, Binder and Storage could be cross-sell profitably with other items.  
8. While customer buy furniture and binder, the combination had very low profit

## Marketing Recommendations
1. Phone (and the Technology) has more profit, direct marketing campaign towards this
2. In Office supplies with higher customer retention, direct marketing campaign toward cross-selling Paper, Binder and Storage with any other item.
3. Marketing ideas for the furniture industry:
    * a. Visual Marketing: Share high-quality photos and videos of your furniture on social media, your website, and in ads to grab attention.
    * b. Influencer Collaborations: Partner with interior design influencers and home decor bloggers to showcase your furniture in real-life settings. Their reviews and tips can boost your brand's visibility.
    * c. Personalized Suggestions: Use data to recommend products based on what customers like and their browsing history, through emails, ads, and on your site.
    * d. Partner with Builders and Designers: Team up with home builders, interior designers, and real estate agents to display your furniture in model homes and design projects. This can increase your exposure and sales.
    * e. Local Campaigns: Customize marketing efforts for specific areas or groups based on local trends and preferences. Use local ads, events, and partnerships with nearby businesses.
    * f. Loyalty Programs: Create programs that reward customers for repeat purchases and referrals with discounts and exclusive offers, encouraging them to keep coming back.

