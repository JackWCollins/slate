---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the TurnSignal API! This is a sample coding project - the source code is located [here](https://github.com/lord/slate). You can use our API to access TurnSignal API endpoints, which can get information on various vehicles, makes, models, options.

# Authentication

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: turnsignal"
```

TurnSignal uses API keys to allow access to the API. Since this is just a sample application, pass the authorization header of `turnsignal`.

TurnSignal expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: turnsignal`

# Makes

## Make object

This object defines the vehicle `make`, such as Ford, Nissan, Subaru, etc. This object can have many `models`. 

```json
{
  "id":95,
  "name":"Mazda",
  "models": [
    {
      "id": 343,
      "name": "ZX5"
    }
  ]
}
```

### Object attributes

Attribute  | Description
---------  | -----------
id | The primary key of the object
name | The name of the make

## Get All Makes

```shell
curl "https://turn-signal.herokuapp.com/makes"
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":96,
    "name":"McLaren",
    "models": []
  },
  {
    "id":95,
    "name":"Mazda",
    "models": [
      {
        "id": 343,
        "name": "ZX5"
      }
    ]
  }
]
```

This endpoint retrieves vehicle makes (paginated 25 per page).

### HTTP Request

`GET https://turn-signal.herokuapp.com/makes`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Get a specific page of results

## Get a Specific Make

```shell
curl "https://turn-signal.herokuapp.com/makes/95"
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
{
  "id":95,
  "name":"Mazda"
}
```

This endpoint retrieves a specific vehicle make.


### HTTP Request

`GET https://turn-signal.herokuapp.com/makes/<ID>`

### Parameters

Parameter | Description
--------- | -----------
ID | The ID of the make to retrieve

## Create a Make

```shell
curl "https://turn-signal.herokuapp.com/makes"
  -H "Authorization: turnsignal"
  -H "Content-Type: application/json"
  -X POST
  -d '{"make": {"name":"Tesla"}}'
```

> The above command returns JSON structured like this:

```json
{
  "id":101,
  "name":"Tesla"
}
```

This endpoint creates a specific make. Note, duplicate make `names` are not allowed.

### Parameters

Parameter | Description
--------- | -----------
name | The name of the vehicle make

## Update a Make

```shell
curl "https://turn-signal.herokuapp.com/makes/101"
  -H "Authorization: turnsignal"
  -H "Content-Type: application/json"
  -X PATCH
  -d '{"make": {"name":"Tesla 2"}}'
```

> The above command returns JSON structured like this:

```json
{
  "id":101,
  "name":"Tesla 2"
}
```

This endpoint updates a specific make. Note, duplicate make `names` are not allowed.

### Parameters

Parameter | Description
--------- | -----------
ID | The ID of the make to update
name | The updated name of the make

## Delete a Make

```shell
curl "https://turn-signal.herokuapp.com/makes/95"
  -X DELETE
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
{
  "id":69,
  "name":"Chrysler"
}
```

This endpoint deletes a specific make.

### HTTP Request

`DELETE https://turn-signal.herokuapp.com/makes/95`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the make to delete


# Models

## Model object

This object defines the vehicle `model`. For example, the Subaru `make` would have `models` of Outback, Forester, Impreza, etc.

```json
{
  "id": 355,
  "name": "Forester",
  "make": {
      "id": 37,
      "name": "Subary"
  },
  "options": []
}
```

### Object attributes

Attribute  | Description
---------  | -----------
id | The primary key of the object
name | The name of the model
make | The `make` object for the model
options | The available `options` for this model.

## Get All Models

```shell
curl "https://turn-signal.herokuapp.com/models"
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 355,
    "name": "Land Cruiser",
    "make": {
        "id": 37,
        "name": "Toyota"
    },
    "options": []
  },
  {
    "id": 354,
    "name": "BRZ",
    "make": {
        "id": 4,
        "name": "Subaru"
    },
    "options": [
      {
        "id": 1,
        "name": "All wheel drive"
      }
    ]
  }
]
```

This endpoint retrieves vehicle models (paginated 25 per page). It also returns the make of the model as well as any `options` or `vehicles` for this model.

### HTTP Request

`GET https://turn-signal.herokuapp.com/models`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Get a specific page of results

## Get a Specific Model

```shell
curl "https://turn-signal.herokuapp.com/models/95"
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
{
  "id":95,
  "name":"Mazda"
}
```

This endpoint retrieves a specific vehicle model.


### HTTP Request

`GET https://turn-signal.herokuapp.com/models/<ID>`

### Parameters

Parameter | Description
--------- | -----------
ID | The ID of the model to retrieve

## Create a Model

```shell
curl "https://turn-signal.herokuapp.com/models"
  -H "Authorization: turnsignal"
  -H "Content-Type: application/json"
  -X POST
  -d '{"model": {"name":"Roadster", "make_id":97}}'
```

> The above command returns JSON structured like this:

```json
{
  "id":150,
  "name":"Roadster",
  "make": {
    "id": 97,
    "name": "Tesla"
  }
}
```

This endpoint creates a specific model.

### Parameters

Parameter | Description
--------- | -----------
name | The name of the model
make_id | The ID of the Make that this model belongs to.

## Update a Model

```shell
curl "https://turn-signal.herokuapp.com/models/101"
  -H "Authorization: turnsignal"
  -H "Content-Type: application/json"
  -X PATCH
  -d '{"model": {"name":"Roadster 2"}}'
```

> The above command returns JSON structured like this:

```json
{
  "id":150,
  "name":"Roadster 2",
  "make": {
    "id": 97,
    "name": "Tesla"
  }
}
```

This endpoint updates a specific model. Note, duplicate model `names` are not allowed.

### Parameters

Parameter | Description
--------- | -----------
ID | The ID of the model to update
name | The updated name of the model
make_id | The updated `make.id` of the model

## Delete a Model

```shell
curl "https://turn-signal.herokuapp.com/models/95"
  -X DELETE
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
{
  "id":150,
  "name":"Roadster 2"
}
```

This endpoint deletes a specific model.

### HTTP Request

`DELETE https://turn-signal.herokuapp.com/models/95`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the model to delete

# Options

## Option object

This object defines the available options that a vehicle or model could have. For example, All wheel drive, sun roof, etc.

```json
{
  "id": 355,
  "name": "Forester",
  "make": {
      "id": 37,
      "name": "Subary"
  },
  "options": []
}
```

### Object attributes

Attribute  | Description
---------  | -----------
id | The primary key of the object
name | The name of the option

## Get All Options

```shell
curl "https://turn-signal.herokuapp.com/options"
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":96,
    "name":"All wheel drive"
  },
  {
    "id":100,
    "name":"Sun roof"
  }
]
```

This endpoint retrieves vehicle options (paginated 25 per page).

### HTTP Request

`GET https://turn-signal.herokuapp.com/options`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Get a specific page of results

## Get a Specific Option

```shell
curl "https://turn-signal.herokuapp.com/options/95"
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
{
  "id":95,
  "name":"All wheel Drive"
}
```

This endpoint retrieves a specific vehicle option.


### HTTP Request

`GET https://turn-signal.herokuapp.com/options/<ID>`

### Parameters

Parameter | Description
--------- | -----------
ID | The ID of the option to retrieve

## Create a Option

```shell
curl "https://turn-signal.herokuapp.com/options"
  -H "Authorization: turnsignal"
  -H "Content-Type: application/json"
  -X POST
  -d '{"option": {"name":"Tesla"}}'
```

> The above command returns JSON structured like this:

```json
{
  "id":101,
  "name":"Sun roof"
}
```

This endpoint creates a specific option. 

### Parameters

Parameter | Description
--------- | -----------
ID | The ID of the option to update

## Update a Option

```shell
curl "https://turn-signal.herokuapp.com/options/101"
  -H "Authorization: turnsignal"
  -H "Content-Type: application/json"
  -X PATCH
  -d '{"option": {"name":"All wheel DRIVE!!!"}}'
```

> The above command returns JSON structured like this:

```json
{
  "id":101,
  "name":"All wheel DRIVE!!!"
}
```

This endpoint updates a specific option.

### Parameters

Parameter | Description
--------- | -----------
ID | The ID of the option to update
name | The updated name of the option

## Delete a Option

```shell
curl "https://turn-signal.herokuapp.com/options/95"
  -X DELETE
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
{
  "id":69,
  "name":"Moon roof"
}
```

This endpoint deletes a specific option.

### HTTP Request

`DELETE https://turn-signal.herokuapp.com/options/95`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the option to delete

# Vehicles


## Vehicle object

This object defines a vehicle that a user owns. 

```json
  {
    "id": 1,
    "description": "Awesome",
    "year": 2009,
    "make": {
        "id": 13,
        "name": "Suzuki"
    },
    "model": {
        "id": 70,
        "name": "Grand Vitara"
    },
    "options": []
  }
```

### Object attributes

Attribute  | Description
---------  | -----------
id | The primary key of the object
description | The user's description of the vehicle
year | The year of manufacture for the user
make | The `make` of the vehicle
model | The `model` of the vehicle. The `model` must belong to the vehicle `make`. 

## Get All Vehicles

```shell
curl "https://turn-signal.herokuapp.com/vehicles"
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "description": "Awesome",
    "year": 2009,
    "make": {
        "id": 13,
        "name": "Suzuki"
    },
    "model": {
        "id": 70,
        "name": "Grand Vitara"
    },
    "options": []
  }
]
```

This endpoint retrieves vehicle vehicles (paginated 25 per page). It also returns the make of the vehicle as well as any `options` or `vehicles` for this vehicle.

### HTTP Request

`GET https://turn-signal.herokuapp.com/vehicles`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Get a specific page of results

## Get a Specific Vehicle

```shell
curl "https://turn-signal.herokuapp.com/vehicles/95"
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "description": "Awesome",
  "year": 2009,
  "make": {
    "id": 13,
    "name": "Suzuki"
  },
  "model": {
    "id": 70,
    "name": "Grand Vitara"
  },
  "options": []
}
```

This endpoint retrieves a specific vehicle.


### HTTP Request

`GET https://turn-signal.herokuapp.com/vehicles/<ID>`

### Parameters

Parameter | Description
--------- | -----------
ID | The ID of the vehicle to retrieve

## Create a Vehicle

```shell
curl "https://turn-signal.herokuapp.com/vehicles"
  -H "Authorization: turnsignal"
  -H "Content-Type: application/json"
  -X POST
  -d '{"vehicle": {"year": 2009, "description": "Awesome car", "make_id": 13, "model_id": 70}}'
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "description": "Awesome car",
  "year": 2009,
  "make": {
    "id": 13,
    "name": "Suzuki"
  },
  "model": {
    "id": 70,
    "name": "Grand Vitara"
  },
  "options": []
}
```

This endpoint creates a specific vehicle.

### Parameters

Parameter | Description
--------- | -----------
year | The year of manufature as an integer
description | A description of the vehicle
make_id | The primary key of the vehicle make
model_id | The primary key of the vehicle model. Note - this must be a valid model for the vehicle make. 
option_ids | An array of option IDs that this vehicle has

## Update a Vehicle

```shell
curl "https://turn-signal.herokuapp.com/vehicles/101"
  -H "Authorization: turnsignal"
  -H "Content-Type: application/json"
  -X PATCH
  -d '{"vehicle": {"name":"Roadster 2"}}'
```

> The above command returns JSON structured like this:

```json
{
  "id":150,
  "name":"Roadster 2",
  "make": {
    "id": 97,
    "name": "Tesla"
  }
}
```

This endpoint updates a specific vehicle. Note, duplicate vehicle `names` are not allowed.

### Parameters

Parameter | Description
--------- | -----------
year | The year of manufature as an integer
description | A description of the vehicle
make_id | The primary key of the vehicle make
model_id | The primary key of the vehicle model. Note - this must be a valid model for the vehicle make. 
option_ids | An array of option IDs that this vehicle has

## Delete a Vehicle

```shell
curl "https://turn-signal.herokuapp.com/vehicles/95"
  -X DELETE
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
{
  "id":150,
  "description":"Awesome car"
}
```

This endpoint deletes a specific vehicle.

### HTTP Request

`DELETE https://turn-signal.herokuapp.com/vehicles/95`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the vehicle to delete


# Vehicle Options

## Create a Vehicle Option

```shell
curl "https://turn-signal.herokuapp.com/vehicle_options"
  -H "Authorization: turnsignal"
  -H "Content-Type: application/json"
  -X POST
  -d '{"vehicle_option": {"vehicle_id":2, "option_id":4}}'
```

> The above command returns JSON structured like this:

```json
{
  "id":150,
  "vehicle": {
    "id": 2,
    "description": "An awesome car"
  },
  "option": {
    "id": 4,
    "name": "All wheel drive"
  }
}
```

This endpoint creates a specific vehicle_option. Use this if you want to add an existing option to an existing vehicle.

### Parameters

Parameter | Description
--------- | -----------
vehicle_id | The ID of the vehicle.
option_id | The ID of the option.

## Delete a Vehicle Option

```shell
curl "https://turn-signal.herokuapp.com/vehicle_options/95"
  -X DELETE
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
{
  "vehicle_id":2,
  "option_id":4
}
```

This endpoint deletes a specific vehicle_option.

### HTTP Request

`DELETE https://turn-signal.herokuapp.com/vehicle_options/95`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the vehicle option to delete


# Model Options

## Create a Model Option
 
```shell
curl "https://turn-signal.herokuapp.com/model_options"
  -H "Authorization: turnsignal"
  -H "Content-Type: application/json"
  -X POST
  -d '{"model_option": {"model_id":2, "option_id":4}}'
```

> The above command returns JSON structured like this:

```json
{
  "id":150,
  "model": {
    "id": 2,
    "name": "Roadster"
  },
  "option": {
    "id": 4,
    "name": "All wheel drive"
  }
}
```

This endpoint creates a specific model_option. Use this if you want to add an existing option to an existing model.

### Parameters

Parameter | Description
--------- | -----------
model_id | The ID of the model.
option_id | The ID of the option.

## Delete a Model Option

```shell
curl "https://turn-signal.herokuapp.com/model_options/95"
  -X DELETE
  -H "Authorization: turnsignal"
```

> The above command returns JSON structured like this:

```json
{
  "model_id": 2,
  "option_id": 4
}
```

This endpoint deletes a specific model_option.

### HTTP Request

`DELETE https://turn-signal.herokuapp.com/model_options/95`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the model option to delete
