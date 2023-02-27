# Fetch-SQL-Test-

--- Question 2: which user spent the most money in the month of Auguest? 
SELECT user_id,
       EXTRACT(month FROM purchase_date) AS month,
	   SUM(total_spent) AS total_spent
FROM receipts 
WHERE EXTRACT(month FROM purchase_date) = 8
GROUP BY user_id, month
ORDER BY total_spent DESC
LIMIT 1
---user_id = "609ab37f7a2e8f2f95ae968f" spent the most money in the month of Auguest

---Question 3: which user bought the most expensive item 
SELECT ri.total_final_price/ri.quantity_purchased AS unit_price, 
	   r.user_id
FROM receipt_items ri
LEFT JOIN receipts r
ON ri.rewards_receipt_id = r.id
WHERE quantity_purchased >0 AND total_final_price>0
ORDER BY unit_price DESC
LIMIT 1
--- user_id: 617376b8a9619d488190e0b6 bought the most expensive item

--- Question 4: what's the name of the most expensive item purchased 
SELECT r.total_final_price/r.quantity_purchased AS unit_price, 
       r.brandcode, b.name
FROM receipt_items r
LEFT JOIN brands b
USING (brandcode)
WHERE quantity_purchased >0 AND total_final_price>0
ORDER BY unit_price DESC
LIMIT 1
--- startbucks is the name of the most expensive item purchased 

--- Question 5: How many users scanned in each month 
SELECT EXTRACT(month FROM date_scanned) AS month,
       COUNT(DISTINCT user_id)
FROM receipts 
GROUP BY month 
ORDER BY month
