## Cancel a Hold

You may retrieve a list of the room types (you'll need the room code / room type id) available to put on hold via an Availability Search and specifying gateway `16` (contracted inventory) (authorized, as mentioned above, using a basic authentication header) to this endpoint. **IMPORTANT NOTE:** Calling this endpoint successfully will return a string (URL), not JSON-encoded.

```shell
curl -X POST \
"https://groups.alliancereservations.com/services/external/roomtypesonhold?&roomTypeId={ROOM-TYPE-ID}&cancelHold" \
-H 'Authorization: Basic {BASE64-ENCODED-STRING}'
```

> The above command returns a string like this:

```
https://groups.alliancereservations.com/services/external/roomtypesonhold?&roomTypeId=111111
```

### HTTP Request

`POST https://groups.alliancereservations.com/services/external/roomtypesonhold`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
roomTypeId | integer | Yes | The RoomTypeId you want to cancel a hold on
cancelHold | void | Yes | Specifies this is a cancellation

### POST form-data Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
cancellationReason | string | Yes | Reason for cancellation
