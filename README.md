# Product-Cost-Segmentation-Analysis-SQL-
#### Project Overview
This project segments products into cost ranges and counts the number of products in each segment.  
The analysis helps businesses understand product pricing distribution and optimize pricing strategies.
#### Objective
- Categorize products into defined cost ranges (below $100, between $100 and $ 500, between 500 and 1000, above 1000).
- Count the number of products per cost segment.
- Provide insights for pricing strategy and portfolio management.
#### SQL queries
  WITH product_segments AS (
    SELECT 
        product_key,
        product_name,
        cost,
        CASE 
            WHEN cost < 100 THEN 'Below 100'
            WHEN cost BETWEEN 100 AND 500 THEN '100 - 500'
            WHEN cost BETWEEN 500 AND 1000 THEN '500 - 1000'
            ELSE 'Above 1000'
        END AS cost_range
    FROM public."gold.dim_products"
)

SELECT 
    cost_range,
    COUNT(product_key) AS product_count
FROM product_segments
GROUP BY cost_range
ORDER BY product_count ASC;
