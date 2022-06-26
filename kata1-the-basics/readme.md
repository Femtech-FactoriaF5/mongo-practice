# THE RESTAURANT

## Intro
We have developed a mongoDB database for our Restaurant Client App. Now it is time to test that all the queries that the App will issue, are running correctly.

## Queries
We should issue the next queries:

1. Find the restaurant with id 30112340.
    db.restaurants.find({restaurant_id: "30112340"})

2. Find May May Kitchen.
    db.restaurants.find({name: "May May Kitchen"})

3. Find the restaurants where their cuisine is Tapas.
     db.restaurants.find({cuisine:"Tapas"})

4. Find the restaurants in postal code 11208.
    db.restaurants.find({"address.zipcode":"11208"}).pretty()

5. Find all restaurants that have a score greater or equal than 70.
    db.restaurants.find({"grades.score":{$gte:70}}).pretty()

6. Find all restaurants in Brooklyn that have a score greater than 80
     db.restaurants.find({$and:[{"borough":"Brooklyn"},{"grades.score":{$gt:80}}]}).pretty()

7. All restaurants with Chilean or Czech cuisine.
     db.restaurants.find({$or:[{"cuisine":"Chilean"},{"cuisine":"Czech"}]}).pretty()

8. All restaurants with grade A in second position of the array.
     db.restaurants.find({"grades.1.grade":"A"}).pretty()

9. All restaurants with grades A or B.
     db.restaurants.find({$or:[{"grades.grade":"A"},{"grades.grade":"B"}]}).pretty()

10. All restaurants that have a review made in 2014-09-16.
     db.restaurants.find({"grades.date":ISODate("2014-09-16T00:00:00Z")}).pretty()

11. All restaurant their cuisine is Tapas ordered by name in ascending (normal) order.
     db.restaurants.find({cuisine:"Tapas"}).sort({name:1})

12. How many restaurants have been graded after 2015-01-01.
    db.restaurants.find({"grades.date":{$gt:ISODate("2015-01-01T00:00:00Z")}}).count()

### Steps

To prepare the test environment:
1. Fork this repository
2. Clon your forked repository to local
3. Open a terminal pointing to the cloned folder and run the next command:

```bash
mongoimport --db restaurants --collection restaurants --file primer-dataset.json
```
To run the tests:

4. Open the mongo shell (mongo terminal client) with the `mongo` command
5. Run the queries to solve the exercise
6. Copy all the queries into the readme.md document.
7. Push changes to your forked repositories.
8. Issue a pull-request to the original kata repository with your name.

