###### Research phase
- [ ] research model for extraction of description and tags from UI screenshot
- ChatGPT can do this for us
- [ ] research model for mapping of ChatGPT response to example
- I think, we can again use ChatGPT to this, so far it seemed to me as the highest quality model for processing requests

- [x] research MVP costs (data storage, 3rd party services)
Models
- ChatGPT can do everything requested and seemed so far the best platform for this
	- 2.5 usd per 1M input tokens approx.
	- 10 usd per 1M output tokens
	- 1M tokens should about 750,000 tokens
		- Could be cheaper using their batch requests (that can take up to 24 hours to finish, but can be used for image processing - time is not that important and is half the price
	- Or we can use older models with some discounted price, for the future we can use different cheaper models for chat or tagging or something else, but ChatGPT was the best out of the ones I tested (Gemini, Grok, Perplexity)

- File storage 
	- We can use cloudflare R2 data storage
	- 10 GB of images is for free and no egress fee's (which means no extra fee for bandwidth)
		- 0.01 USD per another GB
		- 1M of create/update/delete for free, then 4.50 USD per another milion requests
		- 10M of read for free, then 0.36 USD per another milion requests
	- We can in the future use cloudflare image features to transform quality of images to serve them faster to the users


- FE application hosting
	- Cloudflare hosting - deploys the app across the world as well for faster serving to the user's 
	- There is some limitation for development, but seems ok to have just free tier for very long time
- BE Hosting
	- I think, the only way to go would be with hosted BE service with hosted database
	- Most likely that for the beginning I would choose some auto managed platform for easy management ( not to spend time at the beginning on dev ops )
	- Digital ocean is for example
		- Database is 15 USD per month
		- Backend service 12 USD per month
- Authorization / authentication
	- Clerk
		- Supports almost everything we need
		- Super easy to integrate into the product
		- free until 10k users MAU (monthly active users)
			- 25 usd per month plus 0.02 per user MAU