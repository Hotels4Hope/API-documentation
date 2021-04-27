## Get Property Info

You may retrieve specific property information via `GET` request, (authorized, as mentioned above, using a basic authentication header) to this endpoint. Calling this endpoint successfully will return a specific hold / room type's associated property information.

```shell
curl -X GET \
"https://groups.alliancereservations.com/services/external/property?id={PROPERTY-ID}" \
-H 'Authorization: Basic {BASE64-ENCODED-STRING}'
```

> The above command returns JSON structured like this:

```json
{
    "Id": 10165,
    "Name": "Courtyard by Marriott Orlando Lake Mary/North",
    "Address": "135 International Pkwy",
    "City": "Lake Mary",
    "State": "FL",
    "Postal": "32746",
    "Country": "US",
    "Phone": "1 800 555 9000",
    "Email": "someone@thisproperty.com"
}
```

### HTTP Request

`GET https://groups.alliancereservations.com/services/external/property`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
id | integer | Yes | The property id
