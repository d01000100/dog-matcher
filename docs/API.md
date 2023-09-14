# Fetch API

## Login 

- It's a POST with the name and email as JSON in the body
- The response will have in its cookies an fetch-access-token.

  You don't need to store this key anywhere. The browser/server will store it and will add it to subsecuent calls if you set:
  - credentials: 'include'
  - withCredentials: true
  In the header of the following calls

## GET dogs/breeds

```json
[
    "Affenpinscher",
    "Afghan Hound",
    "African Hunting Dog",
    "Airedale",
    "American Staffordshire Terrier",
    "Appenzeller",
    "Australian Terrier",
    "Basenji",
    "Basset",
    "Beagle",
    ...
]
```

## GET dogs/search

**Without params**

```json
{
    "next": "/dogs/search?size=25&from=25",
    "resultIds": [
        "VXGFTIcBOvEgQ5OCx40W",
        "V3GFTIcBOvEgQ5OCx40W",
        "WHGFTIcBOvEgQ5OCx40W",
        "W3GFTIcBOvEgQ5OCx40W",
        "YnGFTIcBOvEgQ5OCx40W",
        "Y3GFTIcBOvEgQ5OCx40W",
        ...
    ],
    "total": 10000
}
```

**With breeds as array**

You add multiple `breeds` params with different breed names

```js
let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://frontend-take-home-service.fetch.com/dogs/search?ageMin=10&breeds=Airedale&breeds=Beagle',
};
```

**With pagination**

- `size`
- `from`

```json
{
    "next": "/dogs/search?ageMin=10&breeds%5B0%5D=Airedale&breeds%5B1%5D=Beagle&size=30&from=110",
    "prev": "/dogs/search?ageMin=10&breeds%5B0%5D=Airedale&breeds%5B1%5D=Beagle&size=30&from=50",
    "resultIds": [
        "U3GFTIcBOvEgQ5OCx6Qn",
        "XnGFTIcBOvEgQ5OCx6Qn",
        "YXGFTIcBOvEgQ5OCx6Qn",
        "h3GFTIcBOvEgQ5OCx6Qn",
        ...
    ],
    "total": 140
}
```

- `sort` = `field:asc` | `field:desc`

```json
{
    "next": "/dogs/search?ageMin=10&breeds%5B0%5D=Airedale&breeds%5B1%5D=Beagle&size=30&from=110&sort=breed%3Aasc",
    "prev": "/dogs/search?ageMin=10&breeds%5B0%5D=Airedale&breeds%5B1%5D=Beagle&size=30&from=50&sort=breed%3Aasc",
    "resultIds": [
        "ZXGFTIcBOvEgQ5OCx6Qn",
        "bHGFTIcBOvEgQ5OCx6Qn",
        "bnGFTIcBOvEgQ5OCx6Qn",
        "f3GFTIcBOvEgQ5OCx6Qn",
    ],
    "total": 140
}
```

## POST /dogs

Get the information of dogs

```js
const axios = require('axios');
let data = JSON.stringify([
  "ZXGFTIcBOvEgQ5OCx6Qn",
  "bHGFTIcBOvEgQ5OCx6Qn",
  "bnGFTIcBOvEgQ5OCx6Qn",
  "Y3GFTIcBOvEgQ5OCx40W"
]);

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://frontend-take-home-service.fetch.com/dogs',
  headers: { 
    'Content-Type': 'application/json',
  data : data
};
```

The body is a JSON array with the ids of dogs

```json
[
    {
        "img": "https://frontend-take-home.fetch.com/dog-images/n02088364-beagle/n02088364_16065.jpg",
        "name": "Werner",
        "age": 13,
        "breed": "Beagle",
        "zip_code": "13202",
        "id": "ZXGFTIcBOvEgQ5OCx6Qn"
    },
    {
        "img": "https://frontend-take-home.fetch.com/dog-images/n02088364-beagle/n02088364_16502.jpg",
        "name": "Judd",
        "age": 14,
        "breed": "Beagle",
        "zip_code": "52054",
        "id": "bHGFTIcBOvEgQ5OCx6Qn"
    },
    {
        "img": "https://frontend-take-home.fetch.com/dog-images/n02088364-beagle/n02088364_16519.jpg",
        "name": "Tiara",
        "age": 14,
        "breed": "Beagle",
        "zip_code": "16635",
        "id": "bnGFTIcBOvEgQ5OCx6Qn"
    },
    {
        "img": "https://frontend-take-home.fetch.com/dog-images/n02085620-Chihuahua/n02085620_1271.jpg",
        "name": "Seamus",
        "age": 2,
        "breed": "Chihuahua",
        "zip_code": "09189",
        "id": "Y3GFTIcBOvEgQ5OCx40W"
    }
]
```

## POST dogs/match

Select (¿randomly?) a dog from the provided list

```js
const axios = require('axios');
let data = JSON.stringify([
  "ZXGFTIcBOvEgQ5OCx6Qn",
  "bHGFTIcBOvEgQ5OCx6Qn",
  "bnGFTIcBOvEgQ5OCx6Qn",
  "Y3GFTIcBOvEgQ5OCx40W"
]);

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://frontend-take-home-service.fetch.com/dogs/match',
  data : data
};
```

```json
{
    "match": "Y3GFTIcBOvEgQ5OCx40W"
}
```

## POST Location

Get the location info from its zip code

```js
const axios = require('axios');
let data = JSON.stringify([
  "13202",
  "52054"
]);

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://frontend-take-home-service.fetch.com/locations',
  headers: { 
    'Content-Type': 'application/json', 
  },
  data : data
};
```

```json
[
    {
        "city": "Syracuse",
        "latitude": 43.043116,
        "county": "Onondaga",
        "state": "NY",
        "zip_code": "13202",
        "longitude": -76.150796
    },
    {
        "city": "La Motte",
        "latitude": 42.284057,
        "county": "Jackson",
        "state": "IA",
        "zip_code": "52054",
        "longitude": -90.595351
    }
]
```

## POST /locations/search

Search locations by city, states, and coordinates bounding box

```js
const axios = require('axios');
let data = JSON.stringify({
  "city": "New",
  "states": [
    "NY",
    "NJ"
  ],
  "size": 3,
  "from": 20
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://frontend-take-home-service.fetch.com/locations/search',
  data : data
};
```

```json
{
    "results": [
        {
            "city": "New York",
            "latitude": 40.708834,
            "county": "New York",
            "state": "NY",
            "zip_code": "10006",
            "longitude": -74.013168
        },
        {
            "city": "New York",
            "latitude": 40.713941,
            "county": "New York",
            "state": "NY",
            "zip_code": "10007",
            "longitude": -74.007401
        },
        {
            "city": "New York",
            "latitude": 40.780751,
            "county": "New York",
            "state": "NY",
            "zip_code": "10008",
            "longitude": -73.977182
        }
    ],
    "total": 204
}```