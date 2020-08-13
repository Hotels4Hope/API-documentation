## Hotel Reservation Creation

Generally speaking this call should be self explanatory. The parameters you will be sending in regarding the fees and costs will come from the detail request you likely would have just made. This is used to double confirm the costs the user was given will match up with the costs in the suppliers / gateways.

```shell
curl -X POST "https://api.travsrv.com/hotel.aspx?\
&siteid={SITEID}\
&gateway=20\
&rooms=1\
&hotelIds=10731\
&rooms=1\
&inDate=2007-03-30\
&outDate=2007-03-31\
&adults=2\
&children=0\
&ratePlanCode=ARN987654321\
&roomCode=987654321\
&guestFirstName=Eddie\
&guestLastName=Collins\
&guestEmail=nobody@yahoo.com\
&guestPhoneCountry=1\
&guestPhoneArea=313\
&guestPhoneNumber=5555555\
&guestMessage=Smoking room requested.\
&addressAddress=123 main st\
&addressCity=detroit\
&addressRegion=MI\
&addressPostalCode=48234\
&addressCountryCode=US\
&roomCostPrice=98.95\
&roomCostTaxAmount=0.00\
&roomCostGatewayFee=0.00\
&roomCostTotalAmount=103.95\
&roomCostCurrencyCode=USD\
&creditCardType=VI\
&creditCardNumber=4242424242424242\
&creditCardExpiration="21/01"\
&creditCardCVV2=123\
&creditCardHolder=Eddie Collins\
&creditCardAddress=123 Main Street\
&creditCardCity=Detroit\
&creditCardRegion=MI\
&creditCardPostalCode=48234\
&creditCardCountryCode=US\
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
      "@TimeReceived": "2007-03-30T22:14:28.484",
      "@TimeCompleted": "2007-03-30T22:14:32.046",
      "@Version": "1.0.0.0",
      "@ServiceUrl": "https://api.travsrv.com/hotel.aspx",
      "@RequestID": "D392A38B-79EC-4064-9C8F-E2C9AFC2EEE6"
    },
    "Reservation": {
      "@DisplayCurrency": "USD",
      "@ItineraryID": "678595",
      "@RecordLocator": "4fa67dc1-9d40-46f4-aa34-eb236117781c",
      "HotelReservation": {
        "@InDate": "2007-03-30",
        "@OutDate": "2007-03-31",
        "@Rooms": "1",
        "@Adults": "2",
        "@Children": "0",
        "@ReservationID": "860964",
        "@CustomerConfirmationNumber": "40156457",
        "Hotel": {
          "@HotelID": "10731",
          "RatePlan": {
            "@Code": "ARN987654321",
            "@Description": "QUALIFYING MEMBER RATE: Aaa/CAA Rate 1 King Bed /1 Room Suite/Partial Room Divider /Microwave Refrigerator/Computer Hookup Guest Must Show Some Form Of Aaa Membership Rate Is Applicable To AAA Members Only And Only On Rooms They Stay In Themselv",
            "@Gateway": "4",
            "Room": {
              "@Code": "987654321",
              "@Name": "Room",
              "@Description": "QUALIFYING MEMBER RATE: Aaa/CAA Rate 1 King Bed /1 Room Suite/Partial Room Divider /Microwave Refrigerator/Computer Hookup Guest Must Show Some Form Of Aaa Membership Rate Is Applicable To AAA Members Only And Only On Rooms They Stay In Themselv",
              "@CurrencyCode": "USD",
              "@DisplayCurrencyMultiplier": "1",
              "@USDMultiplier": "1",
              "@ExchangeGMT": "2007-03-30T17:15:04.627",
              "@MaximumBookable": "1",
              "NightlyRate": {
                "@Date": "2007-03-30",
                "@Price": "98.95"
              },
              "Tax": {
                "@Percent": "0.00",
                "@Amount": "0.00"
              },
              "GatewayFee": {
                "@Amount": "0.00"
              },
              "Total": {
                "@Amount": "98.95",
                "@IncludesBookingFee": "false"
              },
              "BookingFee": {
                "@Amount": "5.00",
                "@CurrencyCode": "USD",
                "@DisplayCurrencyMultiplier": "1",
                "@RoomCurrencyMultiplier": "1",
                "@ExchangeGMT": "2007-03-30T17:15:04.627"
              }
            },
            "Policy": {
              "ExtraPersonPrice": {
                "@Adult": "5.00",
                "@Child": "0.00",
                "@CurrencyCode": "USD",
                "@DisplayCurrencyMultiplier": "1",
                "@USDMultiplier": "1",
                "@ExchangeGMT": "2007-03-30T17:15:04.627"
              },
              "Guarantee": {
                "@Description": "RESERVATION WILL BE HELD TILL 4PM LOCAL TIME Booking fee is not included in the total and it's value is expressed in United States Dollars. Booking fee will be charged at the time of the booking."
              },
              "Cancel": {
                "@Description": "CANCEL BY 4 PM LOCAL HTL TIME DOA",
                "@LatestCancelTime": "2007-03-29T10:00:00.000",
                "@GMTOffSet": "0",
                "Fee": {
                  "@Amount": "0.00",
                  "@CurrencyCode": "USD",
                  "@DisplayCurrencyMultiplier": "1",
                  "@RoomCurrencyMultiplier": "1",
                  "@ExchangeGMT": "2007-03-30T17:15:04.627"
                },
                "Penalty": {
                  "@Amount": "98.95",
                  "@CurrencyCode": "USD",
                  "@DisplayCurrencyMultiplier": "1",
                  "@USDMultiplier": "1",
                  "@ExchangeGMT": "2007-03-30T17:15:04.627"
                }
              },
              "Deposit": {
                "@Description": "None"
              },
              "Payment": [
                {
                  "@Description": "Tax is not included in the total."
                },
                {
                  "@Description": "With your credit card information, the room(s) you book are guaranteed for late arrival."
                },
                {
                  "@Description": "This discount rate requires a $5.00 (USD) per room per night non-refundable service fee at time of reservation and will appear on your credit card under Alliance Reservations Network, Phoenix, AZ."
                }
              ],
              "Property": [
                {
                  "@Description": "Check-In Time",
                  "@Value": "150000"
                },
                {
                  "@Description": "Check-Out Time",
                  "@Value": "1100"
                }
              ]
            }
          }
        },
        "Guests": {
          "Primary": {
            "@Title": "",
            "@FirstName": "Eddie",
            "@MiddleName": "",
            "@LastName": "Collins",
            "@Message": "Smoking room requested.",
            "@Email": "nobody@yahoo.com",
            "@PhoneCountry": "1",
            "@PhoneArea": "313",
            "@PhoneNumber": "5555555",
            "@PhoneExtension": "",
            "@AgeGroup": "Adult",
            "Address": {
              "@Address": "123 main st",
              "@City": "detroit",
              "@Region": "MI",
              "@PostalCode": "48234",
              "@CountryCode": "US",
              "@ExtraInfo": ""
            }
          }
        },
        "Service": {
          "@ExchangeGMT": "2007-03-30T17:15:04.627",
          "RoomCurrency": {
            "@CurrencyCode": "USD",
            "Cost": {
              "@Price": "98.95",
              "@TaxPercent": "0.00",
              "@TaxAmount": "0.00",
              "@GatewayFee": "0.00",
              "@BookingFee": "5.00",
              "@TotalAmount": "103.95",
              "@TotalAmountIncludesBookingFee": "true"
            },
            "Charge": {
              "@Paid": "5.00",
              "@Due": "98.95"
            }
          },
          "DisplayCurrency": {
            "@CurrencyCode": "USD",
            "Cost": {
              "@Price": "98.95",
              "@TaxPercent": "0.00",
              "@TaxAmount": "0.00",
              "@GatewayFee": "0.00",
              "@BookingFee": "5.00",
              "@TotalAmount": "103.95",
              "@TotalAmountIncludesBookingFee": "true"
            },
            "Charge": {
              "@Paid": "5.00",
              "@Due": "98.95"
            }
          },
          "USD": {
            "@CurrencyCode": "USD",
            "Cost": {
              "@Price": "98.95",
              "@TaxPercent": "0.00",
              "@TaxAmount": "0.00",
              "@GatewayFee": "0.00",
              "@BookingFee": "5.00",
              "@TotalAmount": "103.95",
              "@TotalAmountIncludesBookingFee": "true"
            },
            "Charge": {
              "@Paid": "5.00",
              "@Due": "98.95"
            }
          }
        }
      }
    }
  }
}
```

### HTTP Request

`POST https://api.travsrv.com/hotel.aspx?type=Reservation`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
siteid | integer | Yes | Provided by Hotels For Hope
hotelIds | int | Yes | The particular hotel id to reserve the room at.
agentRefNumber | string | No | A reference ID you may use for your own tracking purposes. This is included in a reservation webhook, if used.
rooms | int | Yes | Number of rooms needed. Maximum: 9.
inDate | date | Yes | Desired check-in date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
outDate | date | Yes | Desired check-out date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
adults | int | Yes | Total number of adults. For instance, if `rooms=2&adults=2`, the search is for 1 room per adult. Maximum 8 adults per room. Uneven/odd numbers of adults/rooms will be rounded up to support legacy providers.
children | int | Yes | Total number of children. Maximum: 8. Note: Some legacy providers do not honor the `children` parameter. We suggest setting this value to `0` for most inquiries.
currency | string | No | Default: `USD`. See common value map.
ratePlanCode | string | Yes | See common value map.
roomCode | string | Yes | See common value map.
gateway | int | yes | See common value map.
campaignCode | string | No | See below.
guestTitle | string | No | Primary guest's title (e.g., "Mr.", "Mrs.", etc.)
guestFirstName | string | Yes | Primary guest's first name
guestLastName | string | Yes | Primary guest's last name.
guestEmail | string | Yes | Primary guest's email address.
guestPhoneCountry | string | Yes | Primary guest's phone number country code.
guestPhoneArea | string | Yes | Primary guest's phone number area code.
guestPhoneNumber | string | Yes | Primary guest's phone number (without country or area code)
guestPhoneExtension | string | No | Primary guest's phone number extension.
guestMessage | string | No | Guest special requests.
addressAddress | string | Yes | Primary guest's address.
addressCity | string | Yes | Primary guest's city.
addressRegion | string | Yes | Primary guest's state / region.
addressPostalCode | string | Yes | Primary guest's postal code.
addressCountryCode | string | Yes | Primary guest's country code.
roomCostPrice | decimal | Yes | See below.
roomCostTaxAmount | decimal | Yes | See below.
roomCostGatewayFee | decimal | Yes | See below.
roomCostTotalAmount | decimal | Yes | See below.
roomCostCurrencyCode | string | Yes | See below.
bookingFeeAmount | decimal | Yes | See below.
bookingFeeCurrencyCode | string | See common value map for `currency`.
creditCardType | string | Yes | Options: "AX" (AMEX), "CA" (MasterCard), "VI" (Visa), "DC" (Discover)
creditCardNumber | string | Yes | Credit card number.
creditCardExpiration | string | Yes | Credit card expiration date (format: `MM/YY`)
creditCardCVV2 | int | Yes | Credit card CVV2 number.
creditCardHolder | string | Yes | Name on credit card.
creditCardAddress | string | Yes | Credit card billing address.
creditCardCity | string | Yes | Credit card billing city.
creditCardRegion | string | Yes | Credit card billing state / region.
creditCardPostalCode | string | Yes | Credit card billing postal code.
creditCardCountryCode | string | Yes | Credit card billing country code.
ipAddress | string | Yes | The IPv4 address of the person browsing your website. This is used for fraud checking and preventing booking failures.
userAgent | string | Yes | The userAgent of the app/browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
userLanguage | string | Yes | The language of the browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
locale | string | No | Specifies the response language. Default: "US"
_type | string/enum | No | The response format. One of `xml` or `json`. Default: `json`.

#### `campaignCode`

You may pass in a string which you want to persist with the reservation.  This is analagous to a "subid" and can be used for reconciling with your own marketing campaigns, or really anything else you want to do with it.  The string you provide in this parameter will be added to the reservation being made and available in available reporting.

#### `roomCostPrice`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

#### `roomCostTaxAmount`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

#### `roomCostGatewayFee`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

#### `roomCostTotalAmount`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

#### `roomCostCurrencyCode`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

#### `bookingFeeAmount`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.
