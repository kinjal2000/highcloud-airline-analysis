create database Olist_store;
use Olist_store;

select count(*) from Olist_customers_dataset;
select count(*) from Olist_order_items_dataset;
select count(*) from Olist_order_payments_dataset;
select count(*) from Olist_orders_dataset;
select count(*) from Olist_products_dataset;
select count(*) from Olist_reviews_dataset;


select * from Olist_orders_dataset;
select* from Olist_order_payments_dataset;

-- KPI1

create table kpi1
select orders.order_id,orders.order_purchase_timestamp,payment.payment_value,payment.payment_type from 
Olist_orders_dataset as orders
left join  Olist_order_payments_dataset as payment 
on orders.order_id = payment.order_id;

select * from kpi1;
 
select dayname(order_purchase_timestamp) from Olist_orders_dataset;

select
if (dayname(Order_purchase_timestamp) in("sunday","saturday"), "Weekend","Weekday") as Day_Type, 
round(sum(payment_value),2)as Total_Payment  from kpi1 
group by Day_Type;
 
select
if(weekday(Order_purchase_timestamp)  in(5,6 ), " Weekend" ,"Weekday") as Day_type,
round(sum(payment_value),2) as Total_payment from kpi1
group by Day_type;

------------------------------------------------------------------------------------------------------
-- kpi2

select * from Olist_orders_dataset;
select * from Olist_reviews_dataset;
select *from Olist_order_payments_dataset;

create table kpi2
select orders.order_id, reviews.review_score,payment.payment_type from 
Olist_orders_dataset as orders
 left join Olist_reviews_dataset as reviews on
orders.order_id=reviews.order_id 
left join Olist_order_payments_dataset as payment on
orders.order_id = payment.order_id;

select * from kpi2;
 
select review_score,payment_type,count(order_id)as Total_orders from kpi2
where review_score=5 and payment_type="credit_card"; 
 
 -------------------------------------------------------------------------------------------------------------
--  kpi3

select* from Olist_order_items_dataset;
select *from Olist_orders_dataset;
select *from Olist_products_dataset;
 
create table kpi3
 select o.order_id,i.product_id,p.product_category_name, o.order_delivered_customer_date  from Olist_order_items_dataset as i
 left join Olist_products_dataset as p on
 i.product_id =p.product_id
 left join Olist_orders_dataset as o 
 on i.order_id=o.order_id;
 
 select * from kpi3;
 
 select round(avg(day(order_delivered_customer_date)),0) as Avg_deliverydays from kpi3
 where product_category_name= "pet_shop" ;
 ----------------------------------------------------------------------------------------------------------------
--  kpi4

select * from Olist_customers_dataset;
select *from Olist_order_payments_dataset;
 select* from Olist_order_items_dataset;
 select * from Olist_orders_dataset;
 
 create table kpi4
 select o.order_id, c.customer_id,c.customer_city,i.price,p.payment_value from Olist_orders_dataset as o
 left join Olist_customers_dataset as c
 on o.customer_id=c.customer_id
 left join olist_order_items_dataset as i
 on o.order_id=i.order_id
 left join olist_order_payments_dataset  as p
 on  o.order_id = p.order_id;
 
 select * from kpi4;
 
  select round(avg(price),0) as Avg_Price,round(avg(payment_value),0)as avg_Payment from kpi4
  where customer_city = "Sao paulo";
  
  -----------------------------------------------------------------------------------------------
--   kpi5

select *from Olist_orders_dataset;
select * from Olist_reviews_dataset;

create table kpi5
select o.order_id,o.order_delivered_customer_date,o.order_purchase_timestamp,r.review_score
 from Olist_orders_dataset as o 
 left join olist_reviews_dataset as r 
 on o.order_id =r.order_id;
 
select * from kpi5;

select review_score,round(avg(datediff(order_delivered_customer_date,order_purchase_timestamp)),0) as shipping_days 
from kpi5 
where review_score is not null
group by review_score 
order by review_score;
