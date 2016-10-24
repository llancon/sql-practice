# sql-practice
Week 5 Monday homework
  
  How many users are there? 
    sqlite> select count (*) from users;
    50
  
  What are the 5 most expensive items?
    sqlite> select *
    ...> from items
    ...> order by price desc 
    ...> limit 5;
    25|Small Cotton Gloves|Automotive, Shoes & Beauty|Multi-layered modular service-desk|9984
    83|Small Wooden Computer|Health|Re-engineered fault-tolerant adapter|9859
    100|Awesome Granite Pants|Toys & Books|Upgradable 24/7 access|9790
    40|Sleek Wooden Hat|Music & Baby|Quality-focused heuristic info-mediaries|9390
    itm60|Ergonomic Steel Car|Books & Outdoors|Enterprise-wide secondary firmware|9341
  
  What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
      sqlite> select *
       ...> from items
       ...> where category = Books
       ...> order by price
       ...> limit 2;
    Error: no such column: Books
    sqlite> select *
       ...> from items
       ...> where category like '%Books%'
       ...> order by price 
       ...> limit 1
       ...> ;
    id|title|category|description|price
    76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496
   
  Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
    sqlite> select users.* from users inner join addresses on addresses.user_id = users.id where addresses.street = '6439 Zetta Hills' and addresses.city = 'Willmouth' and addresses.state = 'WY';
  id|first_name|last_name|email
  40|Corrine|Little|rubie_kovacek@grimes.net
    sqlite> select users.first_name, addresses.street,addresses.city, addresses.state from users inner join addresses on addresse
    first_name|street|city|state
    Corrine|6439 Zetta Hills|Willmouth|WY
    Corrine|54369 Wolff Forges|Lake Bryon|CA

