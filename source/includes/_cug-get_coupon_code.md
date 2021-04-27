## Get a Coupon/Code

"Coupons" or "Codes" can be used to give users a pre-defined number of "Points" (in API requests/responses). The points (1 point = 1 USD) may be used to discount select purchases within a closed user group.  The codes may either be used during checkout, or easier, added to a user account and automatically applied at checkout for the user for the maximum discount allowed for that transaction.

This endpoint retrieves the data related to a single coupon/code. The response will validate the code is legitimate, whether the code has been used already or not, the expiration date, and the discount (in points) that is available.

<aside class="notice">
Notice the `type=get`, which is the difference between this endpoint call and the call which is used to redeem a code, as noted below.
</aside>

```shell
curl "https://api.travsrv.com/Coupon.aspx?\
&siteid={SITEID}\
&type=get\
&couponcode={COUPON-CODE}" \
  -H 'Authorization: Basic {BASE64-ENCODED-STRING}'
```

> The above command returns JSON structured like this:

```json
{
  "IsValid": true,
  "Code": "123-4567890",
  "SiteId": 12345,
  "Message": "Is Valid For Up To 500.00 Off Purchase",
  "Data": {
    "IsActive": true,
    "IsUsed": false,
    "Discount": 500.0,
    "MinNights": 1,
    "ExpiresOn": "11/6/2018",
    "MaxUses": 1,
    "IsPercentage": false,
    "Terms": null
  }
}
```

> Codes which have been used would return something like this:

```json
{
  "IsValid": false,
  "Code": "114-4567890",
  "SiteId": 12345,
  "Message": "Is Already Used",
  "Data": {
    "IsActive": true,
    "IsUsed": true,
    "Discount": 500.0,
    "MinNights": 1,
    "ExpiresOn": "11/6/2018",
    "MaxUses": 1,
    "IsPercentage": false,
    "Terms": null
  }
}
```

### HTTP Request

`GET https://api.travsrv.com/Coupon.aspx`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
siteid | integer | Yes | Provided by QuintRooms
type | string | Yes | `get` (in this case), or `redeem` (see below)
couponcode | string | Yes | The code to lookup
