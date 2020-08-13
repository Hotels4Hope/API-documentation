## Get Hold by Room ID

You may retrieve a specific hold / room type via `GET` request, (authorized, as mentioned above, using a basic authentication header) to this endpoint. Calling this endpoint successfully will return a specific hold / room type information.

Included in a successful response will be a `PropertyInfoLink` which is the API endpoint URI for the specific property information this hold / room type is related to.

```shell
curl -X GET \
"https://groups.alliancereservations.com/services/external/roomtypesonhold?&roomTypeId={ROOM-TYPE-ID}" \
-H 'Authorization: Basic {BASE64-ENCODED-STRING}'
```

> The above command returns JSON structured like this:

```json
{
    "SiteId": 12345,
    "EventId": 67890,
    "EventName": "My Crazy Awesome Event",
    "EventStartDate": "2018-02-09T00:00:00",
    "RoomTypeId": 888888,
    "PropertyInfoLink": "https://groups.alliancereservations.com/services/external/property?id=987654",
    "Description": "2 Double beds with mini-fridge, microwave, coffee maker, and 32-inch TV. No breakfast included. Rate based on occupancy of 4 persons per room. You must be at least 21 years old to check into room.",
    "GroupName": "BandMembers-Doubles",
    "MaxOccupancy": 4,
    "BaseOccupancy": null,
    "AdultExtraCharge": 0,
    "ChildExtraCharge": 0,
    "ExtraAdultAge": null,
    "ReleaseDate": "2018-01-21T00:00:00",
    "PaymentPolicy": "",
    "CancellationPolicy": "You must change or cancel your reservation before 2:00 pm hotel time at least 3 day(s) prior to check-in or you will be charged for one night's room plus taxes & fees unless otherwise noted in the room description.",
    "Contacts": [
        {
            "FullName": "Donna Summers",
            "Email": "donna.summers@awesomeevent.com",
            "DaytimePhone": "(888) 555-1212",
            "EveningPhone": "(888) 555-1212",
            "IsPrimary": true
        }
    ],
    "BlockDates": [
        {
            "BlockDate": "2018-02-08T00:00:00",
            "Rate": 129,
            "MinimumNights": 1,
            "QuantityAvailable": 0
        },
        {
            "BlockDate": "2018-02-09T00:00:00",
            "Rate": 129,
            "MinimumNights": 1,
            "QuantityAvailable": 0
        },
        {
            "BlockDate": "2018-02-10T00:00:00",
            "Rate": 129,
            "MinimumNights": 1,
            "QuantityAvailable": 0
        },
        {
            "BlockDate": "2018-02-11T00:00:00",
            "Rate": 129,
            "MinimumNights": 1,
            "QuantityAvailable": 0
        }
    ]
}
```

### HTTP Request

`GET https://groups.alliancereservations.com/services/external/roomtypesonhold`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
roomTypeId | integer | Yes | The hold / room type id
