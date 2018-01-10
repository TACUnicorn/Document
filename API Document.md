# API Document

[TOC]



## Warehouse

### Use Scenario

- Put the raw material in the warehouse.


- The factory  fetch raw material from the warehouse.


- The factory or foundry put the product in the warehouse.
- The background management system check the inventory in warehouse.
- The background management system fetch product from the warehouse.

### ER Design

- product_transfer

  | domain     | type | comment             |
  | ---------- | ---- | ------------------- |
  | id         |      |                     |
  | number     |      |                     |
  | time       |      |                     |
  | product_id |      |                     |
  | type       |      | Put / fetch         |
  | state      |      | processing/finished |

- product

  | domain | type | comment |
  | ------ | ---- | ------- |
  | id     |      |         |
  | name   |      |         |
  | price  |      |         |
  | remain |      |         |

- material

  | domain | type | comment |
  | ------ | ---- | ------- |
  | id     |      |         |
  | name   |      |         |
  | number |      |         |

- material_transfer

  | domain      | type | comment            |
  | ----------- | ---- | ------------------ |
  | id          |      |                    |
  | remain      |      |                    |
  | time        |      |                    |
  | material_id |      |                    |
  | type        |      | Put / fetch        |
  | state       |      | Processin/finished |

### API

- Product Information
  - Check Product list

    - URL `GET /warehouse/products  `

    - Authority `SUPER` `PRODUCT_MANAGEMENT`

    - Response

      ```json
      {
          "code": 200,
          "message": "success",
          "content": [
              {
                  "id": 1,
                  "name": "iphone X",
                  "description": "Our vision has always been to create an iPhone that is entirely screen. One so immersive the device itself disappears into the experience. And so intelligent it can respond to a tap, your voice, and even a glance. With iPhone X, that vision is now a reality. Say hello to the future.",
                  "price": 8388,
                  "num": 270
              }
          ]
      }
      ```

  - Create new product entry

    - URL  `POST /warehouse/product`

    - Authority `SUPER` `CREATE_PRODUCT`

    - Body

      ```json
      {
        "name": "Mac Pro", 
        "description": "Mac has always been built around a singular vision: to create machines that are as powerful and functional as they are beautiful and intuitive. Mac Pro is a stunning realization of that ideal. All the elements that define a pro computer — graphics, storage, expansion, processing power, and memory — have been rethought and reengineered. So you have the power and performance to bring your biggest ideas to life.", 
        "price": 21888
      }
      ```

  - Modify product info

    - URL `PUT /warehouse/product/{product_id}`

    - Body

      ```json
      {
        "name": "Mac Pro", 
        "description": "Mac has always been built around a singular vision: to create machines that are as powerful and functional as they are beautiful and intuitive. Mac Pro is a stunning realization of that ideal. All the elements that define a pro computer — graphics, storage, expansion, processing power, and memory — have been rethought and reengineered. So you have the power and performance to bring your biggest ideas to life.", 
        "price": 20888
      }
      ```

- Product Transfer

  - View transfer history

    - URL `GET /warehouse/product/transfers?start=date&end=date&state=()`

    - Body

      ```json
      {
          "code": 200,
          "message": "success",
          "content": [
              {
                  "id": 2,
                  "num": 10,
                  "name": "iphone X",
                  "p_id": 1,
                  "type": 0,
                  "state": 1,
                  "time": 1515520763000
              },
              {
                  "id": 3,
                  "num": 10,
                  "name": "iphone X",
                  "p_id": 1,
                  "type": 0,
                  "state": 1,
                  "time": 1515521834000
              },
              {
                  "id": 4,
                  "num": 100,
                  "name": "iMac pro",
                  "p_id": 2,
                  "type": 0,
                  "state": 1,
                  "time": 1515524462000
              },
              {
                  "id": 5,
                  "num": 100,
                  "name": "iMac pro",
                  "p_id": 2,
                  "type": 0,
                  "state": 1,
                  "time": 1515524465000
              }
          ]
      }
      ```



  - Put/Fetch product request

    - URL `POST /warehouse/product/put(or fetch)`

    - Authority `SUPER` `PUT_PRODUCT` `FETCH_PRODUCT`

    - Body

      ```json
      {
          "p_id": 2,
          "num": 2,
      }
      ```

  - Accept Transfer

    - URL `PUT /warehouse/product/transefer/{transfer_id}?state=?`

    - Body

      ```json

      ```


- Material

  - URL  `POST /material`
  - The same as product


## Factory

### Use Scenario

- The backstage management system place order to factory
- Confirm order
- The backstage management system check task information

### ER Design

| Domain     |      |      |
| ---------- | ---- | ---- |
| Id         |      |      |
| product_id |      |      |
| number     |      |      |
| state      |      |      |
| time       |      |      |

### API

- Place Order

  - URL: `POST /factory/order`

  - Body

    ```json
    {
      "id" = 1,
      "num" = 1,
    }
    ```

- Update order

  - URL: `PUT /factory/order`

  - Body

    ```json
    {
      "id": 1,
      "p_id": 1,
      "num": 500,
      "state": 1,
      "time": 1515497018000
    }
    ```

- View order

  - URL: `GET /facotry/orders`

  - Body

    ```json
    {
        "code": 200,
        "message": "success",
        "content": [
            {
                "id": 1,
                "state": 0,
                "p_id": 1,
                "num": 50,
                "time": 1515497015000
            },
            {
                "id": 2,
                "state": 0,
                "p_id": 1,
                "num": 50,
                "time": 1515497018000
            }
        ]
    }
    ```


## OEM Adapter

### API

- post order

  ```
  POST http://10.0.1.2:8000/oem/order

  User => Management
  RequestBody {materialId, materialName, materialNo, oem}
  Response {code} "0" is ok, "1" is error
  ```

- get order

  ```
  GET http://10.0.1.2:8000/oem/order

  User => Management
  Response {[orderId, materialId, materialName, materialNo, amount, time, oem]}
  ```

### ER Design

| Domain        |      |      |
| ------------- | ---- | ---- |
| order_id      |      |      |
| material_id   |      |      |
| material_name |      |      |
| material_no   |      |      |
| amount        |      |      |
| time          |      |      |
| oem           |      |      |

## Components Adapter

### API

- post order

  ```
  POST http://10.0.1.2:8086/components/order

  User => Management
  RequestBody {componentsId, componentsName, componentsNo}
  Response {code} "0" is ok, "1" is error
  ```

### ER Design

| Domain       |      |      |
| ------------ | ---- | ---- |
| order_id     |      |      |
| component_id |      |      |
| component_no |      |      |
| amount       |      |      |
| time         |      |      |

## Bank Adapter

### API

- transfer

  ```
  POST http://10.0.1.2:8085/bank/transfer 

  User => FinanceSystem
  RequestBody {fromAcount, toAccount, sum}
  Response {code} "0" is ok, "1" is error
  ```

- view balance

  ```
  User => User
  GET http://10.0.1.2:8085/bank/balance/{account}
  Response {num} num is balance
  ```

## Finance Service

### API

- transfer

  URL:  

  ```
  http://10.0.1.2:3223/finance/transfer
  ```

  POST:

  ```
  User => Management
  RequestBody {"fromAccount":"1552730","toAccount":"1552732", "sum":110000}
  ```

  Response:

  ```
  {
      "code": 200,
      "message": "success",
      "content": "0"
  }
  ```

- view bill

### ER Design

| Domain      |      |                               |
| ----------- | ---- | ----------------------------- |
| id          |      |                               |
| type        |      | Customer/oem/commpent/experss |
| relation_id |      |                               |
| amount      |      |                               |
| time        |      |                               |

URL

```
http://10.0.1.2:3224/finance/bill?start=2017-12-30
```

HTTP Mode

```
User => Management
RequestBody {fromDate, toDate}
Response {bills} the list of bill from one stage to another stage
```

Response

```
{
    "code": 200,
    "message": "success",
    "content": [
        {
            "fromAccount": "1552700",
            "toAccount": "1552701",
            "sum": 100000
        },
        {
            "fromAccount": "1552730",
            "toAccount": "1552732",
            "sum": 110000
        }
    ]
}
```

## Express Adapter

### API

- post order

  URL

  ```
  http://10.0.1.2:8001/express/deliver
  ```

  HTTP Mode

  ```
  POST
  ```

  RequstBody

  ```
  {
      fromUser:
      toUser:
      source: 
      destination: 
      fromUserPhone: 
      toUserPhone:
  }
  ```

  Response

  ```
  {
      "code": 200,
      "message": "success",
      "content": 
  }
  ```

- view express

  URL

  ```
  http://10.0.1.2:8001/express/deliveries
  ```

  HTTP Mode

  ```
  GET
  ```

  Response

  ```
  {
      "code": 200,
      "message": "success",
      "content": [
          {
              "id": 0,
              "fromUser": "Phoenix",
              "fromUserPhone": "18000000001",
              "toUser": "Hadoop",
              "toUserPhone": "18000000001",
              "source": "Tongji University",
              "destination": "Tongji University, Caoan HighWay",
              "time": 1515569827000,
              "state": 0
          },
          {
              "id": 0,
              "fromUser": "Phoenix",
              "fromUserPhone": "18000000001",
              "toUser": "Hadoop",
              "toUserPhone": "18000000001",
              "source": "Tongji University",
              "destination": "Tongji University, Caoan HighWay",
              "time": 1515569796000,
              "state": 0
          }
      ]
  }
  ```

### ER Design

| Domain      |      |      |
| ----------- | ---- | ---- |
| id          |      |      |
| order_id    |      |      |
| state       |      |      |
| create_time |      |      |
