## Featured Locations

All parameters other than `type` are optional and if not provided will be defaulted.

```shell
curl "https://api.travsrv.com/Content.aspx?\
type=findfeaturedlocationdeals\
&mindiscount=10\
&maxdiscount=100\
&checkIn=2020-03-01\
&checkOut=2020-03-03\
&maxresults=2\
&_type=json"
```

> The above command returns JSON structured like this:

```json
[
    {
        "AvgDiscountPercent": 54,
        "AvgNightlyPrice": 406.73,
        "AvgNightlyPriceCurrency": "USD",
        "DealProperties": 9,
        "DealsFound": 151,
        "DealWeight": 8154,
        "LocationCountry": "US",
        "LocationId": 3626,
        "LocationImageUrl": "//media.travsrv.com/1146021/232355706_804480.jpg",
        "LocationImageUrlHighRes": "//media.travsrv.com/1146021/232355706_0.jpg",
        "LocationLatitude": 34.09,
        "LocationLongitude": -118.360833,
        "LocationName": "West Hollywood, CA",
        "MaxDiscountPercent": 75
    },
    {
        "AvgDiscountPercent": 49,
        "AvgNightlyPrice": 100.5,
        "AvgNightlyPriceCurrency": "USD",
        "DealProperties": 10,
        "DealsFound": 147,
        "DealWeight": 7203,
        "LocationCountry": "US",
        "LocationId": 10124,
        "LocationImageUrl": "//media.travsrv.com/12575/123690570_804480.jpg",
        "LocationImageUrlHighRes": "//media.travsrv.com/12575/123690570_0.jpg",
        "LocationLatitude": 33.679444,
        "LocationLongitude": -84.439444,
        "LocationName": "East Point, GA",
        "MaxDiscountPercent": 66
    }
]
```

### HTTP Request

`GET https://api.travsrv.com/Content.aspx`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
type | string | Yes | Always "findfeaturedlocationdeals"
mindiscount | int | No | Return only results >= this value
maxdiscount | int | No | Return only results <= this value
checkIn | date | No | Desired check-in date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
checkOut | date | No | Desired check-in date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
maxresults | int | No | Maximum number of results to return
_type | string/enum | No | The response format. One of `xml` or `json`. Default: `json`.
