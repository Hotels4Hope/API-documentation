## Create/Update a Coupon/Code

"Coupons" or "Codes" can be used to give users a pre-defined number of "Points" (in API requests/responses). The points (1 point = 1 USD) may be used to discount select purchases within a closed user group.  The codes may either be used during checkout, or easier, added to a user account and automatically applied at checkout for the user for the maximum discount allowed for that transaction.

This endpoint creates a single coupon/code.

> The JSON data to stringify and encode may look something like this (not yet encoded):

```json
{
  "Code": "123-4567890",
  "SiteId": 12345,
  "Data": {
    "IsActive": true,
    "IsUsed": false,
    "Discount": 500,
    "MinNights": 1,
    "ExpiresOn": "2018-11-06",
    "MaxUses": 1,
    "IsPercentage": false,
    "Terms": ""
  }
}
```

<aside class="notice">
Notice the `type=save` (and `POST` type), which are the differences between this endpoint call and others used to get or redeem a code, as noted below.
</aside>

<aside class="notice">
If the code already exists this call will update the info as provided.
</aside>

```shell
curl "https://api.travsrv.com/Coupon.aspx?\
&siteid={SITEID}\
&type=save\
&coupon=%7B%22Code%22%3A%22123-4567890%22%2C%22SiteId%22%3A12345%2C%22Data%22%3A%7B%22IsActive%22%3Atrue%2C%22IsUsed%22%3Afalse%2C%22Discount%22%3A500%2C%22MinNights%22%3A1%2C%22ExpiresOn%22%3A%222018-11-06%22%2C%22MaxUses%22%3A1%2C%22IsPercentage%22%3Afalse%2C%22Terms%22%3A%22%22%7D%7D" \
  -H 'Authorization: Basic {BASE64-ENCODED-STRING}'
```

> The above command returns JSON structured like this:

```json
{
  "IsValid": true,
  "Code": "123-4567890",
  "SiteId": 12345,
  "Message": "Is Valid For Up To 500 Off Purchase",
  "Data": {
    "IsActive": true,
    "IsUsed": false,
    "Discount": 500.0,
    "MinNights": 1,
    "ExpiresOn": "1/1/2018",
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
  "Code": "123-4567890",
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

`POST https://api.travsrv.com/Coupon.aspx`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
siteid | integer | Yes | Provided by QuintRooms
type | string | Yes | `save`
coupon | string | Yes | Stringified, URI encoded JSON object containing the params below
Code | string | Yes | The code string you want generated
SiteId | integer | Yes | Provided by QuintRooms
Data | object | Yes | JSON object containing the params below
IsActive | boolean | Yes | `true` if not expired and not redeemed
IsUsed | boolean | Yes | `true` if not yet redeemed
Discount | decimal | Yes | Amount the coupon is worth
MinNights | integer | Yes | Min requirement of nights to be able to use the code
ExpiresOn | date | Yes | Expiration date of this code (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
MaxUses | integer | Yes | Maximum number of times this code may be used
IsPercentage | boolean | Yes | `true` if Discount is a percentage of reservation amount. `false` if Discount is a real amount (1 = 1 USD).
Terms | string | Yes | Set to `""`.
