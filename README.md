# Gramoday - Assignment

## Problem Statement

To build an express JS API web-service which captures user contributed reports and returns an aggregate report in response.

### Prerequisite Installations

- Node Js
- MongoDB

### Instructions to set up project locally

1. Download zip file and extract it

2. Go to command prompt -> `cd` into the main folder directory
3. install the dependencies using -> `npm i`
4. now `npm run dev` or `nodemon index.js`
5. visit `http://localhost:8000/` to view the application locally

> Note :
>
> - Install Robo-3T for visual interface of Data in MongoDB
>
> - Install Postman for testing

### Working of API

#### Post: Send a create report request

The algorithm first checks in the database, if the report provided is already present or not.

The comparison is done by comparing Market ID and Commodity ID with each report.

If the report is not present, the report gets added on the database. Price unit is updated to "kg" and price is updated to average price by

$$
report.price = report.price/report.convFctr
$$

If the report is present, then check if the user has already submitted the report or not, and also check that not more than 2 user can contribute to report. If both conditions are satisfied, then append the user in `userID` list. And update the average price.

#### Get: Get the aggregated report

The algorithm first checks if reportID is given or not. If not given return with `status(400)` Error. If reportID is provided, then search in the whole Database by comparing \_id with reportID. Return the report if found else throw not found error.

#### Delete: Delete the aggregated report

Similar to Get requests, first it is checked if reportID is given or not. return with `status(400)` and if reportID is provided. find the report by ID and then delete it from the database

## Testing of API

### 1. Send a create report request

**Request-1:**

POST /reports

`{ `

​ `"reportDetails": { ` ```

`"userID": "user-1", "marketID": "market-1", "marketName": "Vashi Navi Mumbai", "cmdtyID": "cmdty-1", "marketType": "Mandi", "cmdtyName": "Potato", "priceUnit": "Pack", "convFctr": 50, "price": 700` `}`

`}`

[Request - 1 : Image](https://drive.google.com/file/d/1srXPK_2KJIcbj-vcOUcxa-kzUXVdPTM1/view?usp=sharing)

**Response-1:**

`{ status: "success", reportID: "a429ddb4-d046-457a-bb17-709466fb679e" }`

[Response-1 : Image](https://drive.google.com/file/d/1i82ZReyuujZKdOBI2XpsZwxfxoUqw6Y8/view?usp=sharing)

> <img src="C:\Users\abhin\OneDrive\Pictures\Screenshots\request - 1.png" alt="request - 1" style="zoom:50%;" /> <img src="C:\Users\abhin\OneDrive\Pictures\Screenshots\response 1.png" alt="response 1" style="zoom:50%;" />

**Request-2:**

POST /reports

`{ `

​ `"reportDetails": { `

`"userID": "user-2", "marketID": "market-1", "marketName": "Vashi Navi Mumbai", "cmdtyID": "cmdty-1", "cmdtyName": "Potato", "priceUnit": "Quintal", "convFctr": 100, "price": 1600 ` }

`}`

[Resquest-2 : Image](https://drive.google.com/file/d/1HtYV-K7FjroEd-wUw1665AzHdUj8JrkI/view?usp=sharing)

**Response-2: **

`{ status: "success", reportID: "a429ddb4-d046-457a-bb17-709466fb679e" }`

[Response-2 : Image](https://drive.google.com/file/d/1fzquGt5kHTDG0Raedbw9gO97WO-WOTri/view?usp=sharing)

> <img src="C:\Users\abhin\OneDrive\Pictures\Screenshots\request-2.png" alt="request-2" style="zoom:50%;" />
>
> <img src="C:\Users\abhin\OneDrive\Pictures\Screenshots\response 2.png" alt="response 2" style="zoom:50%;" />

#### Robo 3T Visualization of MongoDB

[Robo 3T : Image](https://drive.google.com/file/d/1nzst8iZmS6BLvMGBqvnzQ_2hyqyQZkWP/view?usp=sharing)

> <img src="C:\Users\abhin\OneDrive\Pictures\Screenshots\robo-3T - 1.png" alt="robo-3T - 1" style="zoom:50%;" />

### 2. Get the aggregated report

**Request GET /reports?reportID=a429ddb4-d046-457a-bb17-709466fb679e**

[Aggragated report : Image](https://drive.google.com/file/d/13K1C0CcXGqxqcWQ85yrOXD3HrGYqmcTi/view?usp=sharing)

> <img src="C:\Users\abhin\OneDrive\Pictures\Screenshots\get - 1.png" alt="get - 1" style="zoom:50%;" />

### 3. Delete the aggregated report

**Request Delete /reports?reportID=a429ddb4-d046-457a-bb17-709466fb679e**

[Delete report result : Image](https://drive.google.com/file/d/1oxtdL6M30Y4QXCgU76bs0eQZd9q0VenY/view?usp=sharing)

> <img src="C:\Users\abhin\OneDrive\Pictures\Screenshots\delete -1.png" alt="delete -1" style="zoom:50%;" />
