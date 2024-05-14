# `QB Program 5`

[A] Puppy pet shop wants to keep track of dogs and their owners. The person can buy maximum three pet dogs. We store person’s name, SSN and address and dog’s name, date of purchase and sex. The owner of the pet dogs will be identified by SSN since the dog’s names are not distinct.

```SQL
CREATE TABLE PERSON (
    SSN VARCHAR(20) PRIMARY KEY,
    NAME VARCHAR(20),
    ADDRESS VARCHAR(30)
);

INSERT INTO PERSON (SSN, NAME, ADDRESS) VALUES 
("101", "Pruthvi", "Hebbal"),
("102", "Ramesh", "Jayanagar"),
("103", "Jennifer", "Rajajinagar"),
("104", "Jenny", "BEL");


CREATE TABLE PETS (
    SSN VARCHAR(20),
    NAME VARCHAR(20),
    PURCHASE_DATE DATE,
    SEX VARCHAR(10),
    PET_PERSON_ID VARCHAR(20),
    FOREIGN KEY (PET_PERSON_ID) REFERENCES PERSON(SSN)
);

INSERT INTO PETS (SSN, NAME, PURCHASE_DATE, SEX, PET_PERSON_ID) VALUES
("D01", "Uppi", "2023-03-03", "M", "103"),
("D02", "Sonu", "2023-05-12", "F", "103"),
("D03", "Mark", "2023-07-25", "M", "102"),
("D04", "Pikachu", "2023-01-14", "F", "104"),
("D05", "Charlie", "2023-08-10", "M", "103");
```


* List all pets owned by a person ‘Ramesh’.
```SQL
SELECT p.NAME, p.PURCHASE_DATE 
FROM PETS p
JOIN PERSON o ON o.SSN = p.PET_PERSON_ID
WHERE o.NAME = "Ramesh";
```

|NAME|PURCHASE_DATE|
|---|---|
|Mark|2023-07-25|

* List all persons who are not owned a single pet
```SQL
SELECT * 
FROM PERSON o
WHERE o.SSN NOT IN (SELECT PET_PERSON_ID FROM PETS);
```

|SSN|NAME|ADDRESS|
|---|---|---|
|101|Pruthvi|Hebbal|


* Write a trigger to check the constraint that the person can buy maximum three pet dogs
```SQL
DELIMITER //
CREATE TRIGGER check_max_three_dogs 
BEFORE INSERT ON PETS
FOR EACH ROW
BEGIN 
    DECLARE DOG_COUNT INT;
    SELECT COUNT(*) INTO DOG_COUNT FROM PETS WHERE PET_PERSON_ID = New.PET_PERSON_ID;
    IF DOG_COUNT >= 3 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'A person can buy maximum three pet dogs.';
    END IF;
END;
//

DELIMITER ;
```

```SQL
CREATE TRIGGER check_max_three_dogs BEFORE INSERT ON PETS FOR EACH ROW BEGIN DECLARE DOG_COUNT INT; SELECT COUNT(*) INTO DOG_COUNT FROM PETS WHERE PET_PERSON_ID = New.PET_PERSON_ID; IF DOG_COUNT >= 3 THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'A person can buy maximum three pet dogs.'; END IF; END;;
```


[B] Consider the following Tourist places table with the following attributes - Place, address –(state, id), tourist attractions,best time of the year to visit,modes of transport(include nearest airport, railway station etc), accommodation, food - what not to miss for sureCreate 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

```js
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


* List the tourist attractions of Kerala. Exclude accommodation and food.
```js
db.tourists_places.find(
  { address: "Kerala" },
  { accommodation: 0, food: 0,  _id: 0 }
);
```

```
[
  {
    Place: 'Kovalam',
    tourist_attractions: [ 'Kovalam Beach', 'Lighthouse Beach', 'Vellayani Lake' ],
    best_time_to_visit: 'September to March',
    modes_of_transport: [
      'Trivandrum International Airport',
      'Thiruvananthapuram Railway Station'
    ]
  },
  {
    Place: 'Varkala',
    tourist_attractions: [ 'Varkala Beach', 'Janardanaswamy Temple', 'Varkala Cliff' ],
    best_time_to_visit: 'September to March',
    modes_of_transport: [ 'Trivandrum International Airport', 'Varkala Railway Station' ]
  },
  {
    Place: 'Kumarakom',
    tourist_attractions: [
      'Kumarakom Bird Sanctuary',
      'Kumarakom Backwaters',
      'Pathiramanal Island'
    ],
    best_time_to_visit: 'September to March',
    modes_of_transport: [ 'Cochin International Airport', 'Kottayam Railway Station' ]
  },
  {
    Place: 'Palakkad',
    tourist_attractions: [
      'Palakkad Fort',
      'Malampuzha Dam',
      'Silent Valley National Park'
    ],
    best_time_to_visit: 'November to February',
    modes_of_transport: [ 'Coimbatore International Airport', 'Palakkad Railway Station' ]
  },
  {
    Place: 'Kozhikode',
    tourist_attractions: [ 'Kozhikode Beach', 'Beypore Beach', 'Mananchira Square' ],
    best_time_to_visit: 'September to May',
    modes_of_transport: [ 'Calicut International Airport', 'Kozhikode Railway Station' ]
  }
]
```

* List the places sorted state wise
```js
db.tourist_places.aggregate([{ $sort: { "address.state": 1 } }]);
```

```
[
  {
    _id: ObjectId('66423f5b7c30af2bf69f9914'),
    Place: 'Bangalore Palace',
    address: 'Karnataka',
    id: 1,
    tourist_attractions: [ 'Bangalore Palace', 'Cubbon Park', 'Lalbagh Botanical Garden' ],
    best_time_to_visit: 'October to February',
    modes_of_transport: [
      'Kempegowda International Airport',
      'Bangalore City Railway Station'
    ],
    accommodation: 'Hotels and resorts',
    food: 'Masala Dosa and Filter Coffee'
  },
  {
    _id: ObjectId('66423f5b7c30af2bf69f9915'),
    Place: 'ISKCON Temple Bangalore',
    address: 'Karnataka',
    id: 2,
    tourist_attractions: [ 'ISKCON Temple', 'Vidhana Soudha', 'Wonderla Amusement Park' ],
    best_time_to_visit: 'Throughout the year',
    modes_of_transport: [
      'Kempegowda International Airport',
      'Bangalore City Railway Station'
    ],
    accommodation: 'Hotels and lodges',
    food: 'Chaat and South Indian Thali'
  },
  {
    _id: ObjectId('66423f5b7c30af2bf69f9916'),
    Place: 'Bannerghatta National Park',
    address: 'Karnataka',
    id: 3,
    tourist_attractions: [
      'Bannerghatta National Park',
      'Wonderla Amusement Park',
      'Art of Living International Center'
    ],
    best_time_to_visit: 'October to March',
    modes_of_transport: [
      'Kempegowda International Airport',
      'Bangalore City Railway Station'
    ],
    accommodation: 'Resorts and guesthouses',
    food: 'Bisi Bele Bath and Ragi Mudde'
  },
  {
    _id: ObjectId('66423f5b7c30af2bf69f9917'),
    Place: 'Ulsoor Lake',
    address: 'Karnataka',
    id: 4,
    tourist_attractions: [ 'Ulsoor Lake', 'Commercial Street', 'MG Road' ],
    best_time_to_visit: 'Throughout the year',
    modes_of_transport: [
      'Kempegowda International Airport',
      'Bangalore City Railway Station'
    ],
    accommodation: 'Hotels and budget stays',
    food: 'Pani Puri and Biryani'
  },
  {
    _id: ObjectId('66423f5b7c30af2bf69f9918'),
    Place: 'Nandi Hills',
    address: 'Karnataka',
    id: 5,
    tourist_attractions: [ 'Nandi Hills', "Tipu Sultan's Summer Palace", 'Lumbini Gardens' ],
    best_time_to_visit: 'September to May',
    modes_of_transport: [
      'Kempegowda International Airport',
      'Bangalore City Railway Station'
    ],
    accommodation: 'Resorts and cottages',
    food: 'Thatte Idli and Mysore Pak'
  },
  {
    _id: ObjectId('66423f5b7c30af2bf69f9919'),
    Place: 'Kovalam',
    address: 'Kerala',
    id: 6,
    tourist_attractions: [ 'Kovalam Beach', 'Lighthouse Beach', 'Vellayani Lake' ],
    best_time_to_visit: 'September to March',
    modes_of_transport: [
      'Trivandrum International Airport',
      'Thiruvananthapuram Railway Station'
    ],
    accommodation: 'Resorts and beachfront hotels',
    food: 'Kerala Fish Curry and Parotta'
  },
  {
    _id: ObjectId('66423f5b7c30af2bf69f991a'),
    Place: 'Varkala',
    address: 'Kerala',
    id: 7,
    tourist_attractions: [ 'Varkala Beach', 'Janardanaswamy Temple', 'Varkala Cliff' ],
    best_time_to_visit: 'September to March',
    modes_of_transport: [ 'Trivandrum International Airport', 'Varkala Railway Station' ],
    accommodation: 'Resorts and guesthouses',
    food: 'Kerala Thali and Banana Chips'
  },
  {
    _id: ObjectId('66423f5b7c30af2bf69f991b'),
    Place: 'Kumarakom',
    address: 'Kerala',
    id: 8,
    tourist_attractions: [
      'Kumarakom Bird Sanctuary',
      'Kumarakom Backwaters',
      'Pathiramanal Island'
    ],
    best_time_to_visit: 'September to March',
    modes_of_transport: [ 'Cochin International Airport', 'Kottayam Railway Station' ],
    accommodation: 'Luxury resorts and houseboats',
    food: 'Kerala Sadya and Toddy'
  },
  {
    _id: ObjectId('66423f5b7c30af2bf69f991c'),
    Place: 'Palakkad',
    address: 'Kerala',
    id: 9,
    tourist_attractions: [
      'Palakkad Fort',
      'Malampuzha Dam',
      'Silent Valley National Park'
    ],
    best_time_to_visit: 'November to February',
    modes_of_transport: [ 'Coimbatore International Airport', 'Palakkad Railway Station' ],
    accommodation: 'Hotels and resorts',
    food: 'Kerala Biriyani and Halwa'
  },
  {
    _id: ObjectId('66423f5b7c30af2bf69f991d'),
    Place: 'Kozhikode',
    address: 'Kerala',
    id: 10,
    tourist_attractions: [ 'Kozhikode Beach', 'Beypore Beach', 'Mananchira Square' ],
    best_time_to_visit: 'September to May',
    modes_of_transport: [ 'Calicut International Airport', 'Kozhikode Railway Station' ],
    accommodation: 'Hotels and homestays',
    food: "Kerala Halwa and Paragon's Biriyani"
  }
]
```