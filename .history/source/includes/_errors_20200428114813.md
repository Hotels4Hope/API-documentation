# Errors
The Hotels for Hope API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API credentials are wrong.
403 | Forbidden -- You are not allowed in there.
404 | Not Found -- The specified hotel or endpoint could not be found.
405 | Method Not Allowed -- You tried to access an endpoint with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json or xml.
410 | Gone -- The hotel requested has been removed from our servers.
418 | I'm a teapot.
429 | Too Many Requests -- You are sending requests too often! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
