## Redeem a Coupon/Code

"Coupons" or "Codes" can be used to give users a pre-defined number of "Points" (in API requests/responses). The points (1 point = 1 USD) may be used to discount select purchases within a closed user group.  The codes may either be used during checkout, or easier, added to a user account and automatically applied at checkout for the user for the maximum discount allowed for that transaction.

This endpoint sets a single coupon/code to `isValid: false`, effectively indicating it's been used and should not be able to be used again. If the code is valid and the call is successfull, the response will look the same as if you were calling a `type=get` (as specified above under "Get a Coupon/Code"). Successive calls to either `type=get` or `type=redeem` will return a response indicating the code is no longer valid.

<aside class="notice">
Notice the `type=redeem`, which is the difference between this endpoint call and the call which is used to simply retrieve the data for a single coupon/code, as noted above.
</aside>

```shell
curl "https://api.travsrv.com/Coupon.aspx?\
&siteid={SITEID}\
&type=redeem\
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

> Subsequent calls will return the following:

```json
{
  "IsValid": false,
  "Code": "123-4567890",
  "SiteId": 12345,
  "Message": "Is Already Used",
  "Data": {
    "IsActive": true,
    "IsUsed": true,
    "Discount": 500.0
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
siteid | integer | Yes | Provided by Hotels For Hope
type | string | Yes | `get` (see above), or `redeem` (in this case)
couponcode | string | Yes | The code to invalidate
