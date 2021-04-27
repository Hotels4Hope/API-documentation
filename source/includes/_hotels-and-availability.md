# Hotels and availability

## Workflow overview

### Creating a reservation

This is the typical workflow for creating a reservation. Each step contains information you will need to create the reservation. These steps exist by design to reduce fraud.

1. Get available inventory using an [Availability Search](#availability-search)
2. [Get inventory details](#hotel-detail)
3. [Create a Reservation](#hotel-reservation-creation) based on details

### Creating a reservation using a hold

[Inventory on hold](#inventory-on-hold) is only useful only for that inventory which is RFP'd and contracted using our Groups application.  It does not pertain to GDS, OTA, or any other type of inventory other than that which you contract and load into the Groups app.

Once contracted inventory is added into the Groups app it becomes available in the API through an Availability Search using the parameter `​gateway=16​`.

1. Add contracted inventory to the Groups app (RFP and accept a bid). _This is a pre-requisite manual step. All other steps can be done with this API._
2. Get available inventory using an [Availability Search](#availability-search) using `gateway=16` (to select from contracted inventory only)
3. [Create a Hold](#create-a-hold) based on search results
4. [Get inventory details](#hotel-detail) using `gateway=20` (to select from held inventory only)
5. [Create a Reservation](#hotel-reservation-creation) based on details using `gateway=20` (to book against held inventory only)

Optionally, you may want to be able to [cancel/expire a Hold](#cancel-hold) and/or [cancel a Reservation](#cancel-reservation).

### Common terms in this section

* **`RoomTypeId` = `RoomCode`**: The ID associated with a room type (as seen in Hold responses and Detail request params).
* **`RatePlanCode`**: "ARN" + `RoomTypeId` (string concatenation) (as seen when creating a Reservation and Detail request params)
* **`HotelId` = `PropertyId`**: These terms are synonmous (as seen in Availability Search responses, Detail responses, and used in a comma separated value list for the `hotelids` parameter value in a Detail request). You may also use these values to look up more details on an individual property using the Property Detail call.

When creating a reservation, use this mapping to find the appropriate values to use for these required parameters:

<aside class="notice">
    All values are based on the Detail response and have a starting point of `ArnResponse.RateDetails.HotelRateDetails.Hotel.RatePlan.Room`
</aside>

* **`roomCostCurrencyCode`**: `@CurrencyCode`
* **`roomCostPrice`**: `NightlyRate@Price`
* **`roomCostTaxAmount`**: `Tax@Amount`
* **`roomCostGatewayFee`**: `GatewayFee@Amount`
* **`roomCostTotalAmount`**: `Total@Amount`
* **`bookingFeeCurrencyCode`**: `BookingFee@CurrencyCode`
* **`bookingFeeAmount`**: `BookingFee@Amount`
