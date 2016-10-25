# sql-practice
Week 5 Monday homework
  
1.) How many users are there? 
    sqlite> select count (*) from users;
    50
  
2.) What are the 5 most expensive items?
    sqlite> select *
    ...> from items
    ...> order by price desc 
    ...> limit 5;
    25|Small Cotton Gloves|Automotive, Shoes & Beauty|Multi-layered modular service-desk|9984
    83|Small Wooden Computer|Health|Re-engineered fault-tolerant adapter|9859
    100|Awesome Granite Pants|Toys & Books|Upgradable 24/7 access|9790
    40|Sleek Wooden Hat|Music & Baby|Quality-focused heuristic info-mediaries|9390
    itm60|Ergonomic Steel Car|Books & Outdoors|Enterprise-wide secondary firmware|9341
  
3.) What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
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
   
4.) Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
    sqlite> select users.* from users inner join addresses on addresses.user_id = users.id where addresses.street = '6439 Zetta Hills' and addresses.city = 'Willmouth' and addresses.state = 'WY';
  id|first_name|last_name|email
  40|Corrine|Little|rubie_kovacek@grimes.net
    sqlite> select users.first_name, addresses.street,addresses.city, addresses.state from users inner join addresses on addresse
    first_name|street|city|state
    Corrine|6439 Zetta Hills|Willmouth|WY
    Corrine|54369 Wolff Forges|Lake Bryon|CA
    
5.) Correct Virginie Mitchell's address to "New York, NY, 10108".    
    id|first_name|last_name|email
    39|Virginie|Mitchell|daisy.crist@altenwerthmonahan.biz
    sqlite> update addresses
       ...> set city = 'New York', state = 'NY', zip = '10108'
       ...> where user_id = '39';
    sqlite> select * from addresses where user_id = '39';
    id|user_id|street|city|state|zip
    41|39|12263 Jake Crossing|New York|NY|10108
    42|39|83221 Mafalda Canyon|New York|NY|10108
    
6.) How much would it cost to buy one of each tool?
    sqlite> select sum(price) from items where category like '%Tools%';
46477

7.) How many total items did we sell?
       sqlite> select sum(quantity) from orders;
      sum(quantity)
      -------------
      2125 
8.) How much was spent on books?
                sqlite> select price * quantity as value from items, orders where category = 'Books' and orders.item_id = items.id;
        value     
        ----------
        11968     
        21392     
        27504     
        71232     
        10472     
        53424     
        80136     
        71232     
        46230     
        17808     
        3056      
        6112      
        sqlite> select sum(price * quantity) as value from items, orders where category = 'Books' and orders.item_id = items.id; 
        value     
        ----------
        420566  
        
9.) Simulate buying an item by inserting a User for yourself and an Order for that User.     
insert into users values
         ...> ('51','Luis','Lancon','abcdefg@tiy.com');
         sqlite> insert into orders values ('378','51','100','20',' 2016-10-09 00:40:31.307668');
         
