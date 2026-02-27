![BookShop Architecture](./redis-node.jpg)

# 📚 BookShop Microservices

![Node.js](https://img.shields.io/badge/-Node.js-339933?style=flat-square&logo=node.js&logoColor=white)
![Redis](https://img.shields.io/badge/-Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Express](https://img.shields.io/badge/-Express-000000?style=flat-square&logo=express&logoColor=white)
[![Build Status](https://travis-ci.org/wooltar/microservices-node-redis.svg?branch=master)](https://travis-ci.org/wooltar/microservices-node-redis)

**Event-driven microservices architecture** for an online bookshop using **Node.js** + **Redis pub/sub**.

When a customer places an order:
1. 📦 **Books service** checks stock availability
2. 💳 **Customers service** validates balance & deducts payment
3. ✅ Order confirmed if stock + funds available
4. ❌ Error returned if insufficient stock or money

All communication happens via **Redis pub/sub** — no direct HTTP calls between services.

---

## 🏗️ Architecture

```
┌─────────────┐         ┌─────────────┐         ┌─────────────┐
│   Books     │         │   Orders    │         │  Customers  │
│  Service    │◄────────┤   Service   │────────►│   Service   │
│  (5544)     │  Redis  │   (8888)    │  Redis  │   (6666)    │
└─────────────┘  Pub/Sub└─────────────┘  Pub/Sub└─────────────┘
```

**Benefits:**
- ✅ **Decoupled** - services don't know about each other
- ✅ **Scalable** - add more service instances easily
- ✅ **Resilient** - one service down doesn't crash the system
- ✅ **Fast** - Redis in-memory messaging

---

## Books

Microservice to handle shop books, runs in 5544 port

### Get all books

GET http://localhost:5544/books


### Get a book

GET http://localhost:5544/books/:id'


### Create a new book

POST http://localhost:5544/books/create


### Update a book

POST http://localhost:5544/books/update


### Delete a book

DELETE http://localhost:5544/books/:id


## Customers

Microservice to handler shop customers, runs in 6666 port

### Get all customer

GET http://localhost:6666/customers


### Get a customer

GET http://localhost:6666/customers/:id'


### Create a new customer

POST http://localhost:6666/customers/create


### Update a customer

POST http://localhost:6666/customers/update


### Delete a customer

DELETE http://localhost:6666/customers/:id


## Orders

Microservice to handler shop orders, runs in 7777 port

### Get all orders

GET http://localhost:7777/orders


### Get a order

GET http://localhost:7777/orders/:id'


### Create a new order

POST http://localhost:7777/orders/create


### Update a order

POST http://localhost:7777/orders/update


### Delete a order

DELETE http://localhost:7777/orders/:id