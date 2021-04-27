## Create a Hold

You may retrieve a list of the room types (you'll need the room code / room type id) available to put on hold via an Availability Search and specifying gateway `16` (contracted inventory) (authorized, as mentioned above, using a basic authentication header) to this endpoint. 

NOTE: When setting the POST form-data Parameters (seen below), be sure the number of values in the comma separated list specified for "roomCountPerNight" match the number of nights (inclusive) specified in the "blockStartDate" / "blockEndDate" range.  Further, the "blockStartDate" (ie, check-in date) must be > today's date. "blockEndDate" (ie, the day before the check-out date) must be > "blockStartDate".  "blockReleaseDate" must be < "blockStartDate" and > today.

For instance, (assuming today's date is < Nov 30, 2019) if the "blockStartDate" = "12/01/2019" and the "blockEndDate" = "12/03/2019", the "roomCountPerNight" should have 3 values, like "1,1,1".  The "blockReleaseDate" must be prior or equal to "11/30/2019".

Additionally, the "blockStartDate" and "blockEndDate" need to be within the parent room type's block dates or the system won't be able to allocate rooms from the parent to hold block.

```shell
curl -X POST \
"https://groups.alliancereservations.com/services/external/roomtypesonhold?&roomTypeId={ROOM-TYPE-ID}&createHold" \
-H 'Authorization: Basic {BASE64-ENCODED-STRING}'
```

> The above command returns JSON structured like this:

```json
{
    "SiteId": 12345,
    "EventId": 54321,
    "EventName": "2018 Test Event",
    "EventStartDate": "2022-02-01T00:00:00",
    "RoomTypeId": 111111,
    "PropertyInfoLink": "https://groups.alliancereservations.com/services/external/property?id=56789",
    "Description": "King\r\n\r\nThis is a test room. Reservatinons will not be honored.\r\n\r\nNo breakfast included. Rate based on occupancy of 1 persons per room.",
    "GroupName": "Some new block description",
    "MaxOccupancy": 2,
    "BaseOccupancy": null,
    "AdultExtraCharge": null,
    "ChildExtraCharge": 0,
    "ExtraAdultAge": null,
    "ReleaseDate": "2022-01-17T00:00:00",
    "PaymentPolicy": "",
    "CancellationPolicy": "Cancellation must be received 2 day(s) prior to day of arrival or will result in a penalty of 1 night's room plus tax",
    "Contacts": [
        {
            "FullName": "Eddie Collins",
            "Email": "nobody@yahoo.com",
            "DaytimePhone": "888-555-1212",
            "EveningPhone": null,
            "IsPrimary": true
        }
    ],
    "BlockDates": [
        {
            "BlockDate": "2022-02-02T00:00:00",
            "Rate": 5,
            "MinimumNights": 1,
            "QuantityAvailable": 1
        },
        {
            "BlockDate": "2022-02-03T00:00:00",
            "Rate": 5,
            "MinimumNights": 1,
            "QuantityAvailable": 2
        }
    ]
}
```

### HTTP Request

`POST https://groups.alliancereservations.com/services/external/roomtypesonhold`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
roomTypeId | integer | Yes | `ArnResponse.Availability.HotelAvailability.Hotel.RatePlan.Room@Code` from an Availability Search (parent block). This is specifying the room from the parent block that you want to create a hold (sub-block) out of.
createHold | void | Yes | Specifies this is a create action

### POST form-data Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
blockDescription | string | Yes | Name this on hold block (anything you would like)
roomCountPerNight | integer | Yes | Comma delimited list of the number of rooms to hold for each night. (ie., "1,1,1" would be 1 room for all 3 nights of the date range)
blockStartDate | date | Yes | Start date of held rooms (ie., check-in date) (format: mm/dd/yyyy) (must be > today's date)
blockEndDate | date | Yes | Last night to hold (ie., the date prior to the check-out date) (format: mm/dd/yyyy) (must be > blockStartDate)
blockReleaseDate | date | Yes | Date when hold will expire (must be > today and < blockStartDate).
