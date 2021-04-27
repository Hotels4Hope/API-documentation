## Get a Token for a Site Admin

This endpoint returns an auth token for an administrative user, valid for 1 hour, which may be used to create or update new (non-administrative) users and their tokens.

Along with the other common parameters to replace, additionally you must replace `{ADMIN-USERNAME}` with the username the Site Admin user uses to login to the site/portal.

<aside class="notice">
The token (`CurrentToken`) will be URI encoded to ensure a valid JSON response. When using it in a POST-based API call, be sure to decode it.  If using it in URLs, when creating/using a SSO link for example, leave it encoded.
</aside>

```shell
curl "https://api.travsrv.com/MemberAPI.aspx?\
&siteid={SITEID}\
&token=ARNUSER-{ADMIN-USERNAME}" \
  -H 'Authorization: Basic {BASE64-ENCODED-STRING}'
```

> The above command returns JSON structured like this:

```json
{
    "MemberId": 918236,
    "Rewards": 0,
    "Points": 0,
    "RedemptionMultiplier": 1,
    "EarnMultiplier": 1,
    "Names": [
        {
            "FirstName": "Joe",
            "LastName": "Schmoe",
            "BirthDate": null,
            "Email": "joe@whatever.com",
            "Address1": "",
            "Address2": null,
            "City": "",
            "State": null,
            "Country": null,
            "Postal": "",
            "Longitude": null,
            "Latitude": null,
            "HomePhone": null,
            "Referral": "",
            "ReferralId": "",
            "Password": null,
            "IsActive": true,
            "DeleteMember": false,
            "UpdateMemberUsername": false,
            "FullName": "Joe Schmoe"
        }
    ],
    "DebugData": "Retrieval Time: 3ms",
    "Error": null,
    "CurrentToken": "%2bzkm8%2feXTB11eE0%2fIoDmDQruFMVpaxVX7WHx%2bT%2fT%2bkUPwOEtWBPPI3mKIItze5fXabC*(&ehmkxTPbnCvp4llCDhxS37DyiKrSiaLHUeydpMnzU3Wc4AusJZHzaylHUNmDfhMs%2fpG39VDoeQ47T0wehE%2fVjWV%2f3bZ5qUARYGzAvLP884khJxCYWvopS5w1V%2bXtSWXQeBw4Sqvz9Fz4dr7Oc58%2bKLuF99D8t3VfJvOMt9y%2bGdUK87DAXzQ0kpmLbR1vUCMpmPx3KDBtapqow8RoYInQtICzMUV18%2fv8jp6wgg4GPFPfy7X3n8GcMyj3HPfibBqlP054zu3c%2fmnk07EvtFpeHy4uAR6CEIg7wZa52I3xBJQeaQwKtp6Ju8Y4FbcHsewPPlSMpkSFHFGSeyK62U4PsPEWMEWwlUR28gZ0VcBBriuySb5pwZ8OHqBmCMr9NPsywSnqBRkI22cihTHmDL5wKvSkPAmxuf0Y3xmG3E9Pe7HTHhVD%2b7K2pE5iaQwtYD5H3yoTHwQNxDqmGuFQIVEZxjysyVNM1ddfqNnVenT%2fT1RMZpoPOIEQKzMKldPBn67UTYDNs489XbwOxg86WqYNM5il%2fv79ebducj8htsAViLxuT7sFp%2fVGvUdkcP3bN3%2ftqNg",
    "TransactionResponse": null,
    "MetaTag": "{\"MemberId\":918236,\"Rewards\":0,\"Points\":0,\"RedemptionMultiplier\":1.0,\"EarnMultiplier\":1.0,\"Names\":[{\"FirstName\":\"Joe\",\"LastName\":\"Schmoe\",\"BirthDate\":null,\"Email\":\"joe@whatever.com\",\"Address1\":\"\",\"Address2\":null,\"City\":\"\",\"State\":null,\"Country\":null,\"Postal\":\"\",\"Longitude\":null,\"Latitude\":null,\"HomePhone\":null,\"Referral\":\"\",\"ReferralId\":\"\",\"Password\":null,\"IsActive\":true,\"DeleteMember\":false,\"UpdateMemberUsername\":false,\"FullName\":\"Joe Schmoe\"}],\"DebugData\":null,\"Error\":null,\"CurrentToken\":null,\"TransactionResponse\":null,\"MetaTag\":null,\"MemberUsername\":\"joe@whatever.com\",\"MemberProvider\":\"ReserveTravel\",\"IsArnProvider\":true,\"AdditionalInfo\":null,\"MemberType\":\"Wholesale\"}",
    "MemberUsername": "joe@whatever.com",
    "MemberProvider": "ReserveTravel",
    "IsArnProvider": true,
    "AdditionalInfo": null,
    "MemberType": "Wholesale"
}
```

### HTTP Request

`GET https://api.travsrv.com/MemberAPI.aspx`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
siteid | integer | Yes | Provided by Hotels For Hope
token | string | Yes | `ARNUSER-` concatonated with the Site Admin's username
