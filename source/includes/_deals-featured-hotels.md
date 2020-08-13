## Featured Hotels

All parameters other than `type` are optional and if not provided will be defaulted.

```shell
curl "https://api.travsrv.com/Content.aspx?\
type=findfeaturedhoteldeals\
&locationid=7151\
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
        "PropertyId": 182462,
        "DealsFound": 1111,
        "DealWeight": 51106,
        "MaxDiscountPercent": 72,
        "AvgDiscountPercent": 46,
        "ReferencePrice": 41.578,
        "ReferencePriceCurrency": "USD",
        "PropertyName": "Westgate Lakes Resort & Spa Universal Studios Area",
        "PropertyAddress": "9500 Turkey Lake Rd, Orlando, FL US",
        "LocationId": 7151,
        "PropertyLatitude": 28.42893,
        "PropertyLongitude": -81.47504,
        "PropertyImageUrl": "//media.travsrv.com/182462/124005548_804480.jpg",
        "PropertyImageUrlHighRes": "//media.travsrv.com/182462/124005548_0.jpg",
        "PropertyRating": "4 Stars",
        "TripAdvisorRating": 3.5,
        "TripAdvisorReviewCount": 6177,
        "RatingImageUrl": "//www.tripadvisor.com/img/cdsi/img2/ratings/traveler/3.5-39958-4.png",
        "CheckIn": "06/12/2019",
        "CheckOut": "06/15/2019"
    },
    {
        "PropertyId": 10507,
        "DealsFound": 990,
        "DealWeight": 39600,
        "MaxDiscountPercent": 55,
        "AvgDiscountPercent": 40,
        "ReferencePrice": 55.5,
        "ReferencePriceCurrency": "USD",
        "PropertyName": "Quality Suites",
        "PropertyAddress": "9350 Turkey Lake Rd, Orlando, FL US",
        "LocationId": 7151,
        "PropertyLatitude": 28.43031,
        "PropertyLongitude": -81.4751,
        "PropertyImageUrl": "//media.travsrv.com/10507/123830947_804480.jpg",
        "PropertyImageUrlHighRes": "//media.travsrv.com/10507/123830947_0.jpg",
        "PropertyRating": "2 Stars",
        "TripAdvisorRating": 3,
        "TripAdvisorReviewCount": 674,
        "RatingImageUrl": "//www.tripadvisor.com/img/cdsi/img2/ratings/traveler/3.0-39958-4.png",
        "CheckIn": "06/12/2019",
        "CheckOut": "06/15/2019"
    }
]
```

### HTTP Request

`GET https://api.travsrv.com/Content.aspx`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
type | string | Yes | Always "findfeaturedhoteldeals"
locationid | int | No | Found via [locationid search](#location-id-search)
mindiscount | int | No | Return only results >= this value
maxdiscount | int | No | Return only results <= this value
checkIn | date | No | Desired check-in date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
checkOut | date | No | Desired check-in date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
maxresults | int | No | Maximum number of results to return
_type | string/enum | No | The response format. One of `xml` or `json`. Default: `json`.
