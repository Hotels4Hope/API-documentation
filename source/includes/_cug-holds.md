# Inventory on hold

This section is only for those using the SSO Authentication feature and pertains to managing contracted inventory, specifically that which has been placed "on hold".

You will need a Site Admin user in your closed user group site. If you don't already have one, please [request one](mailto:hello@quintrooms.com?Subject=Request%20for%20Site%20Admin%20User) be added for your portal/site.

To book a reservation for any held room type, simply use the `roomTypeId` identfier when creating a reservation.

<aside class="warning">
Please note the Authentication method for these calls is not consistent with other calls. For these calls, all calls must include a basic authentication header using the username (email address) and password of an authorized user for the `siteId` you are querying.

Ref: https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication

Simply put, include a header in your requests using the base 64 encoded string of the user's email address and password like so: `-H 'Authorization: Basic {BASE64-ENCODED-STRING}'`.
</aside>

<aside class="warning">
Just as the authentication for this set of endpoints is different, please note that the endpoint domain is also different.

`https://groups.alliancereservations.com/services/external` is the base path for this set of endpoints.
</aside>
