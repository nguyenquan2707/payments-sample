# payments-sample
Rest API for simple prepaid card

java 8

# 1. How to start the application ?
It is simple just execute  ``mvn spring-boot:run``

# 2. Do I need a database to run it ?
No by default it uses in-memorry database but also it is easy just to change it in application.properties if you want the tables to created in real one.

# 3. How to use the API ?

## User create
curl -i -X POST -H "Content-Type:application/json" -d '{ "username":"user@payments.com", "password":"password" }' 'http://localhost:8080/users'
``curl -i -X POST \
   -H "Content-Type:application/json" \
   -d \
'{
  "username":"user@payments.com",
  "password":"password"
}' \
 'http://localhost:8080/users'``

curl -i -X POST -H "Content-Type:application/json" -d '{ "username":"user@payments.com", "password":"password" }' 'http://localhost:8080/authorize'
## User authorize
``curl -i -X POST \
   -H "Content-Type:application/json" \
   -d \
'{ 
  "username":"user@payments.com",
  "password":"password"
}' \
 'http://localhost:8080/authorize'``
curl -i -X POST -H "Content-Type:application/json" H "Authorization:Bearer "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJ1c2VyQHBheW1lbnRzLmNvbSIsImF1ZCI6IkFVVEgiLCJpYXQiOjE2OTE5MzE1MzQsImlzcyI6IlBheW1lbnRzIiwiZXhwIjoxNjkxOTMzMzM0fQ.trloi5yOGfxjlmF270vwO1R28NczV925rFHZQy2zSMZu9Japh-Pa1cIsmdwwAbCXKe0X8imUhlFK1Rz396uSAA" -d '{ "currency":"GBP", "amount":5.5, "description":"Coffee" }' 'http://localhost:8080/payments/'
## Card create
`` curl -i -X POST \
   -H "Content-Type:application/json" \
   -H "Authorization:Bearer <TOKEN>" \
   -d \
'{
  "currency":"GBP",
  "amount":5.5,
  "description":"Coffee"
}' \
 'http://localhost:8080/payments/' ``
 
## Card topup
`` curl -i -X POST \
   -H "Content-Type:application/json" \
   -H "Authorization:Bearer <TOKEN>" \
   -d \
'{
  "currency":"GBP",
  "amount":15
}' \
 'http://localhost:8080/cards/<CARD_UID>/topup' ``

## Card balance

`` curl -i -X GET \
   -H "Authorization:Bearer <TOKEN>" \
 'http://localhost:8080/cards/<CARD_ID>/balance' ``

## Cards list
`` curl -i -X GET \
   -H "Authorization:Bearer <TOKEN>" \
 'http://localhost:8080/cards' ``

 
## Payment create

`` curl -i -X POST \
   -H "Content-Type:application/json" \
   -H "Authorization:Bearer <TOKEN>" \
   -d \
'{
  "currency":"GBP",
  "amount":5.5,
  "description":"Coffee"
}' \
 'http://localhost:8080/payments/' ``

## Payment  authorize

`` curl -i -X POST \
   -H "Content-Type:application/json" \
   -H "Authorization:Bearer <TOKEN>" \
   -d \
'{
  "card":"<CARD_UID>"
}' \
 'http://localhost:8080/payments/<PAYMENT_UID>/authorize' ``
 
## Payment capture
`` curl -i -X POST \
   -H "Content-Type:application/json" \
   -H "Authorization:Bearer <TOKEN>" \
   -d \
'{
  "card":"<CARD_UID>",
  "amount":"2"
}' \
 'http://localhost:8080/payments/<PAYMENT_UID>/capture' ``

## Payment reverse

`` curl -i -X POST \
   -H "Content-Type:application/json" \
   -H "Authorization:Bearer <TOKEN>" \
   -d \
'{
  "card":"<CARD_UID>",
  "amount":"1.5"
}' \
 'http://localhost:8080/payments/<PAYMENT_UID>/reverse' `` 
 
## Payment Refund
`` curl -i -X POST \
   -H "Content-Type:application/json" \
   -H "Authorization:Bearer <TOKEN>" \
   -d \
'{
  "card":"<CARD_UID>",
  "amount":"2.0"
}' \
 'http://localhost:8080/payments/<PAYMENT_UID>/refund' ``
