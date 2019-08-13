# Handling Exceptions and error codes

## How to generate custom exceptions and map to correct response codes in Rest
```bash
no need to maintain any status string in response / success and failure will be handled through status codes
	-	200 = executed without exception and non null data returned 
	-	for any other scenario raise custom exception and populate the exception message with reasonCode and reasonDesc
	-- 	in case of anything other than 200 status code other http error codes will be populated. also the reason from exception msg will be populated 
	-- 	so in case of other than 200 http code scenarios , api consumer should look into the reasoncode and reasonDesc
	e.g.... In case of database connection exception -
			http response code will be 500 - internal server error and reason Object will be {reasonCode : "DBConnectError" , reasonDesc : "error in connectin database"}
			In case of null data return from GenericPatientSearch - 
			http response code will be 400 and reason Object will be {reasonCode : "DataNotFound" , reasonDesc:"search returned no data , please provide valid data"}
```

## Http Responses -

```bash
for Data Errors
400 for when the requested information is incomplete or malformed.
422 for when the requested information is okay, but invalid.
404 for when everything is okay, but the resource doesn’t exist.
409 for when a conflict of data exists, even with valid information.
for Auth Errors
401 for when an access token isn’t provided, or is invalid.
403 for when an access token is valid, but requires more  privileges.
for Standard Statuses
200 for when everything is okay.
204 for when everything is okay, but there’s no content to return.
500 for when the server throws an error, completely unexpected.
```
maintain a key value pair for {key : "reasonCodes" , value : "http codes"} and a constants file for reasonCodes.

reference -
[rest api design] (https://medium.com/studioarmix/learn-restful-api-design-ideals-c5ec915a430f)
