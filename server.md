# Our Test Server

The test server we will be using for this exercise is located [here](http://fhirtest.uhn.ca/). It contains a bunch of test healthcare data put there by various people testing thier FHIR applications. Just as a warning though, this is not a production server, so any data stored on it could be wiped at any time. Do not depend on this server for permanent storage, and keep in mind that someone else could modify or delete your data without warning.

On the left side of the page, you will see a list of the various FHIR resources stored on the server. For our demo application, we are concerned with the [Patient](http://fhirtest.uhn.ca/resource?serverId=home_21&pretty=false&resource=Patient) link.

On the patient page, hit the 'Search' button. The page will reload, and you will see a whole bunch of information.

## Searching

### Request

![alt text][request]

This just outlines the REST request being made to the FHIR server to fetch the patient information. You don't even need the web browser to test this. Go ahead a give it a try on the command line.
```
curl "http://fhirtest.uhn.ca/baseDstu3/Patient?_pretty=true"
```
You should get a very similar JSON response to what is displayed on the website.

### Response

![alt text][response]

The response field lets us know the response to our request, in this case a HTTP 200 OK, and a little bit about the server itself.

### Response Body

![alt text][body]

As you can see in the above screen shot, the last section of the output is the response body. You'll see a list of [patients](https://www.hl7.org/fhir/patient.html) with links to explore further. 

There are two key takeaways from the response you need to note:

1. The request doesn't return a straight array of patient entries, it returns the patients in this FHIR structure known as a [Bundle](https://www.hl7.org/fhir/bundle.html). The structure of the bundle and how the entries are stored is outlined in the verbose JSON output at the bottom of the response body section.
2. Although the id of the patient in FHIR is a long, stored as a String, the webpage displays the full qualified id. So you will see the id column contains the type, id, and history values as well:
```
Patient/191021/_history/6
Patient/20195/_history/2
```
So when curl-ing the server directly for a specific resource, you can use:
```
curl "http://fhirtest.uhn.ca/baseDstu3/Patient/191025/_history/6" 
```
...for the specific historical version, or:
```
curl "http://fhirtest.uhn.ca/baseDstu3/Patient/191025/"
```
...for the latest version, regardless of how many updates have been made.

[request]: request.png
[response]: response.png
[body]: body.png
