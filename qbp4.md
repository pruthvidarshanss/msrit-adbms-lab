# `QB Program 4`

[A] Car marketing company wants keep track of marketed cars and their owner. Each car must be associated with a single owner and owner may have any number of cars. We store car’s registration number, model & color and owner’s name, address & SSN. We also store date of purchase of each car.

```sql
CREATE TABLE OWNER (
    SSN VARCHAR(20) PRIMARY KEY,
    NAME VARCHAR(20),
    ADDRESS VARCHAR(30)
);

INSERT INTO OWNER (SSN, NAME, ADDRESS) VALUES 
("101", "Pruthvi", "Bengaluru"),
("102", "Kajal", "Bengaluru"),
("103", "Roshan", "Mumbai"),
("104", "Salman", "Mumbai");

CREATE TABLE CARS (
    REG_NO VARCHAR(20) PRIMARY KEY,
    MODEL VARCHAR(20),
    COLOR VARCHAR(20),
    OWNER_ID VARCHAR(20),
    PURCHASE_DATE DATE,
    FOREIGN KEY (OWNER_ID) REFERENCES OWNER(SSN)
);

INSERT INTO CARS (REG_NO, MODEL, COLOR, OWNER_ID, PURCHASE_DATE) VALUES 
("5001", "BMW", "Black", "101", "2023-04-06"),
("5002", "Hyundai", "Maroon", "101", "2023-03-03"),
("5003", "Ferrari", "Yellow", "104", "2023-04-24"),
("5004", "Suzuki", "Blue", "102", "2023-11-19"),
("5005", "Honda", "Silver", "103", "2023-03-03"),
("5006", "Mahindra", "Black", "101", "2023-01-13");
```

* Find a person who owns highest number of cars
```SQL
SELECT o.Name, COUNT(*) AS CAR_COUNT
FROM OWNER o
JOIN CARS c ON o.SSN = c.OWNER_ID
GROUP BY o.SSN 
ORDER BY CAR_COUNT DESC
LIMIT 1;
```

|Name|CAR_COUNT|
|---|---|
|Pruthvi|3|

* Retrieve persons and cars information purchased on the day 03-03-2023
```SQL
SELECT o.NAME, c.MODEL, c.REG_NO
FROM OWNER o
JOIN CARS c ON c.OWNER_ID = o.SSN
WHERE PURCHASE_DATE = "2023-03-03";
```

|NAME|MODEL|REG_NO|
|---|---|---|
|Pruthvi|Hyundai|5002|
|Roshan|Honda|5005|


* Write a insertion trigger to check date of purchase must be less than current date (must use system date)
```SQL
DELIMITER //
CREATE TRIGGER check_purchase_date
BEFORE INSERT ON CARS
FOR EACH ROW
BEGIN
    IF NEW.PURCHASE_DATE >= CURDATE() THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Date of purchase must be less than the current date.';
    END IF;
END;
//
DELIMITER ;
```

```SQL
CREATE TRIGGER check_purchase_date BEFORE INSERT ON CARS FOR EACH ROW BEGIN IF NEW.PURCHASE_DATE >= CURDATE() THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Date of purchase must be less than the current date.'; END IF; END;;
```


[B] Consider the following Tourist places table with the following attributes - Place, address – (state), id, tourist attractions, best time of the year to visit, modes of transport(include nearest airport, railway station etc), accommodation, food - what not to miss for sure Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

```js
db.createCollection("tourist_places");

db.tourists_places.insertMany([
    { 
        Place: "Bangalore Palace", 
        address: "Karnataka", 
        id: 1, 
        tourist_attractions: ["Bangalore Palace", "Cubbon Park", "Lalbagh Botanical Garden"], 
        best_time_to_visit: "October to February", 
        modes_of_transport: ["Kempegowda International Airport", "Bangalore City Railway Station"], 
        accommodation: "Hotels and resorts", 
        food: "Masala Dosa and Filter Coffee" 
    },
    { 
        Place: "ISKCON Temple Bangalore", 
        address: "Karnataka", 
        id: 2, 
        tourist_attractions: ["ISKCON Temple", "Vidhana Soudha", "Wonderla Amusement Park"], 
        best_time_to_visit: "Throughout the year", 
        modes_of_transport: ["Kempegowda International Airport", "Bangalore City Railway Station"], 
        accommodation: "Hotels and lodges", 
        food: "Chaat and South Indian Thali" 
    },
    { 
        Place: "Bannerghatta National Park", 
        address: "Karnataka", 
        id: 3, 
        tourist_attractions: ["Bannerghatta National Park", "Wonderla Amusement Park", "Art of Living International Center"], 
        best_time_to_visit: "October to March", 
        modes_of_transport: ["Kempegowda International Airport", "Bangalore City Railway Station"], 
        accommodation: "Resorts and guesthouses", 
        food: "Bisi Bele Bath and Ragi Mudde" 
    },
    { 
        Place: "Ulsoor Lake", 
        address: "Karnataka", 
        id: 4, 
        tourist_attractions: ["Ulsoor Lake", "Commercial Street", "MG Road"], 
        best_time_to_visit: "Throughout the year", 
        modes_of_transport: ["Kempegowda International Airport", "Bangalore City Railway Station"], 
        accommodation: "Hotels and budget stays", 
        food: "Pani Puri and Biryani" 
    },
    { 
        Place: "Nandi Hills", 
        address: "Karnataka", 
        id: 5, 
        tourist_attractions: ["Nandi Hills", "Tipu Sultan's Summer Palace", "Lumbini Gardens"], 
        best_time_to_visit: "September to May", 
        modes_of_transport: ["Kempegowda International Airport", "Bangalore City Railway Station"], 
        accommodation: "Resorts and cottages", 
        food: "Thatte Idli and Mysore Pak" 
    },
    { 
        Place: "Kovalam", 
        address: "Kerala", 
        id: 6, 
        tourist_attractions: ["Kovalam Beach", "Lighthouse Beach", "Vellayani Lake"], 
        best_time_to_visit: "September to March", 
        modes_of_transport: ["Trivandrum International Airport", "Thiruvananthapuram Railway Station"], 
        accommodation: "Resorts and beachfront hotels", 
        food: "Kerala Fish Curry and Parotta" 
    },
    { 
        Place: "Varkala", 
        address: "Kerala", 
        id: 7, 
        tourist_attractions: ["Varkala Beach", "Janardanaswamy Temple", "Varkala Cliff"], 
        best_time_to_visit: "September to March", 
        modes_of_transport: ["Trivandrum International Airport", "Varkala Railway Station"], 
        accommodation: "Resorts and guesthouses", 
        food: "Kerala Thali and Banana Chips" 
    },
    { 
        Place: "Kumarakom", 
        address: "Kerala", 
        id: 8, 
        tourist_attractions: ["Kumarakom Bird Sanctuary", "Kumarakom Backwaters", "Pathiramanal Island"], 
        best_time_to_visit: "September to March", 
        modes_of_transport: ["Cochin International Airport", "Kottayam Railway Station"], 
        accommodation: "Luxury resorts and houseboats", 
        food: "Kerala Sadya and Toddy" 
    },
    { 
        Place: "Palakkad", 
        address: "Kerala", 
        id: 9, 
        tourist_attractions: ["Palakkad Fort", "Malampuzha Dam", "Silent Valley National Park"], 
        best_time_to_visit: "November to February", 
        modes_of_transport: ["Coimbatore International Airport", "Palakkad Railway Station"], 
        accommodation: "Hotels and resorts", 
        food: "Kerala Biriyani and Halwa" 
    },
    { 
        Place: "Kozhikode", 
        address: "Kerala", 
        id: 10, 
        tourist_attractions: ["Kozhikode Beach", "Beypore Beach", "Mananchira Square"], 
        best_time_to_visit: "September to May", 
        modes_of_transport: ["Calicut International Airport", "Kozhikode Railway Station"], 
        accommodation: "Hotels and homestays", 
        food: "Kerala Halwa and Paragon's Biriyani" 
    }
]);
```

* List all the tourist places of Karnataka
```js
db.tourist_places.find({ address: "Karnataka" });
```

* List the tourist attractions of Kerala. Exclude accommodation and food
```js
db.kerala_tourist_places.find(
  { address: "Kerala" },
  { Place: 1, tourist_attractions: 1, best_time_to_visit:1, modes_of_transport:1,  _id: 0 }
);
```