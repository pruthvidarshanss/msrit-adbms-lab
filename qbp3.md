# `QB Program 3`

[A] The production company is organized into different studios. We store each studio’s name branch and location; a studio own any number of Cartoon-serials. We store each Cartoon-Serial’s title, sensor_number and year of production. Star may do voices in any number of Cartoon-Serials and we store each actors name and address. 

```sql
CREATE TABLE STUDIOS (
    STUDIO_ID INT PRIMARY KEY,
    NAME VARCHAR(255),
    BRANCH VARCHAR(255),
    LOCATION VARCHAR(255)
);

INSERT INTO STUDIOS (STUDIO_ID, NAME, BRANCH, LOCATION) VALUES
(1, 'CN', 'London', 'UK'),
(2, 'POGO', 'Ohio', 'USA'),
(3, 'Hungama', 'Mumbai', 'India'),
(4, 'Disney', 'Bengaluru', 'India');


CREATE TABLE CARTOON_SERIALS (
    CARTOON_SERIAL_ID INT PRIMARY KEY,
    TITLE VARCHAR(255),
    SENSOR_NO INT,
    YEAR INT,
    STUDIO_ID INT,
    FOREIGN KEY (STUDIO_ID) REFERENCES STUDIOS(STUDIO_ID)
);

INSERT INTO CARTOON_SERIALS (CARTOON_SERIAL_ID, TITLE, SENSOR_NO, YEAR, STUDIO_ID) VALUES
(1, 'Tom and Jerry', 101, 2000, 1),
(2, 'SpongeBob SquarePants', 102, 2005, 2),
(3, 'ShinChan', 103, 2001, 3),
(4, 'Doraemon', 104, 2002, 4);


CREATE TABLE ACTORS (
    ACTOR_ID INT PRIMARY KEY,
    NAME VARCHAR(255),
    ADDRESS VARCHAR(255)
);

INSERT INTO ACTORS (ACTOR_ID, NAME, ADDRESS) VALUES
(201, 'Richard Kind', 'UK'),
(202, 'Jennifer', 'USA'),
(203, 'Nora', 'USA'),
(204, 'Yashoda', 'India'),
(205, 'Yash', 'India'),
(206, 'John', 'UK');


CREATE TABLE CARTOON_ACTORS (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    CARTOON_SERIAL_ID INT,
    ACTOR_ID INT,
    FOREIGN KEY (CARTOON_SERIAL_ID) REFERENCES CARTOON_SERIALS(CARTOON_SERIAL_ID),
    FOREIGN KEY (ACTOR_ID) REFERENCES ACTORS(ACTOR_ID)
);

INSERT INTO CARTOON_ACTORS (CARTOON_SERIAL_ID, ACTOR_ID) VALUES
(1, 201),
(1, 203),
(2, 204),
(3, 202),
(3, 205),
(4, 206);
```

* Find total no of actors, do voiced in a Cartoon-Serials ‘Tom and Jerry’
```SQL
SELECT COUNT(*) AS total_actors
FROM ACTORS a
JOIN CARTOON_ACTORS ca ON a.ACTOR_ID = ca.ACTOR_ID
JOIN CARTOON_SERIALS cs ON ca.CARTOON_SERIAL_ID = cs.CARTOON_SERIAL_ID
WHERE cs.TITLE = 'Tom and Jerry';
```

|total_actors|
|---|
|2|

* Retrieve name of studio, location and Cartoon-Serials title in which star “Richard Kind” is voiced.
```SQL
SELECT s.NAME AS STUDIO_NAME, s.LOCATION, cs.TITLE AS CARTOON_SERIAL_TITLE
FROM STUDIOS s
JOIN CARTOON_SERIALS cs ON s.STUDIO_ID = cs.STUDIO_ID
JOIN CARTOON_ACTORS csa ON cs.CARTOON_SERIAL_ID = csa.CARTOON_SERIAL_ID
JOIN ACTORS a ON csa.ACTOR_ID = a.ACTOR_ID
WHERE a.NAME = 'Richard Kind';
```

| STUDIO_NAME | LOCATION | CARTOON_SERIAL_TITLE |
|---|---|---|
|CN|UK|Tom and Jerry|


* Write a deletion trigger, does not allow to deleting current year Cartoon-Serials.
```SQL
DELIMITER //
CREATE TRIGGER prevent_delete_current_year_cartoon_serials
BEFORE DELETE ON CARTOON_SERIALS
FOR EACH ROW
BEGIN
    DECLARE current_year INT;
    SET current_year = YEAR(CURDATE());
    IF OLD.YEAR = current_year THEN
        SIGNAL SQLSTATE '45000' 
        SET MESSAGE_TEXT = 'Cannot delete Cartoon-Serials from the current year.';
    END IF;
END;
//
DELIMITER ;
```

```SQL
CREATE TRIGGER prevent_delete_current_year_cartoon_serials BEFORE DELETE ON CARTOON_SERIALS FOR EACH ROW BEGIN DECLARE current_year INT; SET current_year = YEAR(CURDATE()); IF OLD.YEAR = current_year THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Cannot delete Cartoon-Serials from the current year.'; END IF; END;;
```


[B] Consider the following restaurant table with the following attributes - Name, address –(building, street, area, pincode), id, cuisine, nearby landmarks, online delivery-(yes/no), famous for(name of the dish) Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

```js
db.restaurants.insertMany([
  {
    "Name": "Pasta Paradise",
    "Address": {
      "building": "789",
      "street": "Indiranagar Road",
      "area": "Indiranagar",
      "pincode": "560008"
    },
    "Cuisine": "Italian",
    "NearbyLandmarks": ["100 Feet Road", "Indiranagar Metro Station"],
    "OnlineDelivery": true,
    "FamousForDish": "Alfredo Pasta"
  },
  {
    "Name": "Dilli Darbar",
    "Address": {
      "building": "1011",
      "street": "Church Street",
      "area": "Brigade Road",
      "pincode": "560025"
    },
    "Cuisine": "North Indian",
    "NearbyLandmarks": ["UB City", "Commercial Street"],
    "OnlineDelivery": true,
    "FamousForDish": "NorthIndian Thali"
  },
  {
    "Name": "Trattoria Tales",
    "Address": {
      "building": "1213",
      "street": "Koramangala 5th Block",
      "area": "Koramangala",
      "pincode": "560095"
    },
    "Cuisine": "Italian",
    "NearbyLandmarks": ["Jyoti Nivas College", "Koramangala Water Tank"],
    "OnlineDelivery": false,
    "FamousForDish": "Lasagna"
  },
  {
    "Name": "Punjab Sweets",
    "Address": {
      "building": "1415",
      "street": "Malleshwaram Main Road",
      "area": "Malleshwaram",
      "pincode": "560003"
    },
    "Cuisine": "North Indian",
    "NearbyLandmarks": ["Mantri Square Mall", "Malleshwaram Railway Station"],
    "OnlineDelivery": true,
    "FamousForDish": "Rajma Chawal"
  },
  {
    "Name": "Olive Garden",
    "Address": {
      "building": "1617",
      "street": "Richmond Road",
      "area": "Richmond Town",
      "pincode": "560025"
    },
    "Cuisine": "Italian",
    "NearbyLandmarks": ["St. Philomena's Hospital", "Trinity Circle"],
    "OnlineDelivery": true,
    "FamousForDish": "Garlic Bread"
  },
  {
    "Name": "Tuscan Tavern",
    "Address": {
      "building": "1819",
      "street": "Whitefield Main Road",
      "area": "Whitefield",
      "pincode": "560066"
    },
    "Cuisine": "Italian",
    "NearbyLandmarks": ["Phoenix Marketcity", "ITPL"],
    "OnlineDelivery": true,
    "FamousFor": "Tiramisu"
  },
  {
    "Name": "Amritsari Dhaba",
    "Address": {
      "building": "2021",
      "street": "Koramangala Inner Ring Road",
      "area": "Koramangala",
      "pincode": "560034"
    },
    "Cuisine": "North Indian",
    "NearbyLandmarks": ["Sony World Junction", "Koramangala Police Station"],
    "OnlineDelivery": false,
    "FamousForDish": "Amritsari Kulcha"
  },
  {
    "Name": "Mama Mia Pizzeria",
    "Address": {
      "building": "2223",
      "street": "Jayanagar 4th Block",
      "area": "Bengaluru",
      "pincode": "560041"
    },
    "Cuisine": "Italian",
    "NearbyLandmarks": ["Jayanagar Shopping Complex", "Jayanagar Metro Station"],
    "OnlineDelivery": true,
    "FamousForDish": "Neapolitan Pizza"
  },
  {
    "Name": "Pind Punjab",
    "Address": {
      "building": "2425",
      "street": "Bannerghatta Main Road",
      "area": "Bengaluru",
      "pincode": "560076"
    },
    "Cuisine": "North Indian",
    "NearbyLandmarks": ["IIM Bangalore", "Meenakshi Mall"],
    "OnlineDelivery": true,
    "FamousForDish": "NorthIndian Thali"
  },
  {
    "Name": "Ristorante Roma",
    "Address": {
      "building": "2627",
      "street": "Vittal Mallya Road",
      "area": "UB City",
      "pincode": "560001"
    },
    "Cuisine": "Italian",
    "NearbyLandmarks": ["UB City Mall", "Bangalore Turf Club"],
    "OnlineDelivery": false,
    "FamousForDish": "Spaghetti Carbonara"
  }
]);
```

* List the name, address and nearby landmarks of all restaurants in Bangalore where north Indian thali is available.
```js
db.restaurants.find(
	{ "Address.area": "Bengaluru", "FamousForDish": "NorthIndian Thali" },
	{ "Name": 1, "Address": 1, "NearbyLandmarks": 1, "_id": 0 }
);
```

```
[
  {
    Name: 'Pind Punjab',
    Address: {
      building: '2425',
      street: 'Bannerghatta Main Road',
      area: 'Bengaluru',
      pincode: '560076'
    },
    NearbyLandmarks: [ 'IIM Bangalore', 'Meenakshi Mall' ]
  }
]
```

* List the name and address of restaurants and also the dish the restaurant is famous for, in Bangalore where online delivery is available
```js
db.restaurants.find(
	{ "Address.area": "Bengaluru", "OnlineDelivery": true },
	{ "Name": 1, "Address": 1, "FamousForDish": 1, "_id": 0 }
);
```

```
[
  {
    Name: 'Mama Mia Pizzeria',
    Address: {
      building: '2223',
      street: 'Jayanagar 4th Block',
      area: 'Bengaluru',
      pincode: '560041'
    },
    FamousForDish: 'Neapolitan Pizza'
  },
  {
    Name: 'Pind Punjab',
    Address: {
      building: '2425',
      street: 'Bannerghatta Main Road',
      area: 'Bengaluru',
      pincode: '560076'
    },
    FamousForDish: 'NorthIndian Thali'
  }
]
```