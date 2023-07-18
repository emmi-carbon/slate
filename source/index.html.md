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
  "carbon_intensity": 105,
  "2022_temp_alignment": "3.58",
  "2030_temp_alignment": "2.12",
  "2050_temp_alignment": "1.58",
  "2022_capital_loss_mid": "12.82",
  "2022_capital_loss_high": "54.37",
  "2030_capital_loss_mid": "18.68",
  "2030_capital_loss_high": "63.59",
  "2050_capital_loss_mid": "53.59",
  "2050_capital_loss_high": "88.06"
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
curl "https://api.emmi.io/api/public/funds/2/holdings" \
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
    "2022_temp_alignment": "4.0",
    "2022_capital_loss_mid": "3.45",
    "2022_capital_loss_high": "28.1",
    "2030_temp_alignment": "4.0",
    "2030_capital_loss_mid": "5.67",
    "2030_capital_loss_high": "61.4",
    "2050_temp_alignment": "4.0",
    "2050_capital_loss_mid": "27.02",
    "2050_capital_loss_high": "99.99"
  },
  {
    "company_id": 2,
    "isin": "NZATME0002S8",
    "company": "a2 Milk Company Ltd.",
    "weighting": "50.0",
    "2022_temp_alignment": "4.0",
    "2022_capital_loss_mid": "0.42",
    "2022_capital_loss_high": "4.63",
    "2030_temp_alignment": "4.0",
    "2030_capital_loss_mid": "0.68",
    "2030_capital_loss_high": "13.03",
    "2050_temp_alignment": "4.0",
    "2050_capital_loss_mid": "4.3",
    "2050_capital_loss_high": "87.19"
  }
]
```

This endpoint retrieves the holdings of a specific fund.

### HTTP Request

`GET https://api.emmi.io/api/public/funds/<ID>/holdings`

### URL parameters

Parameter | Description
--------- | -----------
ID | The name of the fund
Year | The year of the holdings to retrieve


## Create a Specific Fund


```shell
curl "https://api.emmi.io/api/public/funds" \
  -X POST \
  -H "Authorization: Bearer myapikey" \
  -H 'Content-Type: application/json' \
  -d '{"name":"XYZ","year":2020, "aum: 200000000", companies": [{"isin":"US02079K3059","weighting":0.5},{"isin":"NZATME0002S8","weighting":0.5}]}'
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
AUM | Fund AUM amount. Optional parameter defaulted to $100,000,000
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

