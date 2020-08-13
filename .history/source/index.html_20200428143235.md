---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - intro
  - auth
  - auth-basic_authentication
  - auth-sso
  - common_value_maps
  - cug
  - cug-get_site_admin_token
  - cug-create_member
  - cug-update_member
  - cug-get_member
  - cug-upsert_coupon_code
  - cug-get_coupon_code
  - cug-redeem_coupon_code
  - cug-holds
  - cug-holds-create_hold
  - cug-holds-get_all_holds
  - cug-holds-get_by_room_id
  - cug-holds-get_property
  - cug-holds-cancel_hold
  - hotels-and-availability
  - hotels-search
  - hotels-get_hotel
  - hotels-create_reservation
  - hotels-cancel_reservation
  - deals
  - deals-featured-locations
  - deals-featured-hotels
  - deals-locationid-search
  - errors

search: true
---

# Introduction

Welcome to the Hotels For Hope API! You can use our API to access Hotels For Hope API endpoints, which can get information on hundreds of thousands of hotels, their availability, details, as well as create and cancel reservations.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

## Query String

Hotels For Hope uses a querystring username and password to allow access to the API. You can request Hotels For Hope API credentials by partnering with us and emailing [support](mailto:hello@hotelsforhope.com).

The API credentials are expected in all API requests to the server in the querystring like the following:

`&username={API-USERNAME}&password={API-PASSWORD}&siteid={SITEID}`

<aside class="notice">
You must replace <code>{API-USERNAME}</code>, <code>{API-PASSWORD}</code>, and <code>{SITEID}</code> with your personal API credentials and Site ID respectively.
</aside>

<aside class="warning">
Considering the sensitive nature of query string based API calls, we highly suggest not exposing these credentials by using them in client-side scripting languages like JavaScript. We recommend making calls with these credentials only using server-side technologies.
</aside>

## Single Sign On (SSO)

If you wish to integrate our closed user group portal/site with your own applications and user group, you can utilize our SSO functionality.

Process: 

1. [Request a Site Admin](mailto:hello@hotelsforhope.com?Subject=Request%20for%20Site%20Admin%20User) to be added to your closed user group site (if you don't already have one)
2. Get a token for the Site Admin
3. Create a member using the Site Admin's token
4. Use the member's token in queries on the user's behalf

<aside class="notice">
If you use our portal's UI and wanted to linking directly to a particuilar page without requiring login, use the parameter `memberToken={MEMBER-TOKEN}` in the URL (replacing <code>{MEMBER-TOKEN}</code> with the browsing user's token).
</aside>

# Common value maps

## `currency`

Supported currencies are located in our static database files. Request access if needed. Major 3-letter currency references (e.g., "USD", "CNY", "CAD", etc.) are supported.

## `gateway`

Optional filter. This should be either left empty to return all sources of supply or specified by a single integer or comma separated list of integers. 

Please [contact us](mailto:hello@hotelsforhope.com?Subject=Request%20for%20API%20Gateway%20Codes) for an updated list of gateways.

## `propertyAmenities`

Optional filter. This should either be an integer or a list of comma separated integers represented by the following:

Amenity ID | Amenity
--------- | ------- 
1 | Airport shuttle
2 | Social hour
3 | Fitness center
4 | Internet access
5 | Free local calls
6 | Complimentary breakfast
7 | Pets allowed
8 | Pool
9 | Restaurant on-site
10 | Kitchen / kitchenette

## `propertyClasses`

Optional filter. This should either be an integer or a list of comma separated integers represented by the following.

Property Class | Star Rating | Description
--------- | ------- | -------
1 | 1 | Economy
2 | 2 | Budget
3 | 3 | Moderate 
4 | 4 | Premium
5 | 5 | Luxury

## `propertyTypes`

Optional filter. This should either be an integer or a list of comma separated integers represented by the following:

Property Type ID | Property Type
--------- | ------- 
1 | Hotel
5 | Motel
6 | Resort
8 | Extended stay property
9 | Bed and breakfast
12 | Vacation rental

## `roomCode`

This is the `ArnResponse.Availability.HotelAvailability.Hotel.RatePlan.Room.@Code` value specified in the Availability Search results for the room type you are interested.

## `ratePlanCode`

This is the `ArnResponse.Availability.HotelAvailability.Hotel.RatePlan.@Code` value specified in the Availability Search results for the rate plan you are interested in.

# Closed user groups

This section is only for those using the SSO Authentication feature and pertains to managing users and their authentication tokens.  

You will need a Site Admin user in your closed user group site. If you don't already have one, please [request one](mailto:hello@hotelsforhope.com?Subject=Request%20for%20Site%20Admin%20User) be added for your portal/site.

## Get a Token for a Site Admin

This endpoint returns an auth token for an administrative user, valid for 1 hour, which may be used to create or update new (non-administrative) users and their tokens.

Along with the other common parameters to replace, additionally you must replace `{ADMIN-USERNAME}` with the username the Site Admin user uses to login to the site/portal.

<aside class="notice">
The token (`CurrentToken`) will be URI encoded to ensure a valid JSON response. When using it in a POST-based API call, be sure to decode it.  If using it in URLs, when creating/using a SSO link for example, leave it encoded.
</aside>

```shell
curl "https://api.travsrv.com/MemberAPI.aspx?\
username={API-USERNAME}\
&password={API-PASSWORD}\
&siteid={SITEID}\
&token=ARNUSER-{ADMIN-USERNAME}"
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
username | string | Yes | Provided by Hotels For Hope
password | string | Yes | Provided by Hotels For Hope
siteid | integer | Yes | Provided by Hotels For Hope
token | string | Yes | `ARNUSER-` concatonated with the Site Admin's username

## Create a New Member

Using the Site Admin's token you may create a new member by POSTing a *URI encoded* JSON string to this endpoint. Calling this endpoint successfully generates a member token, found in the `CurrentToken` property, which you should save for them if you want to use the "Get a Member by Token" call.

You may notice this call is exactly the same as the "Update an Existing Member" call.

> The JSON data to stringify and encode may look something like this (not yet encoded):

```json
{
    "Points": 100,
    "Names": [{
        "ReferralId": "mytestuser1@gmail.com",
        "FirstName": "Testme",
        "LastName": "Tester",
        "Email": "mytestuser1@gmail.com",
        "Address1": "123 Main Street",
        "HomePhone": "5551231212"
    }]
}
```

<aside class="notice">
The `Points` attribute is only necessary if you want to update the number of points for the member specified. Please note that it will update the member's points to the value specified, not increment or decrement.
</aside>

<aside class="notice">
The JSON structure includes an array of `Names`, which seems to infer the ability to create more than one person. However, in reality, you should only send this call for one member at a time.
</aside>

> Encoded and POSTed via curl:

```shell
curl -X POST \
  https://api.travsrv.com/MemberAPI.aspx \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'siteid={SITEID}&token={ADMIN-TOKEN}&memberData=%7B%22Points%22%3A100%2C%22Names%22%3A%5B%7B%22ReferralId%22%3A%22mytestuser1%40gmail.com%22%2C%22FirstName%22%3A%22Testme%22%2C%22LastName%22%3A%22Tester%22%2C%22Email%22%3A%22mytestuser1%40gmail.com%22%2C%22Address1%22%3A%22123%20Main%20Street%22%2C%22HomePhone%22%3A%225551231212%22%7D%5D%7D'
```

> The above command returns JSON structured like this:

```json
{
    "MemberId": 54321,
    "Rewards": 0,
    "Points": 100,
    "RedemptionMultiplier": 1.0,
    "EarnMultiplier": 1.0,
    "Names": [{
        "FirstName": "Testme",
        "LastName": "Tester",
        "BirthDate": null,
        "Email": "mytestuser1@gmail.com",
        "Address1": "123 Main Street",
        "Address2": null,
        "City": null,
        "State": null,
        "Country": null,
        "Postal": null,
        "Longitude": null,
        "Latitude": null,
        "HomePhone": "5551231212",
        "Referral": null,
        "ReferralId": "mytestuser1@gmail.com",
        "Password": null,
        "IsActive": true,
        "DeleteMember": false,
        "UpdateMemberUsername": false,
        "FullName": "Testme Tester"
    }],
    "DebugData": " Successful creation of Member RT-12345-mytestuser1@gmail.com",
    "Error": null,
    "CurrentToken": "E7MUlbdRdlq2RwSs8V4%2fhza25Xwca%2fZLodi%2faddmPl%2bJfpCU7VovYjoSKaMk34PvkSDpD1mqvezzQG0abXzuXP1%2baaiIKCLw7ehGaiI7BNI7Pb%2fYK%2fGJf4fCxKCz5EodA79iweA6gc2nCEOdWmkarTuy4Cd%2f5WtNkU043rF42sshCKGkg%2bIavKgJ6emdL7msPJRykM2hf%2fmHjdDOV%2b7jtuOHpk5bAVVIc5jhUqmqJMa5908EK0VoX1OUT60SkDcw2YLBeXEg6sYPu1Q7mTPc5VUhJ%2b6C6wHM08eOKMrKt6LNRxoB0kXcPyVS1azt1LR48yAegw%2fKXPbdgrCBycjsDedm0ItP9SmW1C6Byw4nt5zivxf%2f0ZIMF07wtZ4JhWVqGuhetKPDE3ddzOLRPyjNgetWddHqoq8Tba%2bKWDcIADYnqgH5NVdVSKvyH5VWY3vMHyhlZQiW23z1a6lZReASYfMMycNfDU2X4EhDOEa0tvUYajpsRlnDIkNcLjxT4KPyrZhl5tVsHECCY0Sasy%2f6zh9ce%2b3HE%2bOEtux%2bEHKfBWrkzwt1vpwyn%2fnXzVd%2bQumpQLw5DOZ2DltHZs%2bfmQ96MoMrBgSx8jS%2bQkR3NQjGAysUOqXK%2fAl38ryHzGe0nSeMkLo5BRYEgiEJK%2bftnZqsEQbZC98E8Fyt2zMGiofGQrR1i5v3gRoOCfqjNYJQAft4ru6GCR5kpm0CsvVvOnKmnA%3d%3d",
    "TransactionResponse": "true",
    "MetaTag": null,
    "MemberUsername": "RT-12345-mytestuser1@gmail.com",
    "MemberProvider": null,
    "IsArnProvider": true,
    "MemberType": "Member"
}
```

### HTTP Request

`POST https://api.travsrv.com/MemberAPI.aspx`

### memberData JSON Object Properties

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
siteid | integer | Yes | Provided by Hotels For Hope
token | string | Yes | Site Admin Token
Points | integer | No | Number of points for the user
Names | string | Yes | Stringified, URI encoded JSON array of JSON object containing the params below
ReferralId | string | Yes | The email address of the user (used as the "username")
FirstName | string | Yes | The user's first name
LastName | string | Yes | The user's last name
Email | string | Yes | The email address of the user
Address1 | string | No | The user's full address
HomePhone | string | No | The user's phone number

## Update an Existing Member

Using the Site Admin's token you may update an existing member by POSTing a *URI encoded* JSON string to this endpoint. Successfully calling this endpoint also generates a new member token for the user in the `CurrentToken` property, which you should save for them if you want to use the "Get a Member by Token" call.

You may notice this call is exactly the same as the "Create a New Member" call.

> The JSON data to stringify and encode may look something like this (not yet encoded):

```json
{
    "Points": 100,
    "Names": [{
        "ReferralId": "mytestuser1@gmail.com",
        "FirstName": "Testme",
        "LastName": "Tester",
        "Email": "mytestuser1@gmail.com",
        "Address1": "123 Main Street",
        "HomePhone": "5551231212"
    }]
}
```

<aside class="notice">
The `Points` attribute is only necessary if you want to update the number of points for the member specified. Please note that it will update the member's points to the value specified, not increment or decrement.
</aside>

<aside class="notice">
The JSON structure includes an array of `Names`, which seems to infer the ability to create more than one person. However, in reality, you should only send this call for one member at a time.
</aside>

<aside class="notice">
`"DeleteMember":true` will deactivate a member. The JSON response will simply show a `MemberId:0` instead of what the `MemberId` once was, but if you try to get that member by it's token, it will respond appropriately that the member no longer exists and/or is deactivated.
</aside>

> Encoded and POSTed via curl:

```shell
curl -X POST \
  https://api.travsrv.com/MemberAPI.aspx \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'siteid={SITEID}&token={ADMIN-TOKEN}&memberData=%7B%22Points%22%3A100%2C%22Names%22%3A%5B%7B%22ReferralId%22%3A%22mytestuser1%40gmail.com%22%2C%22FirstName%22%3A%22Testme%22%2C%22LastName%22%3A%22Tester%22%2C%22Email%22%3A%22mytestuser1%40gmail.com%22%2C%22Address1%22%3A%22123MainStreet%22%2C%22HomePhone%22%3A%225551231212%22%7D%5D%7D'
```

> The above command returns JSON structured like this:

```json
{
    "MemberId": 54321,
    "Rewards": 0,
    "Points": 100,
    "RedemptionMultiplier": 1.0,
    "EarnMultiplier": 1.0,
    "Names": [{
        "FirstName": "Testme",
        "LastName": "Tester",
        "BirthDate": null,
        "Email": "mytestuser1@gmail.com",
        "Address1": "123 Main Street",
        "Address2": null,
        "City": null,
        "State": null,
        "Country": null,
        "Postal": null,
        "Longitude": null,
        "Latitude": null,
        "HomePhone": "5551231212",
        "Referral": null,
        "ReferralId": "mytestuser1@gmail.com",
        "Password": null,
        "IsActive": true,
        "DeleteMember": false,
        "UpdateMemberUsername": false,
        "FullName": "Testme Tester"
    }],
    "DebugData": " Successful Existing Member RT-12345-mytestuser1@gmail.com",
    "Error": null,
    "CurrentToken": "E7MUlbdRdlq2RwSs8V4%2fhza25Xwca%2fZLodi%2faddmPl%2bJfpCU7VovYjoSKaMk34PvkSDpD1mqvezzQG0abXzuXP1%2baaiIKCLw7ehGaiI7BNI7Pb%2fYK%2fGJf4fCxKCz5EodA79iweA6gc2nCEOdWmkarTuy4Cd%2f5WtNkU043rF42sshCKGkg%2bIavKgJ6emdL7msPJRykM2hf%2fmHjdDOV%2b7jtuOHpk5bAVVIc5jhUqmqJMa5908EK0VoX1OUT60SkDcw2YLBeXEg6sYPubiUEmc223Z4JhWVqGuhetKPDE3ddzOLRPyjNgetWddHqoq8Tba%2bKWDcIADYnqgH5NVdVSKvyH5VWY3vMHyhlZQiW23z1a6lZReASYfMMycNfDUhDOEa0tvUYajpsRlnDIkNcLjxT4KPyrZhl5tVsHECCY0Sasy%2f6zh9ce%2b3HE%2bOEtux%2bEHKfBWrkzwt1vpwyn%2fnXzVd%2bQumpQLw5DOZ2DltHZs%2bfmQ96MoMrBgSx8jS%2bQkR3NQjGAysUOqXKn83CdkKJDjeGe0nSeMkLo5BRYEgiEJK%2bftnZqsEQbZC98E8Fyt2zMGiofGQrR1i5v3gRoOCfqjNYJQAft4ru6GCR5kpm0CsvVvOnKmnA%3d%3d",
    "TransactionResponse": "true",
    "MetaTag": null,
    "MemberUsername": "RT-12345-mytestuser1@gmail.com",
    "MemberProvider": null,
    "IsArnProvider": true,
    "MemberType": "Member"
}
```

### HTTP Request

`POST https://api.travsrv.com/MemberAPI.aspx`

### memberData JSON Object Properties

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
siteid | integer | Yes | Provided by Hotels For Hope
token | string | Yes | Site Admin Token
Points | integer | No | Number of points for the user
Names | string | Yes | Stringified, URI encoded JSON array of JSON object containing the params below
ReferralId | string | Yes | The email address of the user (used as the "username")
FirstName | string | Yes | The user's first name
LastName | string | Yes | The user's last name
Email | string | Yes | The email address of the user
Address1 | string | No | The user's full address
HomePhone | string | No | The user's phone number
DeleteMember | boolean | No | Set to `true` to deactivate a member
ReactivateMember | boolean | No | Set to `true` to reactivate a deactivated member


## Get a Member by Token

This endpoint retrieves a member using their member token. Successfully calling this endpoint also generates a new member token for the user in the `CurrentToken` property, which you should save for them if you want to call this endpoint again in the future.

```shell
curl "https://api.travsrv.com/MemberAPI.aspx?\
&siteid={SITEID}\
&token={MEMBER-TOKEN}"
```

> The above command returns JSON structured like this:

```json
{
    "MemberId": 54321,
    "Rewards": 0,
    "Points": 0,
    "RedemptionMultiplier": 1.0,
    "EarnMultiplier": 1.0,
    "Names": [{
        "FirstName": "Testme",
        "LastName": "Tester",
        "BirthDate": null,
        "Email": "mytestuser1@gmail.com",
        "Address1": "123 Main Street",
        "Address2": null,
        "City": null,
        "State": null,
        "Country": null,
        "Postal": null,
        "Longitude": null,
        "Latitude": null,
        "HomePhone": "5551231212",
        "Referral": null,
        "ReferralId": "mytestuser1@gmail.com",
        "Password": null,
        "IsActive": true,
        "DeleteMember": false,
        "UpdateMemberUsername": false,
        "FullName": "Testme Tester"
    }],
    "DebugData": " Successful creation of Member RT-12345-mytestuser1@gmail.com",
    "Error": null,
    "CurrentToken": "E7MUlbdRdlq2RwSs8V4%2fhza25Xwca%2fZLodi%2faddmPl%2bJfpCU7VovYjoSKaMk34PvkSDpD1mqvezzQG0abXzuXP1%2baaiIKCLw7ehGaiI7BNI7Pb%2fYK%2fGJf4fCxKCz5EodA79iweA6gc2nCEOdWmkarTuy4Cd%2f5WtNkU043rF42sshCKGkg%2bIavKgJ6emdL7msPJRykM2hf%2fmHjdDOV%2b7jtuOHpk5bAVVIc5jhUqmqJMa5908EK0VoX1OUT60SkDcw2YLBeXEg6sYPu1Q7mTPc5VUhJ%2b6C6wHM08eOKMrKt6LNRxoB0kXcPyVS1azt1LR48yAegw%2fKXPbdgrCBycjsDedm0ItP9SmW1C6Byw4nt5zivxf%2f0ZIMF07wtZ4JhWVqGuhetKPDE3ddzOLRPyjNgetWddHqoq8Tba%2bKWDcIADYnqgH5NVdVSKvyH5VWYyhlZQiW23z1a6lZReASYfMMycNfDU2X4EhDOEa0tvUYajpsRlnDIkNcLjxT4KPyrZhl5tVsHECCY0Sasy%2f6zh9ce%2b3HE%2bOEtux%2bEHKfBWrkzwt1vpwyn%2fnXzVd%2bQumpQLw5DOZ2DltHZs%2bfmQ96MoMrBgSx8jS%2bQkR3NQjGAysUOqXK%2fAl38ryHzGe0nSeMkLo5BRYEgiEJK%2bftnZqsEQbZC98E8Fyt2zMGiofGQrR1i5v3gRoOCfqjNYJQAft4ru6GCR5kpm0CsvVvOnKmnA%3d%3d",
    "TransactionResponse": "true",
    "MetaTag": null,
    "MemberUsername": "RT-12345-mytestuser1@gmail.com",
    "MemberProvider": null,
    "IsArnProvider": true,
    "MemberType": "Member"
}
```

### HTTP Request

`GET https://api.travsrv.com/MemberAPI.aspx`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
siteid | integer | Yes | Provided by Hotels For Hope
token | string | Yes | Token for the member (not Site Admin's)

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
username={API-USERNAME}\
&password={API-PASSWORD}\
&siteid={SITEID}\
&type=save\
&coupon=%7B%22Code%22%3A%22123-4567890%22%2C%22SiteId%22%3A12345%2C%22Data%22%3A%7B%22IsActive%22%3Atrue%2C%22IsUsed%22%3Afalse%2C%22Discount%22%3A500%2C%22MinNights%22%3A1%2C%22ExpiresOn%22%3A%222018-11-06%22%2C%22MaxUses%22%3A1%2C%22IsPercentage%22%3Afalse%2C%22Terms%22%3A%22%22%7D%7D"
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
username | string | Yes | Provided by Hotels For Hope
password | string | Yes | Provided by Hotels For Hope
siteid | integer | Yes | Provided by Hotels For Hope
type | string | Yes | `save`
coupon | string | Yes | Stringified, URI encoded JSON object containing the params below
Code | string | Yes | The code string you want generated
SiteId | integer | Yes | Provided by Hotels For Hope
Data | object | Yes | JSON object containing the params below
IsActive | boolean | Yes | `true` if not expired and not redeemed
IsUsed | boolean | Yes | `true` if not yet redeemed 
Discount | decimal | Yes | Amount the coupon is worth
MinNights | integer | Yes | Min requirement of nights to be able to use the code
ExpiresOn | date | Yes | Expiration date of this code (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
MaxUses | integer | Yes | Maximum number of times this code may be used
IsPercentage | boolean | Yes | `true` if Discount is a percentage of reservation amount. `false` if Discount is a real amount (1 = 1 USD).
Terms | string | Yes | Set to `""`.


## Get a Coupon/Code

"Coupons" or "Codes" can be used to give users a pre-defined number of "Points" (in API requests/responses). The points (1 point = 1 USD) may be used to discount select purchases within a closed user group.  The codes may either be used during checkout, or easier, added to a user account and automatically applied at checkout for the user for the maximum discount allowed for that transaction.

This endpoint retrieves the data related to a single coupon/code. The response will validate the code is legitimate, whether the code has been used already or not, the expiration date, and the discount (in points) that is available.

<aside class="notice">
Notice the `type=get`, which is the difference between this endpoint call and the call which is used to redeem a code, as noted below.
</aside>

```shell
curl "https://api.travsrv.com/Coupon.aspx?\
username={API-USERNAME}\
&password={API-PASSWORD}\
&siteid={SITEID}\
&type=get\
&couponcode={COUPON-CODE}"
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
username | string | Yes | Provided by Hotels For Hope
password | string | Yes | Provided by Hotels For Hope
siteid | integer | Yes | Provided by Hotels For Hope
type | string | Yes | `get` (in this case), or `redeem` (see below)
couponcode | string | Yes | The code to lookup

## Redeem a Coupon/Code

"Coupons" or "Codes" can be used to give users a pre-defined number of "Points" (in API requests/responses). The points (1 point = 1 USD) may be used to discount select purchases within a closed user group.  The codes may either be used during checkout, or easier, added to a user account and automatically applied at checkout for the user for the maximum discount allowed for that transaction.

This endpoint sets a single coupon/code to `isValid: false`, effectively indicating it's been used and should not be able to be used again. If the code is valid and the call is successfull, the response will look the same as if you were calling a `type=get` (as specified above under "Get a Coupon/Code"). Successive calls to either `type=get` or `type=redeem` will return a response indicating the code is no longer valid.

<aside class="notice">
Notice the `type=redeem`, which is the difference between this endpoint call and the call which is used to simply retrieve the data for a single coupon/code, as noted above.
</aside>

```shell
curl "https://api.travsrv.com/Coupon.aspx?\
username={API-USERNAME}\
&password={API-PASSWORD}\
&siteid={SITEID}\
&type=redeem\
&couponcode={COUPON-CODE}"
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
username | string | Yes | Provided by Hotels For Hope
password | string | Yes | Provided by Hotels For Hope
siteid | integer | Yes | Provided by Hotels For Hope
type | string | Yes | `get` (see above), or `redeem` (in this case)
couponcode | string | Yes | The code to invalidate

# Hotels

## Availability Search

This endpoint retrieves all hotels which have availability for the dates and locations (or individual hotels) specified.

Make this request for the total number of rooms and the total number of guests.  The response will return a maximum of 50 hotels per request, thus you must use pagination techniques if you need more than 50. That said, 50 is the maximum but may not be the best performing. Use smaller batches to get faster responses.

Responses will contain available rate plans and room types from various suppliers we call "gateways".

Responses may contain full nightly rates and tax information, only first night rates with or without tax information, or the highest or average nightly rate.  This response depends on the supplier/gateway but the most common from most gateways is the first night's rate, thus the property name in our responses (`FirstNightRate`).

Rates are always returned in the hotel's native currency.  If you request another `currency`, the correct conversion rate from the hotel's native currency to the desired `DisplayCurrency` will be returned as `DisplayCurrencyMultiplier`. You may use this value to convert the hotel currency to the desired currency for display in your UI. This allows you to show both the original currency and display currency side by side.

<aside class="notice">
We do not advise programming in a gateway-specific manner. Gateways may respond with varying amounts of information at any time. Also, new gateways could be added at any time.
</aside>

<aside class="notice">
If an availability search fails to return rates, we suggest not showing the hotel in your user interface.
</aside>

```shell
curl "https://api.travsrv.com/hotel.aspx?\
username={API-USERNAME}\
&password={API-PASSWORD}\
&siteid={SITEID}\
&latitude=30.099016\
&longitude=-81.601370\
&radius=10\
&inDate=2018-10-20\
&outDate=2018-10-22\
&maxResults=1\
&rooms=1\
&adults=2\
&children=0\
&ipAddress=127.0.0.1\
&userAgent=shell\
&userLanguage=en\
&_type=json"
```

> The above command returns JSON structured like this (edited for brevity):

```json
{
  "ArnResponse": {
    "Info": {
      "@SiteID": "{SITEID}",
      "@Username": "{API-USERNAME}",
      "@IpAddress": "127.0.0.1", 
      "@TimeReceived": "2018-04-13T16:01:13.510", 
      "@TimeCompleted": "2018-04-13T16:01:13.651",
      "@Version": "1.0.0.0",
      "@ServiceUrl": "https://api.travsrv.com/hotel.aspx?inDate=2018-10-20&latitude=30.099016&longitude=-81.601370&maxResults=1&outDate=2018-10-22&password={API-PASSWORD}&radius=10&siteid={SITEID}&username={API-USERNAME}",
      "@RequestID": "436E177E-558F-4287-B55A-5DBD9F4C7579"
    },
    "Availability": {
      "@DisplayCurrency": "USD",
      "HotelAvailability": {
        "@InDate": "2018-10-20",
        "@OutDate": "2018-10-22",
        "@Rooms": "1",
        "@Adults": "2",
        "@Children": "0",
        "Hotel": {
          "@HotelID": "272393",
          "@IsEphemeral": "true",
          "RatePlan": [
            {
              "@Code": "F89648494F22FFE25A254AD1CE7D18FD27B862F1A609BD28872D9CD6DDA2E956B160BE3DB7EB0191B160BE3DB7EB01917EA3048807BEE935",
              "@Description": "Best Available",
              "@BuyerOnly": "false",
              "@Gateway": "41",
              "@CommissionStatus": "Commissionable",
              "@BalanceDueAtHotel": "false",
              "Room": {
                "@Code": "HRLM--_eJwFwcuaczAAANAHmgVRCRaziPRvxkyJadx3biWUfkFH9On_fc5BTlaYBzSSx4m6Iwz3cS_pRnKxCtkQzjqPQZm8Lh771NInUK3ri_pDYTzZL6lQtgl0H0_fOj_f5dRd1kT_pX8dtg_pq0LMTJYHFXNuPqi0PxdLuTjEAeTtKNfYZ3Gd3suIjMbm3_prdXk03gvS_pfpUJnL_poCL9kNoyIlpA2DURM1_fqAtELSKYuKh6e248vaSGk9hE9Dns4MYIncb5jC_fcZG_p_fOeSN3Z0N_fib2UqSpSLCPFgqPX2sQTP9rmXEv_ptXOMVOlVLoC_fujzlUz6tJvvFwUEonyP6njavHdzsVVF2EesNGSmILz3twKMBKm_fp7PK2XCcgV8ghjMc93ZaXrLkm622zmAYaTaPSItlgfYOcO2TSZ6hvwXlxw_fSAVdl9fv4Hwe6AJQ",
                "@Name": "Standard room",
                "@Description": "- 1 King Bed - Nonsmoking Room - Free Breakfast, Free Wifi, Fridge, Microwave",
                "@CurrencyCode": "USD",
                "@DisplayCurrencyMultiplier": "1",
                "@USDMultiplier": "1",
                "@ExchangeGMT": "2018-04-13T11:00:26.790",
                "@MaximumBookable": "99",
                "NightlyRate": [
                  {
                    "@Date": "2018-10-20",
                    "@Price": "114.44"
                  },
                  {
                    "@Date": "2018-10-21",
                    "@Price": "114.43"
                  }
                ],
                "Tax": {
                  "@Percent": "11.51",
                  "@Amount": "29.77"
                },
                "GatewayFee": {
                  "@Amount": "0.00"
                },
                "Total": {
                  "@Amount": "258.64",
                  "@IncludesBookingFee": "false"
                },
                "BookingFee": {
                  "@Amount": "0.00",
                  "@CurrencyCode": "USD",
                  "@DisplayCurrencyMultiplier": "1",
                  "@RoomCurrencyMultiplier": "1",
                  "@ExchangeGMT": "2018-04-13T11:00:26.790"
                }
              }
            }
          ]
        }
      }
    }
  }
}
```

### HTTP Request

`GET https://api.travsrv.com/hotel.aspx`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
username | string | Yes | Provided by Hotels For Hope
password | string | Yes | Provided by Hotels For Hope
siteid | integer | Yes | Provided by Hotels For Hope
timeout | int | No | Maximum time to allow for searching gateways, measured in seconds. Default: 15
maxResults | int | No | Number of results to return. Default: 20. Maximum: 50.
hotelIds | int* | No | See below.
refHotelId | int | No | See below.
latitude | float | No | See below.
longitude | float | No | See below.
radius | float | No | See below.
rooms | int | Yes | Number of rooms needed. When searching for more than one room, responses are based on the same room type and occupancy for every room. Maximum: 9 (best results with no more than 4).
inDate | date | Yes | Desired check-in date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
outDate | date | Yes | Desired check-out date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
adults | int | Yes | Total number of adults. For instance, if `rooms=2&adults=2`, the search is for 1 room per adult. Maximum 8 adults per room. Uneven/odd numbers of adults/rooms will be rounded up to support legacy providers.
children | int | Yes | Total number of children. Maximum: 8. Note: Some legacy providers do not honor the `children` parameter.
sortType | string/enum | No | One of `bestvalue`, `dealpercent`, `dealamount`. Default: `bestvalue`. See below.
currency | string | No | Default: `USD`. See common value map.
name | string | No | Partial hotel name filter. E.g., passing "ilton" would return properties like "Hilton Garden Inn", etc.
propertyClasses | int* | No | See common value map.
propertyAmenities | int* | No | See common value map.
propertyTypes | int* | No | See common value map.
gateway | int* | No | See common value map.
ipAddress | string | Yes | The IPv4 address of the person browsing your website. This is used for fraud checking and preventing booking failures.
userAgent | string | Yes | The userAgent of the app/browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
userLanguage | string | Yes | The language of the browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
locale | string | No | Specifies the response language. Default: "US"
page | int | No | Specifies the results page to return (when more than one page of results is available).
_type | string/enum | No | The response format. One of `xml` or `json`. Default: `json`.

#### `hotelIds`, `locationId`, `refHotelId`, `latitude`+`longitude`+`radius`

One of the following is required:

* `hotelIds`: A list of integers, separated by commas if more than one. Max of 50 hotel IDs may be specified at one time. May be substituted with `refHotelId` or `locationId` or `latitude`+`longitude`+`radius`.
* `refHotelId`: A single hotel ID used to look up the city and return results from that city, as if we had searched by `locationId`. May be substituted with `hotelIds` or `locationId` or `latitude`+`longitude`+`radius`.
* `locationId`: A location ID used to return hotels from within the location's city. May be substituted with `hotelIds` or `refHotelId` or `latitude`+`longitude`+`radius`.
* `latitude` + `longitude` + `radius` (Do not send `radius` if doing `latitude`/`longitude` based deal search)
** `radius`: Measured in miles.  NOTE: If doing a market deal search, leave off radius and just pass `latitude` and `longitude`.

#### `sortType`

Sort Type | Description
--------- | -------
`bestvalue` | The default sort type, based on previous booking trends and manual sorting options.
`dealpercent` | Sorts the hotel results based on prices last seen and returns the best percentage savings we have found historically for the specified dates.
`dealamount` | Sorts the hotel results based on prices last seen and returns the best amount savings we have found historically and for those dates.

## Hotel Detail

This call confirms availability with the supplier / gateway (requests to skip any caching they have in place) and retrieves cancellation and booking policies to display prior to the user placing a reservation.

This call is only available for a single hotel ID, room code, and rate code.

Responses will contain nightly rates, taxes and fees associated with the room, and hotel, payment, and cancellation policies which apply to the rate.

This request is rate limited as it is an expensive request to make. Responses with a 429 status code are in response to over use, should you exceed the rate limit. 

Failed responses indicate the rate is sold out. Subsequent availability calls will flush and re-cache this hotel's rates.

**All fees, penalties, and policies from this response must be shown to the user before creating a reservation.**

All room prices are based on the number of adults per room specified in the request.  A response containing an extra adult fee of `0` may simply mean the pricing is not available. Adding more than the specified number of adults to the room because the extra adult fee is `0` will likely incur a price difference when the guest arrives at the hotel. To avoid this, we advise not depend on the extra adult fee specified in the response when it comes to pricing.


```shell
curl "https://api.travsrv.com/hotel.aspx?\
username={API-USERNAME}\
&password={API-PASSWORD}\
&siteid={SITEID}\
&hotelIds=272393\
&inDate=2018-10-20\
&outDate=2018-10-22\
&maxResults=1\
&rooms=1\
&adults=2\
&children=0\
&gateway=51\
&ratePlanCode=F89648494F22FFE25A254AD1CE7D18FD27B862F1A609BD28872D9CD6DDA2E956B160BE3DB7EB0191B160BE3DB7EB01917EA3048807BEE935\
&roomCode=HRLM--_eJwFwcuaczAAANAHmgVRCRaziPRvxkyJadx3biWUfkFH9On_fc5BTlaYBzSSx4m6Iwz3cS_pRnKxCtkQzjqPQZm8Lh771NInUK3ri_pDYTzZL6lQtgl0H0_fOj_f5dRd1kT_pX8dtg_pq0LMTJYHFXNuPqi0PxdLuTjEAeTtKNfYZ3Gd3suIjMbm3_prdXk03gvS_pfpUJnL_poCL9kNoyIlpA2DURM1_fqAtELSKYuKh6e248vaSGk9hE9Dns4MYIncb5jC_fcZG_p_fOeSN3Z0N_fib2UqSpSLCPFgqPX2sQTP9rmXEv_ptXOMVOlVLoC_fujzlUz6tJvvFwUEonyP6njavHdzsVVF2EesNGSmILz3twKMBKm_fp7PK2XCcgV8ghjMc93ZaXrLkm622zmAYaTaPSItlgfYOcO2TSZ6hvwXlxw_fSAVdl9fv4Hwe6AJQ\
&ipAddress=127.0.0.1\
&userAgent=shell\
&userLanguage=en\
&_type=json"
```

> The above command returns JSON structured like this (edited for brevity):

```json
{
  "ArnResponse": {
    "Info": {
      "@SiteID": "{SITEID}",
      "@Username": "{API-USERNAME}",
      "@IpAddress": "24.113.225.28",
      "@TimeReceived": "2018-04-17T00:41:27.367",
      "@TimeCompleted": "2018-04-17T00:41:27.804",
      "@Version": "1.0.0.0",
      "@ServiceUrl": "http://api.travsrv.com/hotel.aspx?_type=json&adults=2&children=0&gateway=51&hotelIds=272393&inDate=2018-10-20&ipAddress=127.0.0.1&maxResults=1&outDate=2018-10-22&password={API-PASSWORD}&ratePlanCode=&roomCode=HRLM--_eJwFwcuaczAAANAHmgVRCRaziPRvxkyJadx3biWUfkFH9On_fc5BTlaYBzSSx4m6Iwz3cS_pRnKxCtkQzjqPQZm8Lh771NInUK3ri_pDYTzZL6lQtgl0H0_fOj_f5dRd1kT_pX8dtg_pq0LMTJYHFXNuPqi0PxdLuTjEAeTtKNfYZ3Gd3suIjMbm3_prdXk03gvS_pfpUJnL_poCL9kNoyIlpA2DURM1_fqAtELSKYuKh6e248vaSGk9hE9Dns4MYIncb5jC_fcZG_p_fOeSN3Z0N_fib2UqSpSLCPFgqPX2sQTP9rmXEv_ptXOMVOlVLoC_fujzlUz6tJvvFwUEonyP6njavHdzsVVF2EesNGSmILz3twKMBKm_fp7PK2XCcgV8ghjMc93ZaXrLkm622zmAYaTaPSItlgfYOcO2TSZ6hvwXlxw_fSAVdl9fv4Hwe6AJQ&rooms=1&siteid={SITEID}&userAgent=shell&userLanguage=en&username={API-USERNAME}",
      "@RequestID": "2999AB6A-6DB9-4FFF-9586-BBED51BB6108"
    },
    "Availability": {
      "@DisplayCurrency": "USD",
      "HotelAvailability": {
        "@InDate": "2018-10-20",
        "@OutDate": "2018-10-22",
        "@Rooms": "1",
        "@Adults": "2",
        "@Children": "0",
        "Hotel": {
          "@HotelID": "272393",
          "@IsEphemeral": "true",
          "RatePlan": [
            {
              "@Code": "F89648494F22FFE25A254AD1CE7D18FD27B862F1A609BD28872D9CD6DDA2E956B160BE3DB7EB0191B160BE3DB7EB01917EA3048807BEE935",
              "@Description": "Best Available",
              "@BuyerOnly": "false",
              "@Gateway": "41",
              "@CommissionStatus": "Commissionable",
              "@BalanceDueAtHotel": "false",
              "Room": {
                "@Code": "",
                "@Name": "Standard room",
                "@Description": "- 1 King Bed - Nonsmoking Room - Free Breakfast, Free Wifi, Fridge, Microwave",
                "@CurrencyCode": "USD",
                "@DisplayCurrencyMultiplier": "1",
                "@USDMultiplier": "1",
                "@ExchangeGMT": "2018-04-17T00:00:06.027",
                "@MaximumBookable": "99",
                "NightlyRate": [
                  {
                    "@Date": "2018-10-20",
                    "@Price": "114.44"
                  },
                  {
                    "@Date": "2018-10-21",
                    "@Price": "114.43"
                  }
                ],
                "Tax": {
                  "@Percent": "11.51",
                  "@Amount": "29.77"
                },
                "GatewayFee": {
                  "@Amount": "0.00"
                },
                "Total": {
                  "@Amount": "258.64",
                  "@IncludesBookingFee": "false"
                },
                "BookingFee": {
                  "@Amount": "0.00",
                  "@CurrencyCode": "USD",
                  "@DisplayCurrencyMultiplier": "1",
                  "@RoomCurrencyMultiplier": "1",
                  "@ExchangeGMT": "2018-04-17T00:00:06.027"
                }
              }
            }
          ]
        }
      }
    }
  }
}
```

### HTTP Request

`GET https://api.travsrv.com/hotel.aspx`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
username | string | Yes | Provided by Hotels For Hope
password | string | Yes | Provided by Hotels For Hope
siteid | integer | Yes | Provided by Hotels For Hope
timeout | int | No | Maximum time to allow for searching gateways, measured in seconds. Default: 15
hotelIds | int | No | The particular hotel id for which more detail is being requested.
rooms | int | Yes | Number of rooms needed. When searching for more than one room, responses are based on the same room type and occupancy for every room. Maximum: 9 (best results with no more than 4).
inDate | date | Yes | Desired check-in date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
outDate | date | Yes | Desired check-out date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
adults | int | Yes | Total number of adults. For instance, if `rooms=2&adults=2`, the search is for 1 room per adult. Maximum 8 adults per room. Uneven/odd numbers of adults/rooms will be rounded up to support legacy providers.
children | int | Yes | Total number of children. Maximum: 8. Note: Some legacy providers do not honor the `children` parameter.
currency | string | No | Default: `USD`. See common value map.
ratePlanCode | string | Yes | See common value map.
roomCode | string | Yes | See common value map.
gateway | int | No | See common value map.
ipAddress | string | Yes | The IPv4 address of the person browsing your website. This is used for fraud checking and preventing booking failures.
userAgent | string | Yes | The userAgent of the app/browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
userLanguage | string | Yes | The language of the browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
locale | string | No | Specifies the response language. Default: "US"
_type | string/enum | No | The response format. One of `xml` or `json`. Default: `json`.

## Hotel Reservation Creation

Generally speaking this call should be self explanatory. The parameters you will be sending in regarding the fees and costs will come from the detail request you likely would have just made. This is used to double confirm the costs the user was given will match up with the costs in the suppliers / gateways.

```shell
curl -X POST "https://api.travsrv.com/hotel.aspx?\
username={API-USERNAME}\
&password={API-PASSWORD}\
&siteid={SITEID}\
&rooms=1\
&hotelIds=10731\
&rooms=1\
&inDate=2007-03-30\
&outDate=2007-03-31\
&adults=2\
&children=1\
&ratePlanCode=AAA\
&roomCode=Z303AAA\
&guestFirstName=Eddie\
&guestLastName=Collins\
&guestEmail=nobody@yahoo.com\
&guestPhoneCountry=1\
&guestPhoneArea=313\
&guestPhoneNumber=5555555\
&guestMessage=Smoking room requested.\
&addressAddress=123 main st\
&addressCity=detroit\
&addressRegion=MI\
&addressPostalCode=48234\
&addressCountryCode=US\
&roomCostPrice=98.95\
&roomCostTaxAmount=0.00\
&roomCostGatewayFee=0.00\
&roomCostTotalAmount=103.95\
&roomCostCurrencyCode=USD\
&bookingFeeAmount=5.00\
&creditCardType=VISA\
&creditCardNumber=4242424242424242\
&creditCardExpiration=2018-12\
&creditCardCVV2=123\
&creditCardHolder=Eddie Collins\
&creditCardCity=Detroit\
&creditCardRegion=MI\
&creditCardPostalCode=48234\
&creditCardCountryCode=US\
&ipAddress=127.0.0.1\
&userAgent=shell\
&userLanguage=en\
&_type=json"
```

> The above command returns JSON structured like this (edited for brevity):

```json
{
  "ArnResponse": {
    "Info": {
      "@SiteID": "{SITEID}",
      "@Username": "{API-USERNAME}",
      "@IpAddress": "127.0.0.1",
      "@TimeReceived": "2007-03-30T22:14:28.484",
      "@TimeCompleted": "2007-03-30T22:14:32.046",
      "@Version": "1.0.0.0",
      "@ServiceUrl": "https://api.travsrv.com/hotel.aspx",
      "@RequestID": "D392A38B-79EC-4064-9C8F-E2C9AFC2EEE6"
    },
    "Reservation": {
      "@DisplayCurrency": "USD",
      "@ItineraryID": "678595",
      "@RecordLocator": "4fa67dc1-9d40-46f4-aa34-eb236117781c",
      "HotelReservation": {
        "@InDate": "2007-03-30",
        "@OutDate": "2007-03-31",
        "@Rooms": "1",
        "@Adults": "2",
        "@Children": "0",
        "@ReservationID": "860964",
        "@CustomerConfirmationNumber": "40156457",
        "Hotel": {
          "@HotelID": "10731",
          "RatePlan": {
            "@Code": "AAA",
            "@Description": "QUALIFYING MEMBER RATE: Aaa/CAA Rate 1 King Bed /1 Room Suite/Partial Room Divider /Microwave Refrigerator/Computer Hookup Guest Must Show Some Form Of Aaa Membership Rate Is Applicable To AAA Members Only And Only On Rooms They Stay In Themselv",
            "@Gateway": "4",
            "Room": {
              "@Code": "Z303AAA",
              "@Name": "Room",
              "@Description": "QUALIFYING MEMBER RATE: Aaa/CAA Rate 1 King Bed /1 Room Suite/Partial Room Divider /Microwave Refrigerator/Computer Hookup Guest Must Show Some Form Of Aaa Membership Rate Is Applicable To AAA Members Only And Only On Rooms They Stay In Themselv",
              "@CurrencyCode": "USD",
              "@DisplayCurrencyMultiplier": "1",
              "@USDMultiplier": "1",
              "@ExchangeGMT": "2007-03-30T17:15:04.627",
              "@MaximumBookable": "1",
              "NightlyRate": {
                "@Date": "2007-03-30",
                "@Price": "98.95"
              },
              "Tax": {
                "@Percent": "0.00",
                "@Amount": "0.00"
              },
              "GatewayFee": {
                "@Amount": "0.00"
              },
              "Total": {
                "@Amount": "98.95",
                "@IncludesBookingFee": "false"
              },
              "BookingFee": {
                "@Amount": "5.00",
                "@CurrencyCode": "USD",
                "@DisplayCurrencyMultiplier": "1",
                "@RoomCurrencyMultiplier": "1",
                "@ExchangeGMT": "2007-03-30T17:15:04.627"
              }
            },
            "Policy": {
              "ExtraPersonPrice": {
                "@Adult": "5.00",
                "@Child": "0.00",
                "@CurrencyCode": "USD",
                "@DisplayCurrencyMultiplier": "1",
                "@USDMultiplier": "1",
                "@ExchangeGMT": "2007-03-30T17:15:04.627"
              },
              "Guarantee": {
                "@Description": "RESERVATION WILL BE HELD TILL 4PM LOCAL TIME Booking fee is not included in the total and it's value is expressed in United States Dollars. Booking fee will be charged at the time of the booking."
              },
              "Cancel": {
                "@Description": "CANCEL BY 4 PM LOCAL HTL TIME DOA",
                "@LatestCancelTime": "2007-03-29T10:00:00.000",
                "@GMTOffSet": "0",
                "Fee": {
                  "@Amount": "0.00",
                  "@CurrencyCode": "USD",
                  "@DisplayCurrencyMultiplier": "1",
                  "@RoomCurrencyMultiplier": "1",
                  "@ExchangeGMT": "2007-03-30T17:15:04.627"
                },
                "Penalty": {
                  "@Amount": "98.95",
                  "@CurrencyCode": "USD",
                  "@DisplayCurrencyMultiplier": "1",
                  "@USDMultiplier": "1",
                  "@ExchangeGMT": "2007-03-30T17:15:04.627"
                }
              },
              "Deposit": {
                "@Description": "None"
              },
              "Payment": [
                {
                  "@Description": "Tax is not included in the total."
                },
                {
                  "@Description": "With your credit card information, the room(s) you book are guaranteed for late arrival."
                },
                {
                  "@Description": "This discount rate requires a $5.00 (USD) per room per night non-refundable service fee at time of reservation and will appear on your credit card under Alliance Reservations Network, Phoenix, AZ."
                }
              ],
              "Property": [
                {
                  "@Description": "Check-In Time",
                  "@Value": "150000"
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
            "@FirstName": "Eddie",
            "@MiddleName": "",
            "@LastName": "Collins",
            "@Message": "Smoking room requested.",
            "@Email": "nobody@yahoo.com",
            "@PhoneCountry": "1",
            "@PhoneArea": "313",
            "@PhoneNumber": "5555555",
            "@PhoneExtension": "",
            "@AgeGroup": "Adult",
            "Address": {
              "@Address": "123 main st",
              "@City": "detroit",
              "@Region": "MI",
              "@PostalCode": "48234",
              "@CountryCode": "US",
              "@ExtraInfo": ""
            }
          }
        },
        "Service": {
          "@ExchangeGMT": "2007-03-30T17:15:04.627",
          "RoomCurrency": {
            "@CurrencyCode": "USD",
            "Cost": {
              "@Price": "98.95",
              "@TaxPercent": "0.00",
              "@TaxAmount": "0.00",
              "@GatewayFee": "0.00",
              "@BookingFee": "5.00",
              "@TotalAmount": "103.95",
              "@TotalAmountIncludesBookingFee": "true"
            },
            "Charge": {
              "@Paid": "5.00",
              "@Due": "98.95"
            }
          },
          "DisplayCurrency": {
            "@CurrencyCode": "USD",
            "Cost": {
              "@Price": "98.95",
              "@TaxPercent": "0.00",
              "@TaxAmount": "0.00",
              "@GatewayFee": "0.00",
              "@BookingFee": "5.00",
              "@TotalAmount": "103.95",
              "@TotalAmountIncludesBookingFee": "true"
            },
            "Charge": {
              "@Paid": "5.00",
              "@Due": "98.95"
            }
          },
          "USD": {
            "@CurrencyCode": "USD",
            "Cost": {
              "@Price": "98.95",
              "@TaxPercent": "0.00",
              "@TaxAmount": "0.00",
              "@GatewayFee": "0.00",
              "@BookingFee": "5.00",
              "@TotalAmount": "103.95",
              "@TotalAmountIncludesBookingFee": "true"
            },
            "Charge": {
              "@Paid": "5.00",
              "@Due": "98.95"
            }
          }
        }
      }
    }
  }
}
```

### HTTP Request

`POST https://api.travsrv.com/hotel.aspx?type=Reservation`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
username | string | Yes | Provided by Hotels For Hope
password | string | Yes | Provided by Hotels For Hope
siteid | integer | Yes | Provided by Hotels For Hope
hotelIds | int | Yes | The particular hotel id to reserve the room at.
agentRefNumber | string | No | A reference ID you may use for your own tracking purposes. This is included in a reservation webhook, if used.
rooms | int | Yes | Number of rooms needed. Maximum: 9.
inDate | date | Yes | Desired check-in date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
outDate | date | Yes | Desired check-out date (format: `YYYY-MM-DD` based on UTC -7 (MST) time zone)
adults | int | Yes | Total number of adults. For instance, if `rooms=2&adults=2`, the search is for 1 room per adult. Maximum 8 adults per room. Uneven/odd numbers of adults/rooms will be rounded up to support legacy providers.
children | int | Yes | Total number of children. Maximum: 8. Note: Some legacy providers do not honor the `children` parameter.
currency | string | No | Default: `USD`. See common value map.
ratePlanCode | string | Yes | See common value map.
roomCode | string | Yes | See common value map.
gateway | int | yes | See common value map.
campaignCode | string | No | See below.
guestTitle | string | No | Primary guest's title (e.g., "Mr.", "Mrs.", etc.)
guestFirstName | string | Yes | Primary guest's first name
guestLastName | string | Yes | Primary guest's last name.
guestEmail | string | Yes | Primary guest's email address.
guestPhoneCountry | string | Yes | Primary guest's phone number country code.
guestPhoneArea | string | Yes | Primary guest's phone number area code. 
guestPhoneNumber | string | Yes | Primary guest's phone number (without country or area code)
guestPhoneExtension | string | No | Primary guest's phone number extension.
guestMessage | string | No | Guest special requests.
addressAddress | string | Yes | Primary guest's address.
addressCity | string | Yes | Primary guest's city.
addressRegion | string | Yes | Primary guest's state / region.
addressPostalCode | string | Yes | Primary guest's postal code.
addressCountryCode | string | Yes | Primary guest's country code.
roomCostPrice | decimal | Yes | See below.
roomCostTaxAmount | decimal | Yes | See below.
roomCostGatewayFee | decimal | Yes | See below.
roomCostTotalAmount | decimal | Yes | See below.
roomCostCurrencyCode | string | Yes | See below.
bookingFeeAmount | decimal | Yes | See below.
creditCardType | string | Yes | Credit card type ("AMEX", "MasterCard", "VISA", etc.)
creditCardNumber | string | Yes | Credit card number.
creditCardExpiration | string | Yes | Credit card expiration date (format: `YYYY-MM`)
creditCardCVV2 | int | Yes | Credit card CVV2 number.
creditCardHolder | string | Yes | Name on credit card.
creditCardAddress | string | Yes | Credit card billing address.
creditCardCity | string | Yes | Credit card billing city.
creditCardRegion | string | Yes | Credit card billing state / region.
creditCardPostalCode | string | Yes | Credit card billing postal code.
creditCardCountryCode | string | Yes | Credit card billing country code.
ipAddress | string | Yes | The IPv4 address of the person browsing your website. This is used for fraud checking and preventing booking failures.
userAgent | string | Yes | The userAgent of the app/browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
userLanguage | string | Yes | The language of the browser of the person browsing your website. This is used for fraud checking and preventing booking failures.
locale | string | No | Specifies the response language. Default: "US"
_type | string/enum | No | The response format. One of `xml` or `json`. Default: `json`.

#### `campaignCode`

You may pass in a string which you want to persist with the reservation.  This is analagous to a "subid" and can be used for reconciling with your own marketing campaigns, or really anything else you want to do with it.  The string you provide in this parameter will be added to the reservation being made and available in available reporting.

#### `roomCostPrice`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

#### `roomCostTaxAmount`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

#### `roomCostGatewayFee`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

#### `roomCostTotalAmount`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

#### `roomCostCurrencyCode`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

#### `bookingFeeAmount`

Send the exact same information received from the Hotel Detail Request (assuming the same `currency` designation in both requests. This is used to assure the expected reservation amounts match the actual prices the hotel has given.

## Hotel Reservation Cancellation

To cancel a reservation you will need the `reservationId` and `itineraryId` returned in the reservation creation response.

```shell
curl -X POST "https://api.travsrv.com/hotel.aspx?\
username={API-USERNAME}\
&password={API-PASSWORD}\
&siteid={SITEID}\
&reservationId=915892\
&itineraryId=733525\
&ipAddress=127.0.0.1\
&userAgent=shell\
&userLanguage=en\
&_type=json"
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
            "@Code": "ARN",
            "@Description": "Internet Special",
            "@Gateway": "1",
            "Room": {
              "@Code": "3979",
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
username | string | Yes | Provided by Hotels For Hope
password | string | Yes | Provided by Hotels For Hope
siteid | integer | Yes | Provided by Hotels For Hope
reservationId | string | Yes | The `reservationId` from the reservation creation response.
itineraryId | string | Yes | The `itineraryId` from the reservation creation response.
_type | string/enum | No | The response format. One of `xml` or `json`. Default: `json`.
