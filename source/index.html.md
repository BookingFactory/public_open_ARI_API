---
title: Public Open ARI API Reference

language_tabs:
  - javascript

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction

Welcome to the Booking Factory Public Open ARI API! You can use our API to write your own booking widgets.

Our API based at simple HTTP requests, as result you can use any language! You can view code examples in the dark area to the right, we provide examples at JavaScript, but you can use CURL or other libraries.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# API Endpoint
```javascript
const API_ENDPOINT = 'https://app.thebookingfactory.com/api/public/ari/v1/';
```

Our API endpoint located at https://app.thebookingfactory.com/api/public/ari/v1/

# Authentication
```javascript
const API_KEY = 'meowmeowmeow';
```

> Make sure to replace `meowmeowmeow` with your API key.

Our engine uses API keys to allow access to the API. You can register a new API key at your [hotel settings page](https://app.thebookingfactory.com/client/#/settings/other/api_key).

We expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Token: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Methods


## Get Availability

```javascript
fetch(
    API_ENDPOINT + 'availability?date_from=2017-01-01&date_to=2017-01-02&fields=',
    {
      method:  'GET',
      headers: { 'Token': API_KEY }
    }
  )
  .then(function(raw_response) {
    return raw_response.json();
  })
  .then(function(response) {
    console.log(response);
  })
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "data": {
    "date_from": "2017-01-01",
    "date_to": "2017-01-02",
    "availability": {
      "STDB": {
        "2017-01-01": {
          "min_stay": 1,
          "available": 0,
          "closed_arrival": 0,
          "closed_departure": 0
        },
        "2017-01-02": {
          "min_stay": 1,
          "available": 1,
          "closed_arrival": 0,
          "closed_departure": 0
        }
      },
      "EXDB": {
        "2017-01-01": {
          "min_stay": 1,
          "available": 2,
          "closed_arrival": 0,
          "closed_departure": 0
        },
        "2017-01-02": {
          "min_stay": 1,
          "available": 8,
          "closed_arrival": 0,
          "closed_departure": 0
        }
      },
      "ext1": {
        "2017-01-01": {
          "min_stay": 1,
          "available": 0,
          "closed_arrival": 0,
          "closed_departure": 0
        },
        "2017-01-02": {
          "min_stay": 1,
          "available": 1,
          "closed_arrival": 0,
          "closed_departure": 0
        }
      },
      "ETTW": {
        "2017-01-01": {
          "min_stay": 1,
          "available": 1,
          "closed_arrival": 0,
          "closed_departure": 0
        },
        "2017-01-02": {
          "min_stay": 1,
          "available": 2,
          "closed_arrival": 0,
          "closed_departure": 0
        }
      },
      "CSDB": {
        "2017-01-01": {
          "min_stay": 1,
          "available": 1,
          "closed_arrival": 0,
          "closed_departure": 0
        },
        "2017-01-02": {
          "min_stay": 1,
          "available": 0,
          "closed_arrival": 0,
          "closed_departure": 0
        }
      },
      "SERV": {
        "2017-01-01": {
          "min_stay": 2,
          "available": 0,
          "closed_arrival": 0,
          "closed_departure": 0
        },
        "2017-01-02": {
          "min_stay": 2,
          "available": 0,
          "closed_arrival": 0,
          "closed_departure": 0
        }
      }
    }
  }
}

{
  "status": false,
  "data": {},
  "errors": [
    "date_to is invalid date"
  ]
}

{
  "status": false,
  "data": {},
  "errors": [
    "date_to is not defined, but required"
  ]
}
```

This endpoint retrieves list of all availability rooms.
date_from, date_to is required fields.

### HTTP Request

`GET https://app.thebookingfactory.com/api/public/ari/v1/availability`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
date_from | true | Date from, should be a valid date in ISO 8601 YYYY-MM-DD format
date_to | true | Date to, should be a valid date in ISO 8601 YYYY-MM-DD format
fields | false | comma separated list of required fields (default is: available, min_stay, closed_arrival, closed_departure)

### Response
Parameter | Description
--------- | -----------
success | Show current request status, if all is ok then TRUE, if request has any errors then FALSE
errors | Array of error descriptions. Displayed only if success == false
data | Array of availability for Room Type

#### Data object description
Parameter | Description
--------- | -----------
date_from | Date from
date_to | Date to
availability | Array of Room Type

#### Availability object description
Parameter | Description
--------- | -----------
min_stay | Min stay
available | Availability
closed_arrival | Closed Arrival
closed_departure | Closed departure


## Get Rates

```javascript
fetch(
    API_ENDPOINT + 'rates?date_from=2017-03-01&date_to=2017-03-02',
    {
      method:  'GET',
      headers: { 'Token': API_KEY }
    }
  )
  .then(function(raw_response) {
    return raw_response.json();
  })
  .then(function(response) {
    console.log(response);
  })
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "data": {
    "date_from": "2017-03-01",
    "date_to": "2017-03-02",
    "rates": {
      "40": {
        "2017-03-01": "55.0",
        "2017-03-02": "55.0"
      },
      "A": {
        "2017-03-01": "65.0",
        "2017-03-02": "65.0"
      },
      "STDB": {
        "2017-03-01": "76.0",
        "2017-03-02": "76.0"
      },
      "EXDB": {
        "2017-03-01": "86.0",
        "2017-03-02": "86.0"
      },
      "B": {
        "2017-03-01": "75.0",
        "2017-03-02": "75.0"
      },
      "ext1": {
        "2017-03-01": "65.0",
        "2017-03-02": "65.0"
      },
      "S2FU": {
        "2017-03-01": "90.0",
        "2017-03-02": "90.0"
      },
      "D": {
        "2017-03-01": "75.0",
        "2017-03-02": "75.0"
      },
      "ETTW": {
        "2017-03-01": "90.0",
        "2017-03-02": "90.0"
      },
      "CSDB": {
        "2017-03-01": "55.0",
        "2017-03-02": "55.0"
      },
      "SERV": {
        "2017-03-01": "100.0",
        "2017-03-02": "100.0"
      }
    }
  }
}
```

This endpoint retrieves list of all rates.
date_from, date_to is required fields.

### HTTP Request

`GET https://app.thebookingfactory.com/api/public/ari/v1/rates`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
date_from | true | Date from, should be a valid date in ISO 8601 YYYY-MM-DD format
date_to | true | Date to, should be a valid date in ISO 8601 YYYY-MM-DD format
rooms | false | comma separated list of short_codes for required rooms
rate_categories | false | comma separated list of short_codes for required rate_categories
rates | false | comma separated list of short_codes for required rates

### Response
Parameter | Description
--------- | -----------
status | Show current request status, if all is ok then TRUE, if request has any errors then FALSE
data | Array of rates

#### Data object description
Parameter | Description
--------- | -----------
rates | Array of real rates on the selected date


## Get Inventory Rates

```javascript
fetch(
    API_ENDPOINT + 'inventory/rates',
    {
      method:  'GET',
      headers: { 'Token': API_KEY }
    }
  )
  .then(function(raw_response) {
    return raw_response.json();
  })
  .then(function(response) {
    console.log(response);
  })
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "data": {
    "rates": [
      {
        "short_code": "A",
        "room_code": "STDB",
        "name": "Standard Double Room (Single Occupancy)",
        "rate_category_code": "5"
      },
      {
        "short_code": "STDB",
        "room_code": "STDB",
        "name": "Standard Double Room",
        "rate_category_code": "4"
      },
      {
        "short_code": "EXDB",
        "room_code": "EXDB",
        "name": "Executive Double Room",
        "rate_category_code": "4"
      },
      {
        "short_code": "B",
        "room_code": "EXDB",
        "name": "Executive Double Room (Single Occupancy)",
        "rate_category_code": "5"
      },
      {
        "short_code": "ext1",
        "room_code": "ext1",
        "name": "External Double",
        "rate_category_code": "4"
      },
      {
        "short_code": "40",
        "room_code": "ext1",
        "name": "External Double (Single Occupancy)",
        "rate_category_code": "5"
      },
      {
        "short_code": "S2FU",
        "room_code": "S2FU",
        "name": "Executive Twin/Double",
        "rate_category_code": "4"
      },
      {
        "short_code": "D",
        "room_code": "ETTW",
        "name": "Executive Twin/Double (Single Occupancy)",
        "rate_category_code": "5"
      },
      {
        "short_code": "ETTW",
        "room_code": "ETTW",
        "name": "Executive Twin/Double",
        "rate_category_code": "4"
      },
      {
        "short_code": "CSDB",
        "room_code": "CSDB",
        "name": "Cosy Double For One",
        "rate_category_code": "4"
      },
      {
        "short_code": "SERV",
        "room_code": "SERV",
        "name": "Serviced Apartment",
        "rate_category_code": "4"
      }
    ],
    "rate_categories": [
      {
        "short_code": "4",
        "title": "Breakfast Rate",
        "max_occupancy": null,
        "cancellation_policy": "No deposit is required. Remaining balance to be paid on Arrival. We have the right to pre-authorise your card prior to arrival. Free cancellation up 24 Hours before arrival. In case of no-show or late cancellation the first night will be charged.",
        "mandatory_extras": [
          {
            "title": "Breakfast Included",
            "price": "0.0",
            "sell_mode": "per_person_per_night"
          }
        ]
      },
      {
        "short_code": "5",
        "title": "Single Occupancy",
        "max_occupancy": null,
        "cancellation_policy": "No deposit is required. Remaining balance to be paid on Arrival. We have the right to pre-authorise your card prior to arrival. Free cancellation up 24 Hours before arrival. In case of no-show or late cancellation the first night will be charged.",
        "mandatory_extras": []
      }
    ]
  }
}

{
  "status": false,
  "data": {},
  "errors": [
    "Authorization Token is invalid"
  ]
}
```

This endpoint retrieves list of all invenory rates.

### HTTP Request

`GET https://app.thebookingfactory.com/api/public/ari/v1/inventory/rates`

### Response
Parameter | Description
--------- | -----------
status | Show current request status, if all is ok then TRUE, if request has any errors then FALSE
data | Array of rates

#### Rates object description
Parameter | Description
--------- | -----------
short_code | Unique code for rate
room_code | Unique room code
name | Name of rate
rate_category_code | Unique code for category rate

#### Rate Categories object description
Parameter | Description
--------- | -----------
short_code | Unique code for category rate
title | Name of category rate
max_occupancy | Max occupancy
cancellation_policy | Cancellation policy
mandatory_extras | Array of mandatory extras


## Get Inventory Rooms

```javascript
fetch(
    API_ENDPOINT + 'inventory/rooms',
    {
      method:  'GET',
      headers: { 'Token': API_KEY }
    }
  )
  .then(function(raw_response) {
    return raw_response.json();
  })
  .then(function(response) {
    console.log(response);
  })
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "data": {
    "rooms": [
      {
        "short_code": "STDB",
        "name": "Standard Double Room",
        "occupancy": 2,
        "adult": 2,
        "children": 0,
        "default_availability": 4,
        "online_availability": 4,
        "photos": [
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/033/original/IMG_8219.JPG?1476783545",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/039/original/IMG_8235.JPG?1476783586",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/047/original/IMG_8233.JPG?1476783632"
        ]
      },
      {
        "short_code": "EXDB",
        "name": "Executive Double Room",
        "occupancy": 2,
        "adult": 2,
        "children": 0,
        "default_availability": 9,
        "online_availability": 9,
        "photos": [
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/034/original/IMG_8220.JPG?1476783555",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/035/original/IMG_8221.JPG?1476783561",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/036/original/IMG_8222.JPG?1476783567",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/037/original/IMG_8223.JPG?1476783573",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/045/original/IMG_8261.JPG?1476783627"
        ]
      },
      {
        "short_code": "ext1",
        "name": "External Double",
        "occupancy": 2,
        "adult": 2,
        "children": 0,
        "default_availability": 1,
        "online_availability": 1,
        "photos": [
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/103/original/IMG_0049.JPG?1476784388",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/104/original/IMG_0047.JPG?1476784409"
        ]
      },
      {
        "short_code": "ETTW",
        "name": "Executive Twin/Double",
        "occupancy": 2,
        "adult": 2,
        "children": 0,
        "default_availability": 2,
        "online_availability": 2,
        "photos": [
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/042/original/IMG_8242.JPG?1476783606",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/043/original/IMG_8243.JPG?1476783613",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/044/original/IMG_8241.JPG?1476783621"
        ]
      },
      {
        "short_code": "CSDB",
        "name": "Cosy Double For One",
        "occupancy": 1,
        "adult": 1,
        "children": 0,
        "default_availability": 1,
        "online_availability": 1,
        "photos": [
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/038/original/IMG_8228.JPG?1476783579",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/040/original/IMG_8229.JPG?1476783591",
          "https://s3.amazonaws.com/buuqit-dev/photos/photos/000/000/041/original/IMG_8227.JPG?1476783599"
        ]
      },
      {
        "short_code": "SERV",
        "name": "Serviced Apartment",
        "occupancy": 2,
        "adult": 2,
        "children": 0,
        "default_availability": 1,
        "online_availability": 0,
        "photos": []
      }
    ],
    "virtual_rooms": [
      {
        "short_code": "S2FU",
        "name": "Family Room",
        "occupancy": 3,
        "adult": 2,
        "children": 1,
        "default_availability": 2,
        "online_availability": 2,
        "original_room": "ETTW",
        "photos": []
      }
    ]
  }
}

{
  "status": false,
  "data": {},
  "errors": [
    "Authorization Token is invalid"
  ]
}
```

This endpoint retrieves list of all Inventory rooms.

### HTTP Request

`GET https://app.thebookingfactory.com/api/public/ari/v1/inventory/rooms`

### Response
Parameter | Description
--------- | -----------
success | Show current request status, if all is ok then TRUE, if request has any errors then FALSE
errors | Array of error descriptions. Displayed only if success == false
data | Array of inventory rooms

#### Data object description
Parameter | Description
--------- | -----------
rooms | Array of real inventory
virtual_rooms | Array of virtual rooms mapped to real inventory. This rooms use availability settings from parent real room.

#### Rooms object description
Parameter | Description
--------- | -----------
short_code | Unique code at system
name | Room name
occupancy | Max available occupancy
adults | Max available adults occupancy
children | Max available children occupancy
default_availability | Count of numbers associated with selected room
online_availability | Count of numbers associated with selected room to sell online
photos | Array of images inventory rooms

#### Virtual Rooms object description
Parameter | Description
--------- | -----------
short_code | Unique code at system
name | Room name
occupancy | Max available occupancy
adults | Max available adults occupancy
children | Max available children occupancy
default_availability | Count of numbers associated with selected room
online_availability | Count of numbers associated with selected room to sell online
original_room | Parent room short_code for virtual room
photos | Array of images inventory rooms