# Superstore-sales-analysis
Analyzed Superstore sales data using SQL to find profit drivers

-- Kaunsi Category sabse zyada profit deti hai?
select category, round(sum(profit),2) as total_profit
from superstore
group by category
order by total_profit desc;

-- Region-wise profit
select region, round(sum(profit), 2) as total_profit
from superstore
group by region
order by total_profit desc;

-- Furniture ke andar loss kahan se aa raha hai (Sub-Category level):
select subcategory , round(sum(profit),2) as total_profit, round(avg(discount), 2) as discount
from superstore
where category = 'Furniture'
group by 1
order by total_profit asc;


-- Discount aur Profit ka overall relationship
select 
	case
		when discount = 0 then 'No '
        when discount <=0.2 then 'Low 0-20%'
        when discount <= 0.4 then 'Medium 20-40%'
        else 'High 40-100%' end as discount_range,
	round(sum(profit), 2) as total_profit,
    count(*) as Num_Orders
from superstore
group by discount_range
order by total_profit desc;

-- Top 5 Products (by Profit)
select subcategory, round(sum(profit), 2) as total_profit
from superstore
group by 1
order by 2 desc
limit 5;

-- Bottom 5 Products 
select subcategory, round(sum(profit), 2) as Low_Profit
from superstore
group by 1
order by 2 asc
limit 5;

Superstore Sales Analysis — Key Findings

Category Performance: Technology sabse profitable category hai ($145K), phir Office Supplies ($122K). Furniture sabse kam profitable hai (~$18K) discount-heavy sub-categories ki wajah se.
Regional Performance: West aur East regions sabse zyada profit dete hain. Central region sabse kam profitable hai — potential improvement area.
Discount-Profit Relationship: Ye sabse important finding hai — 20% se zyada discount dene par company loss mein chali jati hai. No-discount orders ne $320K profit diya, jabke 40%+ discount wale orders ne $99K ka loss diya.
Problem Products: Tables aur Bookcases sabse zyada loss de rahe hain, jo unke high average discount (26% aur 21%) se directly linked hai.
Star Products: Copiers, Phones, aur Accessories sabse zyada profit generate karte hain aur discount strategy ko replicate/study karne layak hain.

Recommendation: Discount policy ko revisit karna chahiye, khaas kar Tables aur Bookcases par — 20% se zyada discount avoid karna profit barha sakta hai.
