## Get All Holds

You may retrieve a list of the room types on hold via `GET` request, (authorized, as mentioned above, using a basic authentication header) to this endpoint. Calling this endpoint successfully will return an array of API endpoing URIs for each room type currently on hold.

You may use the resulting URI (and the `roomTypeId` specified within) to retrieve specific hold / room type information.

<aside class="notice">
Either the `affiliateId` or `siteId` must be passsed into this endpoint.  This example uses `siteId`, which is the most likely use case.
</aside>

```shell
curl -X GET \
"https://groups.alliancereservations.com/services/external/roomtypesonhold?&siteId={SITE-ID}" \
-H 'Authorization: Basic {BASE64-ENCODED-STRING}'
```

> The above command returns JSON structured like this:

```json
{
    "TotalOnHoldRoomTypes":4,
    "OnHoldRoomTypes":[
        "https://groups.alliancereservations.com/services/external/roomtypesonhold?roomTypeId=1111",
        "https://groups.alliancereservations.com/services/external/roomtypesonhold?roomTypeId=2222",
        "https://groups.alliancereservations.com/services/external/roomtypesonhold?roomTypeId=3333",
        "https://groups.alliancereservations.com/services/external/roomtypesonhold?roomTypeId=4444"
    ]
}
```

### HTTP Request

`GET https://groups.alliancereservations.com/services/external/roomtypesonhold`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
siteId | integer | No | Provided by QuintRooms
affiliateId | integer | No | Provided by QuintRooms
includeExpired | void | No | Response includes expired holds
