![Root logo](https://imgur.com/Hq8xgzy.png)
# Answers

### 1. All the companies whose name match 'Babelgum'. Retrieve only their `name` field.

<!-- Your Code Goes Here -->
db.companies.find({name: "Babelgum"},{_id: 0,name: 1})

### 2. All the companies that have more than 5000 employees. Limit the search to 20 companies and sort them by **number of employees**.

<!-- Your Code Goes Here -->
db.companies.find({number_of_employees: {$gt: 5000}},{_id: 0, name: 1, number_of_employees: 1}).sort({number_of_employees: 1}).limit(20)

### 3. All the companies founded between 2000 and 2005, both years included. Retrieve only the `name` and `founded_year` fields.

<!-- Your Code Goes Here -->
db.companies.find({founded_year: {$gte: 2000, $lte: 2005}},{_id: 0, founded_year: 1, name: 1})

### 4. All the companies that had a Valuation Amount of more than 100.000.000 and have been founded before 2010. Retrieve only the `name` and `ipo` fields.

<!-- Your Code Goes Here -->
db.companies.find({$and: [{ "ipo.valuation_amount": { $gt: 100000000 } },{ founded_year: { $lt: 2010 } } ] },
  { name: 1,"ipo.valuation_amount": 1,_id: 0  })

### 5. All the companies that have less than 1000 employees and have been founded before 2005. Order them by the number of employees and limit the search to 10 companies.

<!-- Your Code Goes Here -->
db.companies.find(
   {
      founding_year: { $lt: 2005 },
      number_of_employees: { $lt: 1000 }
   }
).sort(
   {
      number_of_employees: 1
   }
).limit(10)


### 6. All the companies that don't include the `partners` field.

<!-- Your Code Goes Here -->
db.companies.find({
    "partners": { $exists: false }
})


### 7. All the companies that have a null type of value on the `category_code` field.

<!-- Your Code Goes Here -->
db.companies.find({
    $or: [
        { "category_code": null },
        { "category_code": { $exists: false } }
    ]
})


### 8. All the companies that have at least 100 employees but less than 1000. Retrieve only the `name` and `number of employees` fields.

<!-- Your Code Goes Here -->
db.companies.find(
    {
        "number_of_employees": { $gte: 100, $lt: 1000 }
    },
    {
        "_id": 0,  // Exclude the default _id field from the result
        "name": 1,
        "number_of_employees": 1
    }
)


### 9. Order all the companies by their IPO price in a descending order.

<!-- Your Code Goes Here -->
db.companies.find().sort({"ipo_price": -1})

### 10. Retrieve the 10 companies with most employees, order by the `number of employees`

<!-- Your Code Goes Here -->
db.companies.find().sort({"number_of_employees": -1}).limit(10)

### 11. All the companies founded on the second semester of the year. Limit your search to 1000 companies.

<!-- Your Code Goes Here -->
db.companies.find({
    "founding_month": { $gte: 7, $lte: 12 }  // Assuming 7-12 represents the second semester
}).limit(1000)


### 12. All the companies founded before 2000 that have an acquisition amount of more than 10.000.000

<!-- Your Code Goes Here -->
db.companies.find({
    "founding_year": { $lt: 2000 },
    "acquisition_amount": { $gt: 10000000 }
})


### 13. All the companies that have been acquired after 2010, order by the acquisition amount, and retrieve only their `name` and `acquisition` field.

<!-- Your Code Goes Here -->
db.companies.find(
    {
        "acquisition.acquired_year": { $gt: 2010 }
    },
    {
        "_id": 0,  // Exclude the default _id field from the result
        "name": 1,
        "acquisition": 1
    }
).sort(
    {
        "acquisition.price_amount": 1  // Order by acquisition amount in ascending order
    }
)


### 14. Order the companies by their `founded year`, retrieving only their `name` and `founded year`.

<!-- Your Code Goes Here -->
db.companies.find(
    {},
    {
        "_id": 0,  // Exclude the default _id field from the result
        "name": 1,
        "founding_year": 1
    }
).sort(
    {
        "founding_year": 1  // Order by founded year in ascending order
    }
)

### 15. All the companies that have been founded on the first seven days of the month, including the seventh. Sort them by their `acquisition price` in a descending order. Limit the search to 10 documents.

<!-- Your Code Goes Here -->
db.companies.find(
    {
        "founding_day": { $gte: 1, $lte: 7 }
    },
    {
        "_id": 0,  // Exclude the default _id field from the result
        "name": 1,
        "founding_day": 1,
        "acquisition.price_amount": 1
    }
).sort(
    {
        "acquisition.price_amount": -1  // Order by acquisition price in descending order
    }
).limit(10)
### 16. All the companies on the 'web' `category` that have more than 4000 employees. Sort them by the amount of employees in ascending order.

<!-- Your Code Goes Here -->
db.companies.find(
    {
        "category": "web",
        "number_of_employees": { $gt: 4000 }
    },
    {
        "_id": 0,  // Exclude the default _id field from the result
        "name": 1,
        "number_of_employees": 1
    }
).sort(
    {
        "number_of_employees": 1  // Order by number of employees in ascending order
    }
)


### 17. All the companies whose acquisition amount is more than 10.000.000, and currency is 'EUR'.

<!-- Your Code Goes Here -->
db.companies.find(
    {
        "acquisition.price_amount": { $gt: 10000000 },
        "acquisition.price_currency_code": "EUR"
    },
    {
        "_id": 0,  // Exclude the default _id field from the result
        "name": 1,
        "acquisition.price_amount": 1,
        "acquisition.price_currency_code": 1
    }

### 18. All the companies that have been acquired on the first trimester of the year. Limit the search to 10 companies, and retrieve only their `name` and `acquisition` fields.

<!-- Your Code Goes Here -->
db.companies.find(
    {
        "acquisition.acquired_month": { $gte: 1, $lte: 3 }
    },
    {
        "_id": 0,  // Exclude the default _id field from the result
        "name": 1,
        "acquisition": 1
    }
).limit(10)


### 19. All the companies that have been founded between 2000 and 2010, but have not been acquired before 2011.

<!-- Your Code Goes Here -->
db.companies.find({
    "founding_year": { $gte: 2000, $lte: 2010 },
    $or: [
        { "acquisition": { $exists: false } },
        { "acquisition.acquired_year": { $gte: 2011 } }
    ]
},
{
    "_id": 0,  // Exclude the default _id field from the result
    "name": 1,
    "founding_year": 1,
    "acquisition": 1
})