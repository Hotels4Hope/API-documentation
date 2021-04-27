## Availability Search

This endpoint retrieves all hotels which have availability for the dates and locations (or individual hotels) specified.

Make this request for the total number of rooms and the total number of guests.  The response will return a maximum of 50 hotels per request, thus you must use pagination techniques if you need more than 50. That said, 50 is the maximum but may not be the best performing. Use smaller batches to get faster responses.

Responses will contain available rate plans and room types from various suppliers we call "gateways".

Responses may contain full nightly rates and tax information, only first night rates with or without tax information, or the highest or average nightly rate.  This response depends on the supplier/gateway but the most common from most gateways is the first night's rate, thus the property name in our responses (`FirstNightRate`).

Rates are always returned in the hotel's native currency.  If you request another `currency`, the correct conversion rate from the hotel's native currency to the desired `DisplayCurrency` will be returned as `DisplayCurrencyMultiplier`. You may use this value to convert the hotel currency to the desired currency for display in your UI. This allows you to show both the original currency and display currency side by side.

<aside class="notice">
We do not advise programming in a gateway-specific manner. Gateways may respond with varying amounts of information at any time. Also, new gateways could be added at any time.
</aside>

<aside class="notice">
If an availability search fails to return rates, we suggest not showing the hotel in your user interface.
</aside>

<aside class="notice">
For the `children` parameter, we always suggest sending in a value of "0". Many older GDS do not accept this parameter at all, and including it may return inconsistent pricing because of this.
</aside>

<aside class="notice">
  If returned, the `NightlyRate` discount is pre-tax discount from the pre-tax price. The `Total.Discount` is a post-tax discount from post-tax total.
</aside>

```shell
curl "https://api.travsrv.com/hotel.aspx?\
&siteid={SITEID}\
&latitude=30.099016\
&longitude=-81.601370\
&radius=10\
&inDate=2018-10-20\
&outDate=2018-10-22\
&maxResults=1\
&rooms=1\
&adults=2\
&children=0\
&ipAddress=127.0.0.1\
&userAgent=shell\
&userLanguage=en\
&_type=json" \
  -H 'Authorization: Basic {BASE64-ENCODED-STRING}'
```

> The above command returns JSON structured like this (edited for brevity):

```json
{
  "ArnResponse": {
    "Info": {
      "@SiteID": "{SITEID}",
      "@Username": "{API-USERNAME}",
      "@IpAddress": "127.0.0.1",
      "@TimeReceived": "2018-04-13T16:01:13.510",
      "@TimeCompleted": "2018-04-13T16:01:13.651",
      "@Version": "1.0.0.0",
      "@ServiceUrl": "https://api.travsrv.com/hotel.aspx?inDate=2018-10-20&latitude=30.099016&longitude=-81.601370&maxResults=1&outDate=2018-10-22&radius=10&siteid={SITEID}",
      "@RequestID": "436E177E-558F-4287-B55A-5DBD9F4C7579"
    },
    "Availability": {
      "@DisplayCurrency": "USD",
      "HotelAvailability": {
        "@InDate": "2018-10-20",
        "@OutDate": "2018-10-22",
        "@Rooms": "1",
        "@Adults": "2",
        "@Children": "0",
        "Hotel": {
          "@HotelID": "272393",
          "@IsEphemeral": "true",
          "RatePlan": [
            {
              "@Code": "F89648494F22FFE25A254AD1CE7D18FD27B862F1A609BD28872D9CD6DDA2E956B160BE3DB7EB0191B160BE3DB7EB01917EA3048807BEE935",
              "@Description": "Best Available",
              "@BuyerOnly": "false",
              "@Gateway": "41",
              "@CommissionStatus": "Commissionable",
              "@BalanceDueAtHotel": "false",
              "Room": {
                "@Code": "HRLM--_eJwFwcuaczAAANAHmgVRCRaziPRvxkyJadx3biWUfkFH9On_fc5BTlaYBzSSx4m6Iwz3cS_pRnKxCtkQzjqPQZm8Lh771NInUK3ri_pDYTzZL6lQtgl0H0_fOj_f5dRd1kT_pX8dtg_pq0LMTJYHFXNuPqi0PxdLuTjEAeTtKNfYZ3Gd3suIjMbm3_prdXk03gvS_pfpUJnL_poCL9kNoyIlpA2DURM1_fqAtELSKYuKh6e248vaSGk9hE9Dns4MYIncb5jC_fcZG_p_fOeSN3Z0N_fib2UqSpSLCPFgqPX2sQTP9rmXEv_ptXOMVOlVLoC_fujzlUz6tJvvFwUEonyP6njavHdzsVVF2EesNGSmILz3twKMBKm_fp7PK2XCcgV8ghjMc93ZaXrLkm622zmAYaTaPSItlgfYOcO2TSZ6hvwXlxw_fSAVdl9fv4Hwe6AJQ",
                "@Name": "Standard room",
                "@Description": "- 1 King Bed - Nonsmoking Room - Free Breakfast, Free Wifi, Fridge, Microwave",
                "@CurrencyCode": "USD",
                "@DisplayCurrencyMultiplier": "1",
                "@USDMultiplier": "1",
                "@ExchangeGMT": "2018-04-13T11:00:26.790",
                "@MaximumBookable": "99",
                "NightlyRate": [
                  {
                    "@Date": "2018-10-20",
                    "@Price": "114.44"
                  },
                  {
                    "@Date": "2018-10-21",
                    "@Price": "114.43"
                  }
                ],
                "Tax": {
                  "@Percent": "11.51",
                  "@Amount": "29.77"
                },
                "GatewayFee": {
                  "@Amount": "0.00"
                },
                "Total": {
                  "@Amount": "258.64",
                  "@IncludesBookingFee": "false"
                },
                "BookingFee": {
                  "@Amount": "0.00",
                  "@CurrencyCode": "USD",
                  "@DisplayCurrencyMultiplier": "1",
                  "@RoomCurrencyMultiplier": "1",
                  "@ExchangeGMT": "2018-04-13T11:00:26.790"
                }
              }
            }
          ]
        }
      }
    }
  }
}
```

### HTTP Request

`GET https://api.travsrv.com/hotel.aspx`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
siteid | integer | Yes | Provided by QuintRooms
timeout | int | No | Maximum time to allow for searching gateways, measured in seconds. Default: 15
maxResults | int | No | Number of results to return. Default: 20. Maximum: 50.
hotelIds | int* | No | See below.
refHotelId | int | No | See below.
latitude | float | No | See below.
longitude | float | No | See below.
radius | float | No | See below.
candidatesearch | boolean | No | See below.
rooms | int | Yes | Number of rooms needed. When searching for more than one room, responses are based on the same room type and occupancy for every room. Maximum: 9 (best results with no more than 4).
inDate | date | Yes | Desired check-in date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
outDate | date | Yes | Desired check-out date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
adults | int | Yes | Total number of adults. For instance, if `rooms=2&adults=2`, the search is for 1 room per adult. Maximum 8 adults per room. Uneven/odd numbers of adults/rooms will be rounded up to support legacy providers.
children | int | Yes | Total number of children. Maximum: 8. Note: Some legacy providers do not honor the `children` parameter. We suggest usually setting this to `0`.
sortType | string/enum | No | One of `bestvalue`, `dealpercent`, `dealamount`. Default: `bestvalue`. See below.
currency | string | No | Default: `USD`. See common value map.
name | string | No | Partial hotel name filter. E.g., passing "ilton" would return properties like "Hilton Garden Inn", etc.
propertyClasses | int* | No | See common value map.
propertyAmenities | int* | No | See common value map.
propertyTypes | int* | No | See common value map.
gateway | int* | No | See common value map.
ipAddress | string | Yes | The IPv4 address of the person browsing your website. This is used for fraud checking and preventing booking failures.
userAgent | string | Yes | The userAgent of the app/browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
userLanguage | string | Yes | The language of the browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
locale | string | No | Specifies the response language. Default: "US"
page | int | No | Specifies the results page to return (when more than one page of results is available).
_type | string/enum | No | The response format. One of `xml` or `json`. Default: `json`.

#### `hotelIds`, `locationId`, `refHotelId`, `latitude`+`longitude`+`radius`

One of the following is required:

* `hotelIds`: A list of integers, separated by commas if more than one. Max of 50 hotel IDs may be specified at one time. May be substituted with `refHotelId` or `locationId` or `latitude`+`longitude`+`radius`.
* `refHotelId`: A single hotel ID used to look up the city and return results from that city, as if we had searched by `locationId`. May be substituted with `hotelIds` or `locationId` or `latitude`+`longitude`+`radius`.
* `locationId`: A location ID used to return hotels from within the location's city. May be substituted with `hotelIds` or `refHotelId` or `latitude`+`longitude`+`radius`.
* `latitude` + `longitude` + `radius` (and maybe `candidatesearch`) (Do not send `radius` if doing `latitude`/`longitude` based deal search)
** `radius`: Measured in miles.  NOTE: If doing a market deal search, leave off radius and just pass `latitude` and `longitude`.
** `candidatesearch`: If a location based search is being made, this attribute can be sent to specify that no rates and availability should be returned. When set to true, and in conjunction with a location based search, only the list of candidate properties are returned (very fast). This allows calls to be made for each individual property asynchronously for actual rates and availability.

#### `sortType`

<aside class="notice">
  Note the `dealpercent` and `dealamount` sorting are related to historical discounts, not currently listed discounts.  You must sort the results of an availability search by the calculated percentage or given discount amount yourself after receiving the results of the query.
</aside>

Sort Type | Description
--------- | -------
`bestvalue` | The default sort type, based on previous booking trends and manual sorting options.
`dealpercent` | Sorts the hotel results based on prices last seen and returns the best percentage savings we have found historically (not currently) for the specified dates.
`dealamount` | Sorts the hotel results based on prices last seen and returns the best amount savings we have found historically (not currently) and for those dates.
