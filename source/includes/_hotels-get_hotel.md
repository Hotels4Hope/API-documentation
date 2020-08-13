## Hotel Detail

This call confirms availability with the supplier / gateway (requests to skip any caching they have in place) and retrieves cancellation and booking policies to display prior to the user placing a reservation.

This call is only available for a single hotel ID, room code, and rate code.

Responses will contain nightly rates, taxes and fees associated with the room, and hotel, payment, and cancellation policies which apply to the rate.

This request is rate limited as it is an expensive request to make. Responses with a 429 status code are in response to over use, should you exceed the rate limit. 

Failed responses indicate the rate is sold out. Subsequent availability calls will flush and re-cache this hotel's rates.

**All fees, penalties, and policies from this response must be shown to the user before creating a reservation.**

All room prices are based on the number of adults per room specified in the request.  A response containing an extra adult fee of `0` may simply mean the pricing is not available. Adding more than the specified number of adults to the room because the extra adult fee is `0` will likely incur a price difference when the guest arrives at the hotel. To avoid this, we advise not to depend on the extra adult fee specified in the response when it comes to pricing.


```shell
curl "https://api.travsrv.com/hotel.aspx?\
&siteid={SITEID}\
&hotelIds=272393\
&inDate=2018-10-20\
&outDate=2018-10-22\
&maxResults=1\
&rooms=1\
&adults=2\
&children=0\
&gateway=51\
&ratePlanCode=987654321\
&roomCode=HRLM--_eJwFwcuaczAAANAHmgVRCRaziPRvxkyJadx3biWUfkFH9On_fc5BTlaYBzSSx4m6Iwz3cS_pRnKxCtkQzjqPQZm8Lh771NInUK3ri_pDYTzZL6lQtgl0H0_fOj_f5dRd1kT_pX8dtg_pq0LMTJYHFXNuPqi0PxdLuTjEAeTtKNfYZ3Gd3suIjMbm3_prdXk03gvS_pfpUJnL_poCL9kNoyIlpA2DURM1_fqAtELSKYuKh6e248vaSGk9hE9Dns4MYIncb5jC_fcZG_p_fOeSN3Z0N_fib2UqSpSLCPFgqPX2sQTP9rmXEv_ptXOMVOlVLoC_fujzlUz6tJvvFwUEonyP6njavHdzsVVF2EesNGSmILz3twKMBKm_fp7PK2XCcgV8ghjMc93ZaXrLkm622zmAYaTaPSItlgfYOcO2TSZ6hvwXlxw_fSAVdl9fv4Hwe6AJQ\
&ipAddress=127.0.0.1\
&userAgent=shell\
&userLanguage=en\
&_type=json" \
  -H 'Authorization: Basic {BASE64-ENCODED-STRING}' \
```

> The above command returns JSON structured like this (edited for brevity):

```json
{
  "ArnResponse": {
    "Info": {
      "@SiteID": "{SITEID}",
      "@Username": "{API-USERNAME}",
      "@IpAddress": "24.113.225.28",
      "@TimeReceived": "2018-04-17T00:41:27.367",
      "@TimeCompleted": "2018-04-17T00:41:27.804",
      "@Version": "1.0.0.0",
      "@ServiceUrl": "http://api.travsrv.com/hotel.aspx?_type=json&adults=2&children=0&gateway=51&hotelIds=272393&inDate=2018-10-20&ipAddress=127.0.0.1&maxResults=1&outDate=2018-10-22&&ratePlanCode=&roomCode=HRLM--_eJwFwcuaczAAANAHmgVRCRaziPRvxkyJadx3biWUfkFH9On_fc5BTlaYBzSSx4m6Iwz3cS_pRnKxCtkQzjqPQZm8Lh771NInUK3ri_pDYTzZL6lQtgl0H0_fOj_f5dRd1kT_pX8dtg_pq0LMTJYHFXNuPqi0PxdLuTjEAeTtKNfYZ3Gd3suIjMbm3_prdXk03gvS_pfpUJnL_poCL9kNoyIlpA2DURM1_fqAtELSKYuKh6e248vaSGk9hE9Dns4MYIncb5jC_fcZG_p_fOeSN3Z0N_fib2UqSpSLCPFgqPX2sQTP9rmXEv_ptXOMVOlVLoC_fujzlUz6tJvvFwUEonyP6njavHdzsVVF2EesNGSmILz3twKMBKm_fp7PK2XCcgV8ghjMc93ZaXrLkm622zmAYaTaPSItlgfYOcO2TSZ6hvwXlxw_fSAVdl9fv4Hwe6AJQ&rooms=1&siteid={SITEID}&userAgent=shell&userLanguage=en",
      "@RequestID": "2999AB6A-6DB9-4FFF-9586-BBED51BB6108"
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
          "@HotelInfo": "https://api.travsrv.com/api/content/findpropertyinfo?propertyid=272393&locale={{locale}}",
          "@Latitude": "30.2334",
          "@Longitude": "-97.74027",
          "@Name": "La Quinta Inn Austin Oltorf",
          "@Address1": "1603 East Oltorf Blvd",
          "@City": "Austin",
          "@CountryCode": "US",
          "@ImageThumbnail": "https://media.travsrv.com/272393/124017095_70.jpg",
          "@LocationDescription": "Near South Congress Avenue",
          "@TripAdvisorReviewCount": "377",
          "@TripAdvisorRating": "2.5",
          "@PriceClass": "2 Stars"
          "RatePlan": [
            {
              "@Code": "ARN987654321",
              "@Description": "Best Available",
              "@BuyerOnly": "false",
              "@Gateway": "41",
              "@CommissionStatus": "Commissionable",
              "@BalanceDueAtHotel": "false",
              "Room": {
                "@Code": "987654321",
                "@Name": "Standard room",
                "@Description": "- 1 King Bed - Nonsmoking Room - Free Breakfast, Free Wifi, Fridge, Microwave",
                "@CurrencyCode": "USD",
                "@DisplayCurrencyMultiplier": "1",
                "@USDMultiplier": "1",
                "@ExchangeGMT": "2018-04-17T00:00:06.027",
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
                  "@ExchangeGMT": "2018-04-17T00:00:06.027"
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
siteid | integer | Yes | Provided by Hotels For Hope
timeout | int | No | Maximum time to allow for searching gateways, measured in seconds. Default: 15
hotelIds | int | No | The particular hotel id for which more detail is being requested.
rooms | int | Yes | Number of rooms needed. When searching for more than one room, responses are based on the same room type and occupancy for every room. Maximum: 9 (best results with no more than 4).
inDate | date | Yes | Desired check-in date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
outDate | date | Yes | Desired check-out date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
adults | int | Yes | Total number of adults. For instance, if `rooms=2&adults=2`, the search is for 1 room per adult. Maximum 8 adults per room. Uneven/odd numbers of adults/rooms will be rounded up to support legacy providers.
children | int | Yes | Total number of children. Maximum: 8. Note: Some legacy providers do not honor the `children` parameter.
currency | string | No | Default: `USD`. See common value map.
ratePlanCode | string | Yes | See common value map.
roomCode | string | Yes | See common value map.
gateway | int | No | See common value map.
ipAddress | string | Yes | The IPv4 address of the person browsing your website. This is used for fraud checking and preventing booking failures.
userAgent | string | Yes | The userAgent of the app/browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
userLanguage | string | Yes | The language of the browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
locale | string | No | Specifies the response language. Default: "US"
_type | string/enum | No | The response format. One of `xml` or `json`. Default: `json`.
