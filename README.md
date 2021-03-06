

# Dave's Tech Test


![Screenshot](https://github.com/dave2591/cf/blob/master/screenshot.png?raw=true)


## Running the app

To start the app run `make currencyFair-run` (Requires docker)

I developed on Ubuntu but it should all work on Mac. If there's an error running that command let
me know.

To run tests `make run-tests`

## Tools used

Backend: Laravel, PHP 7.4, Docker, Postgres

Frontend: React, TypeScript, SASS (FE code is in /frontend-app dir)

## Approach

While this API consists of just two endpoints, I approached the task as if I were building 
the foundations of a large API.

 - Instead of traditional controllers I went with single action controllers. I find as an API grows over time
 this keeps the code base clean and you don't end up with monster controllers. They are also easier to test.
 - DB access is via repositories which return DomainObjects, making it easy to swap in elasticSearch or another data 
 store seamlessly.
 - Service classes all have just one public 'execute' method. Again, easy to test and adheres to the SRP.
 - All validation is done in custom requests so no validation logic in controllers or services. Each entity has its own 
 validator which is easily reusable.
 - Everything is Dockerised so setup 'should' be simple
 
## What I'd change with more time / What I didn't do
  - Currently the FE is polling the API, this should be using websockets
  - It would have been nice to use a time-series DB like TimeseriesDb or InfluxDB
  - The FE has no tests
  - Adding visualisation
  - The FE UI isn't responsive
  - I hackily 0777 some dirs in the setup as I didn't have time to debug docker
    
## cURL requests
 
### Create a transaction

```
curl -X POST \
  http://127.0.0.1:2591/api/transactions \
  -H 'accept: application/json' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"userId": "134256", "currencyFrom": "USD", "currencyTo": "GBP", "amountSell": 2222.45, "amountBuy": 200.10, "rate": 0.7471, "timePlaced" : "24-JAN-18 10:27:44", "originatingCountry" : "FR"} '
```
 
### Get all transactions

```
curl -X GET \
  http://127.0.0.1:2591/api/transactions \
  -H 'accept: application/json' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
```

Any questions let me know :-)

Cheers!
