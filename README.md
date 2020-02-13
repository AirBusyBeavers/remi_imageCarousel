# Getting start with the image carousel:

1) npm run seed
2) npm run build
3) npm run start

# CRUD API

API Documentation
______________________________________________________________________
GET /gallery
- BEHAVIOR
  - retrieves all stored galleries in the database
- INPUT PARAMETERS
  - none
- OUTPUT
  - an array of objects representing galleries
  - returns an empty array if no galleries are in the database

Example command to pull all the galeries:
```terminal
curl -X GET http://localhost:3000/gallery/
```

Example output:
```javascript
[{...},
{...},
{...},
]
```
______________________________________________________________________
GET /gallery/:id
- BEHAVIOR
  - retrieves a specific gallery in the database based on an id
- INPUT PARAMETERS
  - none (the id is specified in the url)
- OUTPUT
  - an object representing the gallery of specified id
  - returns an empty array if no gallery match the id in the database

Example command to retrieve all the galeries:
```terminal
curl -X GET 'http://localhost:3000/gallery/21'
```

Example output:
```javascript
{
	"_id" : ObjectId("5e443ca166225f8fac8eb20b"),
	"listing_id" : 19,
	"listing_title" : "Downtown SF Studio Apartment Near Civic Center",
	"listing_images" : [
		{
			"_id" : ObjectId("5e443ca166225f8fac8eb220"),
			"id" : 561554778,
			"url" : "https://a0.muscache.com/4ea/air/v2/pictures/29a3d676-0c64-4df3-8568-ad1e48d25a5e.jpg?t=r:w1200-h720-sfit,e:fjpg-c90",
			"caption" : ""
		},
		{
			"_id" : ObjectId("5e443ca166225f8fac8eb21f"),
			"id" : 561554726,
			"url" : "https://a0.muscache.com/4ea/air/v2/pictures/da820318-2f83-41ab-8bc2-b97ac67dd6da.jpg?t=r:w1200-h720-sfit,e:fjpg-c90",
			"caption" : ""
		},
	],
	"__v" : 0
}
```
______________________________________________________________________
POST /gallery
- BEHAVIOR
  - stores a new gallery into the database
- INPUT PARAMETERS
  - an object with properties:

  - listing_id (type NUMBER): unique property identifier
  - listing_title (type STRING): name of the property
  - listing_images (type OBJECT): array containing the pictures of the property
    - id (type NUMBER): unique property image identifier
    - url (type STRING): url of the picture
    - caption (type STRING): caption of the picture

- OUTPUT
  - resID (type NUMBER): unique reservation ID that is cached locally for faster update/delete access

Example command to insert a gallery into the database: 
```terminal
curl -X POST 'Content-Type: application/json' '{"listing_id" : "200000","listing_title" : "xxxx","listing_images" : [{"id" : "561554778","url" : "https://a0.muscache.com/4ea/air/v2/pictures/29a3d676-0c64-4df3-8568-ad1e48d25a5e.jpg?t=r:w1200-h720-sfit,e:fjpg-c90","caption" : ""},{"id" : "561554726","url" : "https://a0.muscache.com/4ea/air/v2/pictures/da820318-2f83-41ab-8bc2-b97ac67dd6da.jpg?t=r:w1200-h720-sfit,e:fjpg-c90","caption" : "beautiful place"}]}' 'http://localhost:3000/gallery/21'
```
______________________________________________________________________
PUT /gallery/:id
- BEHAVIOR
  - updates the stored record matching the id with specified changes
- INPUT
  - object specifying the request changes. The object follows the guidelines of db.collection.update() of mongoDB.
- OUTPUT
  - none

Example command to update a gallery: 
```terminal
curl -X PUT -H "content-type: application/JSON" -d '{"$set": {"listing_title":"bob","listing_images.0.caption":"beautiful room"}}' http://localhost:3000/gallery/22
```
______________________________________________________________________
DELETE /:id
- BEHAVIOR
  - deletes a gallery in the database based on the id
- INPUT
  - none. The id is specified in the url.
- OUTPUT
  - none

Example command to delete a gallery:
```terminal
Curl -X DELETE 'http://localhost:3000/gallery/21'
```