
###### Priorities
- [x] Fix the authrization / authentication
	- [x] Log in of new users
		- [x] sso-callback page broken 
		- [x] email register new user broken
- [x] CMS - management system
	- [x] Create Products entity
		- [x] Create Product
		- [x] List Products
		- [x] Delete product 
		- [x] List one product - detail
	- [x] Create flows
		- [x] BE is prepared
		- [x] Create flow
		- [x] List all flows inside of an product
		- [x] Delete flow inside of an product
		- [x] List one flow - detail
	- [x] Create screenshot entities
		- [x] BE is prepared
		- [x] Create screenshot
		- [x] List all screenshots inside of an product
		- [x] Delete screenshot
		- [x] List all screenshots inside of an flow
		- [x] List one screenshot - detail
- [x] Upload of the images
	- [x] Subscription of the cloudflare R2
	- [x] Adding images in the cloudflare dashboard and adding ID's in the platfiorm
	- [x] Displaying images in the platform
	- [x] Upload images through the platform
- [x] Deployments
	- [x] Re-search again hosting - most likely AWS
	- [x] Deploy BE successfully
		- [x] Deploy the NodeJS service
		- [x] Deploy postgresql database and migrate everything correctly
	- [x] Deploy FE
		- [x] Deploy FE with correct env variables
		- [x] Cloudflare images are accessible from my domain
- [x] User management
	- [x] BE is prepared
	- [x] Listing all of the users
	- [x] Making some user an admin
- [x] Filtering in the table of different entities
- [x] Add dayJS to resolve date times in the tables

###### Product's page
- You can add name of the product
- You can add description of the product
- (image of the product - not important now)
###### Flow's page
- You can add different screenshot's
- You can add name of the flow
- You can add description of the flow

- [x] Pay for cloudflare subscription so I am able to upload image's

###### Screenshot
-![[Untitled1.png]]

Postgresql database in aws

- master username
	- davkud7
	- mypassworddavkud7


ERT4ue+hD8RiavyBzCGbjHWwEXAtE3VHULnJDFNW

_0c51d6ae237508c54de56439ac15bb92.djqtsrsxkq.acm-validations.aws.


###### Impovements
- [x] Bulk upload of screenshots that would automatically create the `Screenshot` entity
- [x] URL is missing on screenshot entity
- [x] Ordering of screenshots on frontend by the number or createdAt entity
- [x] Generating tags - for screenshots by endpoint

###### On Product screenshot
- [x] Needs to include URL



