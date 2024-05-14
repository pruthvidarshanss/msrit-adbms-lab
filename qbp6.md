# `QB Program 6`

[A] Education institute is managing the on line course enrollment system. Students can enroll maximum of six courses of their choice and a maximum student to be enrolled to any course is 60. We store student details like name, USN, semester and several addresses, course details like unique title, unique id and credits.

```SQL
CREATE TABLE STUDENTS (
    USN VARCHAR(255) PRIMARY KEY,
    NAME VARCHAR(255),
    SEM INT,
    ADDRESS VARCHAR(255)
);

INSERT INTO STUDENTS (USN, NAME, SEM, ADDRESS) VALUES
('1MS23SCS17', 'Pruthvi', 1, '123 Main St'),
('1MS23SCS10', 'Jayanth', 1, '456 Elm St'),
('1MS23SCS08', 'Hrishikesh', 1, '789 Oak St');


CREATE TABLE COURSES (
    ID VARCHAR(20) PRIMARY KEY,
    TITLE VARCHAR(255) UNIQUE,
    CREDITS INT,
    MAX_ENROLLMENT INT DEFAULT 60
);

INSERT INTO COURSES (ID, TITLE, CREDITS) VALUES
('MSC11', 'ADBMS', 4),
('MSC12', 'AI', 3),
('MSC13', 'IOT', 3);


CREATE TABLE ENROLLMENT (
    STUDENT_USN VARCHAR(255),
    COURSE_ID VARCHAR(20),
    FOREIGN KEY (STUDENT_USN) REFERENCES STUDENTS(USN),
    FOREIGN KEY (COURSE_ID) REFERENCES COURSES(ID),
    PRIMARY KEY (STUDENT_USN, COURSE_ID)
);

INSERT INTO ENROLLMENT (STUDENT_USN, COURSE_ID) VALUES
('1MS23SCS17', 'MSC11'),
('1MS23SCS17', 'MSC12'),
('1MS23SCS10', 'MSC12'),
('1MS23SCS08', 'MSC11'),
('1MS23SCS08', 'MSC13');
```

* Find number of students enrolled for the course ‘ADBMS’
```SQL
SELECT COUNT(*) AS ENROLLED_STUDENTS
FROM ENROLLMENT
WHERE COURSE_ID = (SELECT ID FROM COURSES WHERE TITLE = 'ADBMS');
```

|ENROLLED_STUDENTS|
|---|
|2|

* Retrieve student names that are enrolled for AI course but not enrolled for IOT.
```SQL
SELECT s.NAME
FROM STUDENTS s
JOIN ENROLLMENT e ON e.STUDENT_USN = s.USN
JOIN COURSES c ON e.COURSE_ID = c.ID
WHERE c.TITLE = "AI"
EXCEPT
SELECT s.NAME
FROM STUDENTS s
JOIN ENROLLMENT e ON e.STUDENT_USN = s.USN
JOIN COURSES c ON e.COURSE_ID = c.ID
WHERE c.TITLE = "ADBMS";
```

|NAME|
|---|
|Jayanth|

* Write a trigger to establish the constraint that the students can enroll maximum of six courses of their choice.
```SQL
DELIMITER //

CREATE TRIGGER max_course_enrollment_constraint
BEFORE INSERT ON ENROLLMENT
FOR EACH ROW
BEGIN
    DECLARE course_count INT;
    SELECT COUNT(*) INTO course_count FROM ENROLLMENT WHERE STUDENT_USN = NEW.STUDENT_USN;
    IF course_count >= 6 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'A student can enroll a maximum of six courses.';
    END IF;
END;
//

DELIMITER ;
```

```SQL
CREATE TRIGGER max_course_enrollment_constraint BEFORE INSERT ON ENROLLMENT FOR EACH ROW BEGIN DECLARE course_count INT; SELECT COUNT(*) INTO course_count FROM ENROLLMENT WHERE STUDENT_USN = NEW.STUDENT_USN; IF course_count >= 6 THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'A student can enroll a maximum of six courses.'; END IF; END;;
```


[B] Consider the following Tourist places table with the following attributes - Place, address – (state, id), tourist attractions,best time of the year to visit,modes of transport(include nearest airport, railway station etc), accommodation, food - what not to miss for sure Create 10 collections with data relevant to the following questions. Write and execute MongoDB queries:

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

* List all the tourist places of Karnataka
```js
db.tourists_places.find({ address: "Karnataka" });
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
  }
]
```

* List the places sorted state wise
```js
db.tourist_places.find().sort({address: 1 });
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
    _id: ObjectId('664369dc7209cd00749f990a'),
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
    _id: ObjectId('664369dc7209cd00749f990b'),
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
    _id: ObjectId('664369dc7209cd00749f990c'),
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
    _id: ObjectId('664369dc7209cd00749f990d'),
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
    _id: ObjectId('664369dc7209cd00749f990e'),
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
  },
  {
    _id: ObjectId('664369dc7209cd00749f990f'),
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
    _id: ObjectId('664369dc7209cd00749f9910'),
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
    _id: ObjectId('664369dc7209cd00749f9911'),
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
    _id: ObjectId('664369dc7209cd00749f9912'),
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
    _id: ObjectId('664369dc7209cd00749f9913'),
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