## Location ID Search

Search for a Location ID by a string (ie, city and region)

<aside class="notice">
This endpoint always responds with JSON. There is no option for XML response using a `_type` parameter.
</aside>

<aside class="notice">
Please URL encode your `name` parameter string.
</aside>

```shell
curl "https://api.travsrv.com/widgetapi.aspx?\
type=cities\
&count=1\
&name=new+york"
```

> The above command returns JSON structured like this:

```json
[
    {
        "LocationId": 9044,
        "Name": "New York City, NY",
        "NumberOfHotels": 798
    }
]
```

### HTTP Request

`GET https://api.travsrv.com/widgetapi.aspx`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
type | string | Yes | Always "cities".
count | int | No | Maximum number of results to return. Defaults to 10.
name | string | Yes | City (URL encoded) name to search for.
