## Hotel Reservation Cancellation

To cancel a reservation you will need the `reservationId` and `itineraryId` returned in the reservation creation response.  These values are mapped 1-to-1, so both are needed and they likely will not be the same values, but will be related to each other.

```shell
curl -X POST "https://api.travsrv.com/hotel.aspx?\
&siteid={SITEID}\
&reservationId=915892\
&itineraryId=733525\
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
      "@IpAddress": "127.0.0.1",
      "@TimeReceived": "2018-04-01T19:16:35.581",
      "@TimeCompleted": "2018-04-01T19:16:36.065",
      "@Version": "1.0.0.0",
      "@ServiceUrl": "https://api.travsrv.com/hotel.aspx",
      "@RequestID": "52AEC4E5-BBB9-44CB-BF09-CFEE7462FE97"
    },
    "Cancellation": {
      "@DisplayCurrency": "USD",
      "@ItineraryID": "733525",
      "HotelCancellation": {
        "@Success": "true",
        "@CancelGMT": "2018-04-01T19:16:36.065",
        "@CancellationID": "ARN342559-C",
        "@InDate": "2018-04-10",
        "@OutDate": "2018-04-12",
        "@Rooms": "1",
        "@Adults": "2",
        "@Children": "0",
        "@ReservationID": "915892",
        "@CustomerConfirmationNumber": "ARN342559",
        "Hotel": {
          "@HotelID": "219295",
          "RatePlan": {
            "@Code": "ARN987654321",
            "@Description": "Internet Special",
            "@Gateway": "1",
            "Room": {
              "@Code": "987654321",
              "@Name": "Double Room",
              "@Description": "Double Room - one double bed, satellite television, minibar, coffee maker, in-room safe, work desk, air conditioning, hairdryer, private bathroom, complimentary breakfast buffet. Rate includes transportation from the airport to the hotel. Please enter your Airline and Flight Number in the 'Other Special Requests' field when placing your reservation. Rates based on single or double occupancy. (Maximum 2 people)",
              "@CurrencyCode": "USD",
              "@DisplayCurrencyMultiplier": "1",
              "@USDMultiplier": "1",
              "@ExchangeGMT": "2018-04-01T17:15:03.443",
              "@MaximumBookable": "5",
              "NightlyRate": {
                "@Date": "2018-04-10",
                "@Price": "144.00"
              },
              "Tax": {
                "@Percent": "20.00",
                "@Amount": "28.80"
              },
              "GatewayFee": {
                "@Amount": "0.00"
              },
              "Total": {
                "@Amount": "172.80",
                "@IncludesBookingFee": "false"
              },
              "BookingFee": {
                "@Amount": "3.60",
                "@CurrencyCode": "USD",
                "@DisplayCurrencyMultiplier": "1",
                "@RoomCurrencyMultiplier": "1",
                "@ExchangeGMT": "2018-04-01T17:15:03.443"
              }
            },
            "Policy": {
              "ExtraPersonPrice": {
                "@Adult": "0.00",
                "@Child": "0.00",
                "@CurrencyCode": "USD",
                "@DisplayCurrencyMultiplier": "1",
                "@USDMultiplier": "1",
                "@ExchangeGMT": "2018-04-01T17:15:03.443"
              },
              "Guarantee": {
                "@Description": "No prices or hotel availability are guaranteed until full payment is received. Booking fee is not included in the total and it's value is expressed in United States Dollars. Booking fee will be charged at the time of the booking."
              },
              "Cancel": {
                "@Description": "You must cancel your reservation before 2:00 pm hotel time at least 1 day(s) prior to check-in or you will be charged for one night's room plus taxes & fees.",
                "@LatestCancelTime": "2018-04-08T14:00:00.000",
                "@GMTOffSet": "0",
                "Fee": {
                  "@Amount": "10.00",
                  "@CurrencyCode": "USD",
                  "@DisplayCurrencyMultiplier": "1",
                  "@RoomCurrencyMultiplier": "1",
                  "@ExchangeGMT": "2018-04-01T17:15:03.443"
                },
                "Penalty": {
                  "@Amount": "172.80",
                  "@CurrencyCode": "USD",
                  "@DisplayCurrencyMultiplier": "1",
                  "@USDMultiplier": "1",
                  "@ExchangeGMT": "2018-04-01T17:15:03.443"
                }
              },
              "Deposit": {
                "@Description": "Credit card is charged for the total cost of the room at the time of booking."
              },
              "Payment": [
                {
                  "@Description": "Tax is included in the total."
                },
                {
                  "@Description": "Total Room Cost includes tax recovery charge and fees."
                },
                {
                  "@Description": "This discount rate requires full payment of reservation at time of booking."
                },
                {
                  "@Description": "Payment will appear on your credit card under Alliance Reservations Network, Phoenix, AZ"
                },
                {
                  "@Description": "Rooms are guaranteed once full payment is received."
                }
              ],
              "Property": [
                {
                  "@Description": "Check-In Time",
                  "@Value": "1600"
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
            "@FirstName": "Mary",
            "@MiddleName": "",
            "@LastName": "Andersen",
            "@Message": "Non-smoking room requested.",
            "@Email": "karianan@xxx.com",
            "@PhoneCountry": "0047",
            "@PhoneArea": "0",
            "@PhoneNumber": "5555555",
            "@PhoneExtension": "",
            "@AgeGroup": "Adult",
            "Address": {
              "@Address": "Vaar Frue gt 2",
              "@City": "Zeud",
              "@Region": "",
              "@PostalCode": "7013",
              "@CountryCode": "NO",
              "@ExtraInfo": ""
            }
          }
        },
        "Service": {
          "@ExchangeGMT": "2018-04-01T17:15:03.443",
          "RoomCurrency": {
            "@CurrencyCode": "USD",
            "Cost": {
              "@Price": "144.00",
              "@TaxPercent": "20.00",
              "@TaxAmount": "28.80",
              "@GatewayFee": "0.00",
              "@BookingFee": "3.60",
              "@TotalAmount": "176.40",
              "@TotalAmountIncludesBookingFee": "true"
            },
            "Charge": {
              "@Paid": "176.40",
              "@Due": "0.00"
            }
          },
          "DisplayCurrency": {
            "@CurrencyCode": "USD",
            "Cost": {
              "@Price": "144.00",
              "@TaxPercent": "20.00",
              "@TaxAmount": "28.80",
              "@GatewayFee": "0.00",
              "@BookingFee": "3.60",
              "@TotalAmount": "176.40",
              "@TotalAmountIncludesBookingFee": "true"
            },
            "Charge": {
              "@Paid": "176.40",
              "@Due": "0.00"
            }
          },
          "USD": {
            "@CurrencyCode": "USD",
            "Cost": {
              "@Price": "144.00",
              "@TaxPercent": "20.00",
              "@TaxAmount": "28.80",
              "@GatewayFee": "0.00",
              "@BookingFee": "3.60",
              "@TotalAmount": "176.40",
              "@TotalAmountIncludesBookingFee": "true"
            },
            "Charge": {
              "@Paid": "176.40",
              "@Due": "0.00"
            }
          }
        }
      }
    }
  }
}
```

### HTTP Request

`POST https://api.travsrv.com/hotel.aspx?type=Cancellation`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
siteid | integer | Yes | Provided by QuintRooms
reservationId | string | Yes | The `reservationId` from the reservation creation response.
itineraryId | string | Yes | The `itineraryId` from the reservation creation response.
_type | string/enum | No | The response format. One of `xml` or `json`. Default: `json`.
