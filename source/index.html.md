---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://www.emmi.io'>About Emmi</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Emmi API
---


# Authentication

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: Bearer myapikey"
```


> Make sure to replace `myapikey` with your API key.

Emmi uses API keys to allow access to the API. You can register a new Emmi API key by contacting [ernest.lie@emmi.io](ernest.lie@emmi.io)

Emmi expects for the API key to be included in all API requests using Bearer Authentication to the server in a header that looks like the following:

`Authorization: Bearer myapikey`

<aside class="notice">
You must replace <code>myapikey</code> with your personal API key.
</aside>

# Funds

## Get All Funds


```shell
curl "https://api.emmi.io/api/public/funds" \
  -H "Authorization: Bearer myapikey"
```


> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "ABC",
    "creator": "Kenny",
    "updated_at": "2022-03-01T00:00:00.000Z"
  },
  {
    "id": 2,
    "name": "DEF",
    "creator": "Belle",
    "updated_at": "2022-01-01T00:00:00.000Z"
  },
]
```

This endpoint retrieves all funds.

### HTTP Request

`GET https://api.emmi.io/api/public/funds`

## Get a specific Fund


```shell
curl "https://api.emmi.io/api/public/funds/2" \
  -H "Authorization: Bearer myapikey"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "DEF",
  "creator": "Belle",
  "updated_at": "2022-01-01T00:00:00.000Z"
}
```

This endpoint retrieves a specific fund.

### HTTP Request

`GET https://api.emmi.io/api/public/funds/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the fund to retrieve

## Get metrics of a specific Fund


```shell
curl "https://api.emmi.io/api/public/funds/1/metrics" \
  -H "Authorization: Bearer myapikey"
```

> The above command returns JSON structured like this:

```json
{
  "fund_id": 1,
  "name": "Kenny",
  "emissions": {
    "scope1": 2000.0,
    "scope2": 8000.0,
    "scope3": 5000000.0
  },
  "emmi_score": 93.0,
  "temperature_alignment": 1.5,
  "carbon_intensity": 105
}
```

This endpoint retrieves the metrics of a specific fund.

### HTTP Request

`GET https://api.emmi.io/api/public/funds/<ID>/metrics`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the fund to retrieve
Year | The year of the metrics to retrieve

## Get holdings of a specific Fund


```shell
curl "https://api.emmi.io/api/public/funds/2" \
  -H "Authorization: Bearer myapikey"
```

> The above command returns JSON structured like this:

```json
[
  {
    "company_id": 1,
    "isin": "US02079K3059",
    "company": "Alphabet Inc. Class A",
    "weighting": "50.0",
    "emmi_score": "99.5",
    "temperature_alignment": "1.5"
  },
  {
    "company_id": 2,
    "isin": "NZATME0002S8",
    "company": "a2 Milk Company Ltd.",
    "weighting": "50.0",
    "emmi_score": "84.35",
    "temperature_alignment": "1.71"
  }
]
```

This endpoint retrieves the holdings of a specific fund.

### HTTP Request

`GET https://api.emmi.io/api/public/funds/<ID>/holdings`

### URL parameters

Parameter | Description
--------- | -----------
Name | The name of the fund to create
Year | The year of the fund to create


## Create a Specific Fund


```shell
curl "https://api.emmi.io/api/public/funds" \
  -X POST \
  -H "Authorization: Bearer myapikey" \
  -H 'Content-Type: application/json' \
  -d '{"name":"XYZ","year":2020, "companies": [{"isin":"US02079K3059","weighting":0.5},{"isin":"NZATME0002S8","weighting":0.5}]}'
```

> The above command returns JSON structured like this:

```json
{
    "id": 3,
    "name": "XYZ",
    "creator": "Kenny",
    "updated_at": "2022-12-01T00:00:00.000Z"
}
```

This endpoint create a fund.

### HTTP Request

`POST https://api.emmi.io/api/public/funds`

### Data Payload Parameters

Parameter | Description
--------- | -----------
Name | The name of the fund to create
Year | The year of the fund to create
Companies | The companies for a fund. Companies must be an array of objects containing an `isin` and  a `weighting`.


<aside class="notice">
Note that if an ISIN cannot be found in our system, we will return a 422 Error with a list of any unmatched ISINs
</aside>

## Delete a Specific Fund


```shell
curl "https://api.emmi.io/api/public/funds/2" \
  -X DELETE \
  -H "Authorization: Bearer myapikey"
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint deletes a specific fund.

### HTTP Request

`DELETE https://api.emmi.io/api/public/funds/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the fund to delete

