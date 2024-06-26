# `QB Program 2`

[A] The production company is organized into different studios. We store each studio’s name branch and location; every studio must own at least one movie. We store each movie’s title, sensor_number and year of production. Star may act in any number of movies and we store each actors name and address.

```SQL
CREATE TABLE STUDIO (
  STUDIO_ID INT PRIMARY KEY, 
  NAME VARCHAR(50), 
  BRANCH VARCHAR(50), 
  LOCATION VARCHAR(50)
);

INSERT INTO STUDIO (STUDIO_ID, NAME, BRANCH, LOCATION) VALUES (1, "Hombale", "Hebbal", "Bengaluru"), (2, "Marvel", "Chicago", "USA"), (3, "DC", "London", "UK");


CREATE TABLE MOVIE (
  MOVIE_ID INT PRIMARY KEY, 
  TITLE VARCHAR(50), 
  SENSOR_NO INT, 
  YEAR_OF_PRODUCTION INT, 
  STUDIO_ID INT, 
  FOREIGN KEY (STUDIO_ID) REFERENCES STUDIO(STUDIO_ID)
);

INSERT INTO MOVIE (MOVIE_ID, TITLE, SENSOR_NO, YEAR_OF_PRODUCTION, STUDIO_ID) VALUES (1, "Kantara", 101, 2023, 1), (2, "Deadpool 3", 201, 2024, 2);


CREATE TABLE ACTORS (ACTOR_ID INT PRIMARY KEY, NAME VARCHAR(50), ADDRESS VARCHAR(100));

INSERT INTO ACTORS (ACTOR_ID, NAME, ADDRESS) VALUES (1, "Rishab Shetty", "Bengaluru"), (2, "Saptami Gowda", "Bengaluru"), (3, "Ryan Renolds", "San Andreas");

CREATE TABLE MOVIE_ACTORS (ID INT AUTO_INCREMENT PRIMARY KEY, ACTOR_ID INT, MOVIE_ID INT, FOREIGN KEY (ACTOR_ID) REFERENCES ACTORS(ACTOR_ID), FOREIGN KEY (MOVIE_ID) REFERENCES MOVIE(MOVIE_ID));

INSERT INTO MOVIE_ACTORS (ACTOR_ID, MOVIE_ID) VALUES (1, 1), (2, 1), (3, 2);
```


* List all the studios of the movie “Kantara”;
```SQL
SELECT s.NAME, s.BRANCH, s.LOCATION FROM STUDIO s, MOVIE m WHERE s.STUDIO_ID = m.STUDIO_ID AND m.TITLE = "Kantara";
```

| Name | Branch | Location |
|---|---|---|
| Hombale | Hebbal | Bengaluru |

* List all the actors , acted in a movie ‘Kantara’
```SQL
SELECT a.NAME FROM ACTORS a JOIN MOVIE_ACTORS ma ON ma.ACTOR_ID = a.ACTOR_ID JOIN MOVIE m ON ma.MOVIE_ID = m.MOVIE_ID WHERE m.TITLE = "Kantara";
```

|NAME|	
|---|
|Rishab Shetty|
|Saptami Gowda|

* Write a deletion trigger, does not allow to deleting current year movies
```SQL
DELIMITER //
CREATE TRIGGER not_delete_current_year_movie
BEFORE DELETE ON MOVIE
FOR EACH ROW
BEGIN
    DECLARE current_year INT;
    SET current_year = YEAR(CURDATE());
    IF OLD.YEAR_OF_PRODUCTION = current_year THEN
        SIGNAL SQLSTATE '45000' 
        SET MESSAGE_TEXT = 'Cannot delete movies from the current year.';
    END IF;
END;
//
DELIMITER ;
```

```SQL
CREATE TRIGGER not_delete_current_year_movie BEFORE DELETE ON MOVIE FOR EACH ROW BEGIN DECLARE current_year INT; SET current_year = YEAR(CURDATE()); IF OLD.YEAR_OF_PRODUCTION = current_year THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Cannot delete Cartoon-Serials from the current year.'; END IF; END;;
```


[B] Consider the following restaurant table with the following attributes - Name, address –(building, street, area, pincode), id, cuisine, nearby landmarks, online delivery-(yes/no), famousfor(name of the dish) Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

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

* List the name, address and nearby landmarks of all restaurants in Bangalore where north Indian thali is available
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

* List the name and address of restaurants and also the dish the restaurant is famous for, in Bangalore.
```js
db.restaurants.find(
	{ "Address.area": "Bengaluru" },
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