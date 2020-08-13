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

## `roomCode` / `roomTypeId`

This is the `ArnResponse.Availability.HotelAvailability.Hotel.RatePlan.Room@Code` value specified in the Availability Search results for the room type you are interested.

The terms `roomCode` and `roomTypeId` are synonymous.

## `ratePlanCode`

This is the `ArnResponse.Availability.HotelAvailability.Hotel.RatePlan@Code` value specified in the Availability Search results for the rate plan you are interested in.  It's simply the `roomCode` / `roomTypeId` with a prefixed "ARN" string in front of it.

## `HotelId` / `PropertyID`

These two terms and their values are synonymous.  You may use the values of these properties in a resulting `hotelids` parameter (comma-delimited).
