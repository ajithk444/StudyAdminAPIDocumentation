Study Admin API
===============

Overview
-------------------
The Study Admin API was developed to provide other software systems a web interface to the study admin web portal. The api provides access to the same core study and de-identified subject data that can be accessed within [Study Admin](http://studyadmin.actigraphcorp.com).

Enabling API Access
-------------------
Please contact [Actigraph](http://www.actigraphcorp.com/support/contact-support/) for more information.

Technical Overview
-------------------

###Json###

This is a JSON API. When sending Http requests you must supply the Content-Type field within the header as  “application/json” on PUT and POST operations. If an error occurs, you may receive a text/plain response, e.g. a 400 bad   request response indicates you will need to take action.

###Date Formatting - UTC###
 * All dates will adhere to ISO 1806 and will be in UTC. So when sending Http requests you must supply the Date field within the HTTP header in UTC format.
 * When the trailing 'Z' is withheld it will signify that the date should be interpreted in the subject's timezone.

###Authentication###

 Refer to the [Authentication](https://github.com/actigraph/StudyAdminAPIDocumentation/blob/master/sections/authentication.md) section for specifics and examples on request signing.

###HTTPS###

Any non-HTTPS request will result in a Forbidden response.

###Resource Links###
* [HTTPS](http://tools.ietf.org/html/rfc2818) 
* [JSON](http://tools.ietf.org/html/rfc4627)
* [HMAC](http://tools.ietf.org/html/rfc2104) [SHA256](http://tools.ietf.org/html/rfc4634)
* [ISO 8601](http://www.w3.org/TR/NOTE-datetime)

Standard Response Format
---------
All responses include a standard HTTP status code and most of them have additional information for confirming actions or explaining errors.  In this section we provide example status codes and responses to illustrate our standard response format.

For successful requests, the status code within response will be within the 200 range.  After successfully creating a subject through the ***POST /v1/subjects*** endpoint, the resulting json will include the subject Id of the newly created subject, e.g:

**Request** 

	POST  https://studyadmin-api.actigraphcorp.com/v1/subjects
	{
	  "Gender": "Male",
	  "SiteID": "33",
	  "SubjectIdentifier": "000008",
	  "WearPosition": "Left Wrist",
	  "WeightLbs": "185.00",
	  "DOB": "1975-10-06"
	}


**Response**

	Status: 201 Created
	{
	   "SubjectId": "123" 
	}

After successfully editing a subject through the ***PUT /v1/subjects*** endpoint, the status code within the response will denote 200 OK. After successfully retrieving data on any subject, site, or study endpoints the status code within response should also denote 200 OK.

For unsuccessful requests, the status code within response will be within the 400 range which may indicate an action required by API user. These responses may contain error messages in plain text, e.g:

###Example 1###

**Request** 

	GET  https://studyadmin-api.actigraphcorp.com/v1/subjects/-154/stats

**Response**
	
	Status: 400 BadRequest
	Subject Id is invalid

###Example 2###

**Request** 

	PUT  https://studyadmin-api.actigraphcorp.com/v1/subjects
	
	  "SubjectId": "594",
	  "Gender": "Male 
	  "SiteID": "33",
	  "SubjectIdentifier": "000055",
	  "WearPosition": "Left Wrist",
	  "WeightLbs   "185.00",
	  "DOB": "1975-10-06"
	}

**Response**
	
	Status 400 BadRequest
	Json request not well-formed



Endpoints
---------
* [Studies](sections/studies.md) Logical structures for grouping data for one or more subjects.
* [Sites](sections/sites.md) Physical/geographical locations within studies.
* [Subjects](sections/subjects.md) Participants in studies.
* [Uploads](sections/Uploads.md) Retrieve and create upload.
* [Webhooks](sections/webhooks.md) Retrieve history of webhooks.


Request Limiting
---------
This API is request limited. We only allow a certain number of requests per day. Please contact [Actigraph](http://www.actigraphcorp.com/support/contact-support/) for more information.
