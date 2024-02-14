# Google Shopping Pro - Scraper

## Description

The [Google Shopping Pro](https://apify.com/gooyer.co/google-shopping-pro) - Scraper is a sophisticated Actor designed for an in-depth extraction of data from Google Shopping. This tool is capable of retrieving a broad spectrum of information, from search results to intricate details on product pages, including offers, reviews, and specifications. Tailored for flexibility, it supports customized search queries, multiple country domains, and employs advanced proxy settings to navigate through Google's regional variations and anti-scraping measures efficiently.

## Features

- **Dynamic Data Retrieval**: Extracts data from search results, product pages, reviews, specifications, and offers.
- **Customizable Searches**: Users can specify start URLs, search queries, and desired pages for scraping.
- **Localized Scraping**: Adjust your scraping efforts to specific countries by setting the country code.
- **Enhanced Proxy Configuration**: Leverages customizable proxy settings for reliable data access across regions.

## Setup 

The code examples below show how to run the Actor and get its results. To run the code, you need to have an Apify account. Replace <YOUR_API_TOKEN> in the code with your API token, which you can find under Settings > Integrations in Apify Console. Learn mode



```javascript
import { ApifyClient } from 'apify-client';

// Initialize the ApifyClient with API token
const client = new ApifyClient({
    token: '<YOUR_API_TOKEN>',
});

// Prepare Actor input
const input = {
    "proxyUrls": {
        "useApifyProxy": true,
        "apifyProxyGroups": [
            "GOOGLE_SERP"
        ]
    }
};

(async () => {
    // Run the Actor and wait for it to finish
    const run = await client.actor("gooyer.co/google-shopping-pro").call(input);

    // Fetch and print Actor results from the run's dataset (if any)
    console.log('Results from dataset');
    const { items } = await client.dataset(run.defaultDatasetId).listItems();
    items.forEach((item) => {
        console.dir(item);
    });
})();
```

## Output Structure and Examples

### Search Page Output Example

```json
{
  	"query": "4k tv",
	"domain": "google.com",
	"source": "SEARCH_RESULTS",
	"rank": 1,
	"type": "organic",
	"productName": "Tcl 43 inch Class 4-Series 4K UHD HDR Smart Roku TV - 43s451",
	"lang": "en",
	"price": {
		"price": "$176.00",
		"currency": "$",
		"discount": null,
		"installment": null,
		"coupon": null,
		"deal": null,
		"status": null,
		"other": [
			"$196.00",
			"$176.00 Was $196.00."
		]
	},
	"deliveryInfo": "Free delivery & Free 90-day returns",
	"reviewsScore": "4.3",
	"reviewsCount": "",
	"tags": [
		"Flat",
		"HDR",
		"4K",
		"High Definition",
		"60 Hz",
		"LED",
		"3840 x 2160",
		"Black",
		"Google Assistant",
		"Amazon Alexa"
	],
	"description": "The TCL 4-Series Roku TV offers stunning 4K picture quality with four times the resolution of Full HD for enhanced clarity and ...",
	"merchantName": "Walmart",
	"merchantLink": "https://www.walmart.com/ip/....",
	"productLink": null,
	"images": [
		"https://encrypted-tbn2.gstatic.com/shopping..."
	],
	"compareLink": null,
	"shoppingId": null,
	"updated": "2024-02-12T18:43:05.106Z"
}
```

### Product Page Output Example

```json
{
  "source": "PRODUCT",
  "id": "4638703097820267064",
  "link": "https://www.google.com/shopping/product/4638703097820267064?q=4....",
  "lang": "en",
  "productName": "Hisense - 55\" Class A76K Series QLED 4K UHD Smart Google TV",
  "description": "The Hisense A76K series includes QLED – Quantum Dot Color Technology to dramatically increase the color space and improve overall color saturation from everything you watch. FilmMaker Mode built-in for simple video casting capabilities. These advancements are available in all sizes and position the A76K series as the “go-to” Hisense television for the perfect big 4K fit.",
	,
  "prices": [...],
  "images": [...],
  "tags": ["Flat", "HDR", "4K", "High Definition"],
  "specs": [...],
  "related": [...],
  "updated": "2024-02-11T17:15:21.085Z"
}
```

### Reviews Output Example

```json
{
  "source": "PRODUCT",
  "id": "4638703097820267064",
  "link": "https://www.google.com/shopping/product/17752236757406676875/reviews",
  "lang": "en",
  "productName": "Vizio 70\" Class V-Series 4K UHD LED Smart TV V705-J03",
  "avgRating": "4.5",
  "totalReviews": "9",
  "reviews": [...],
  "updated": "2024-02-11T17:19:07.241Z"
}
```

### Product Specs Output Example

```json
{
  "source": "PRODUCT",
  "id": "4638703097820267064", 
  "link": "https://www.google.com/shopping/product/4287311630501639152/specs",
  "Lang": "en",
  "productName": "Samsung 32 M80B 4K UHD HDR Smart Computer Monitor",
  "Description": "HANDPICKED BY AMAZON: They did the research so you don’t have to...",
  "Details": [...],
  "Updated": "2024-02-11T17:20:39.597Z"
}
```

### Offer Output Example

```json
{
  "source": "PRODUCT",
  "id": "4638703097820267064",
  "link": "https://www.google.com/shopping/product/7114557395854094262/offers",
  "lang": "en",
  "productName": "Samsung - 32\" M70B 4K USB-C Smart Monitor & Streaming TV",
  "offers": [...],
  "updated": "2024-02-11T17:17:25.807Z"
}
```

## Note & Feedback

Regular updates are crucial to maintain alignment with Google Shopping's evolving interface. Users are encouraged to monitor their scraping activities closely and adjust their configurations as needed for optimal performance.

We’re always working on improving the performance of our Actors. So if you’ve got any technical feedback or simply found a bug, please create an issue on the Actor’s Issues tab in Apify Console.

### Limitations

- Data extraction success may fluctuate due to changes on Google Shopping's website.
