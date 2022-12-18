# Errors

The Emmi API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
404 | Not Found -- The specified fund could not be found.
422 | Unprocessible Entity -- There was an issue processing the fund request - for example an ISIN could not be found
500 | Internal Server Error -- We had a problem with our server. Try again later.
