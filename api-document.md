### Warehouse

#### Use Scenario

- **Put the raw material in the warehouse.**


- **The factory  fetch raw material from  from the warehouse.**


- The factory or foundry put the product in the warehouse.
- The background management system check the inventory in warehouse.
- The background management system fetch product from the warehouse.

#### Put Product

URL

```
http://localhost:2224/warehouse/put
```

HTTP Mode

```
POST {"id":1,"num":10}
```
Response
```
{
    "code": 200,
    "message": "success",
    "content": "true"
}
```

Request Parameter

| name |  type  |     Meaning     |
| :--: | :----: | :-------------: |
|  id  | string |   product id    |
| num  |  int   | product  amount |

#### Check Inventory

URL

```
http://localhost:2224/warehouse/view?id=1
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
    "content": {
        "id": 1,
        "name": "iphoneX",
        "description": "the best mobile in the world",
        "num": 50
    }
}
```
Request Parameter

| name |  type  |  Meaning   |
| :--: | :----: | :--------: |
|  id  | string | product id |

#### Fetch Product

URL
```
http://localhost:2224/warehouse/fetch
```

HTTP Mode

```
POST {"id":1,"num":10}
```

Response
```
{
    "code": 200,
    "message": "success",
    "content": ""
}
```
Request Parameter

| name |  type  |    Meaning     |
| :--: | :----: | :------------: |
|  id  | string |   product id   |
| num  |  int   | product amount |

### Factory

#### Use Scenario

- The backstage management system place order to factory
- The backstage management system check task information

#### Place Order

URL

```
http://localhost:4224/factory/place
```

HTTP Mode

```
POST {"id":1,"num":10}
```
Response
```
{
    "code": 200,
    "message": "success",
    "content": "1"
}
```

Request Parameter

| name |  type  |   Meaning   |
| :--: | :----: | :---------: |
|  id  | string |   task id   |
| num  |  int   | task amount |

#### Check Task

URL

```
http://localhost:4224/factory/check?id=1
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
    "content": {
        "id": 1,
        "progress": 10,
        "p_id": 1,
        "num": 50
    }
}
```
Request Parameter

| name |  type  | Meaning |
| :--: | :----: | :-----: |
|  id  | string | task id |





### OEM

#### 1. post order

```
POST http://10.0.1.2:8000/oem/order

User => Management
RequestBody {materialId, materialName, materialNo}
Response {orderId}
```

#### 2.get order

```
GET http://10.0.1.2:8000/oem/get/{orderId}

User => Management
Response {orderId, materialId, materialName, materialNo, amount, time}
```

### Components

#### 1. post order

```
POST http://ip:port/components/order

User => Management
RequestBody {componentsId, componentsName, componentsNo}
Response {code} "0" is ok, "1" is error
```

### Authentication

#### 1. login

```
POST http://ip:port/authentication

User => User
RequestBody {username, password}
Response {cookie, userInfo}
```

### External

#### 1. get info

```
GET http://ip:port/item/info/{id}

User => Management
RequestBody {itemId}
Response {itemInfo}
```

#### 2. post order

```
POST http://ip:port/item/order

User => Management
RequestBody {orderId, orderItems}
Response {code} "0" is ok, "1" is error
```

#### 3. check inventory

```
GET http://ip:port/item/inventory/{id}

User => Management
RequestBody {itemId}
Response {itemNo}
```





### Bank

#### 1. transfer

```
POST http://ip:port/bank/transfer 

User => FinanceSystem
RequestBody {fromAcount, toAccount, sum}
Response {code} "0" is ok, "1" is error
```

#### 2. view balance

```
User => User
GET http://ip:port/bank/balance/{account}
Response {num} num is balance
```

### Finance Service

#### 1. transfer

URL
```
http://localhost:3223/finance/transfer
```
POST 
```
User => Management
RequestBody {"fromAccount":"1552730","toAccount":"1552732", "sum":110000}
```

Response
```
{
    "code": 200,
    "message": "success",
    "content": "0"
}
```

#### 2. view bill

URL
```
http://localhost:3224/finance/bill?start=2017-12-30 15:54:25&end=2017-12-31 17:54:25
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


### Express

#### 1.post order
URL
```
http://ip:port/express/deliver
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

#### 2.view express
URL
```
http://ip:port/express/deliveries
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
    "content": []
}
```