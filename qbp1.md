# `QB Program 1`

[A] Suppose a movie_studio has several film crews. The crews might be designated by a given studio as crew1, crew 2, and so on. However, other studios might use the same designations for crews, so the attribute crew_number is not a key for crews. Movie_studio holds the information like name, branch and several locations. Each crew holds information like sector and strength.

```SQL
CREATE TABLE MOVIE_STUDIO (
    STUDIO_ID INT(3) PRIMARY KEY,
    NAME VARCHAR(50) NOT NULL,
    BRANCH VARCHAR(50),
    LOCATION VARCHAR(50)
);

INSERT INTO movie_studio (STUDIO_ID, NAME, BRANCH, LOCATION) VALUES
    (1, 'Hombale', 'Bengaluru', 'India'),
    (2, 'Marvel', 'Washington', 'USA'),
    (3, 'Yash Raj', 'Mumbai', 'India'),
    (4, 'DC Comics', 'London', 'UK'),
    (5, 'Horror', 'Chicago', 'UK');

CREATE TABLE CREWS (
    CREW_NO INT(3),
    STUDIO_ID INT(3) NOT NULL,
    SECTOR VARCHAR(50),
    STRENGTH INT(3),
    FOREIGN KEY (STUDIO_ID) REFERENCES MOVIE_STUDIO(STUDIO_ID)
);

INSERT INTO crews (CREW_NO, STUDIO_ID, SECTOR, STRENGTH) VALUES
    (10, 1, 'Sector A', 8),
    (16, 1, 'Sector B', 6),
    (11, 2, 'Sector C', 10),
    (12, 2, 'Sector D', 7),
    (13, 2, 'Sector E', 9),
    (14, 3, 'Sector F', 5),
    (15, 3, 'Sector G', 4),
    (12, 4, 'Sector H', 4),
    (15, 4, 'Sector I', 4);
```

* List all movie studios which are not used a single crews.

```SQL
SELECT NAME FROM MOVIE_STUDIO WHERE STUDIO_ID NOT IN (SELECT STUDIO_ID FROM CREWS);
```

| NAME |
|---|
| Horror |


* Retrieve the movie studio which uses highest strength crew.

```SQL
SELECT ms.NAME, c.STRENGTH
FROM MOVIE_STUDIO ms
JOIN CREWS c ON ms.STUDIO_ID = c.STUDIO_ID
ORDER BY c.STRENGTH DESC
LIMIT 1;
```

| NAME | STRENGTH |
|---|---|
| Marvel | 10 |

* Write a before insert trigger to check maximum number of crews to any studio is limited to 10.

```sql
DELIMITER //
CREATE TRIGGER max_crew_limit_check
BEFORE INSERT ON CREWS
FOR EACH ROW
BEGIN
    DECLARE studio_crew_count INT;
    SELECT COUNT(*) INTO studio_crew_count
    FROM CREWS
    WHERE STUDIO_ID = NEW.STUDIO_ID;
    
    IF studio_crew_count >= 10 THEN
        SIGNAL SQLSTATE '45000' 
        SET MESSAGE_TEXT = 'Maximum crew limit (10) reached for this movie studio.';
    END IF;
END;
//
DELIMITER ;
```

```SQL
CREATE TRIGGER max_crew_limit_check BEFORE INSERT ON CREWS FOR EACH ROW BEGIN DECLARE studio_crew_count INT; SELECT COUNT(*) INTO studio_crew_count FROM CREWS WHERE STUDIO_ID = NEW.STUDIO_ID; IF studio_crew_count >= 10 THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Maximum crew limit (10) reached for this movie studio.'; END IF; END;;
```

[B] Consider the following restaurant database with the following attributes - Name, address – (building, street, area, pincode), id, cuisine, nearby landmarks, online delivery- yes/no, famous for (name of the dish). Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

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

* List the name and address of all restaurants in Bangalore with Italian cuisine.

```js
db.restaurants.find(
  { "Address.area": "Bengaluru", "Cuisine": "Italian" },
  { "Name": 1, "Address": 1, "_id": 0 }
);
```

* List the name, address and nearby landmarks of all restaurants in Bangalore where north Indianthali is available.

```js
db.restaurants.find(
	{ "Address.area": "Bengaluru", "FamousForDish": "NorthIndian Thali" },
	{ "Name": 1, "Address": 1, "NearbyLandmarks": 1, "_id": 0 }
);
```
