# Yelp-Web-API Service Wrapper

This is a .Net (VS 20013 .net 4.5) service wrapper used to leverage Yelp's Business and
Search Web APIs.

## Code Example

```cs

 			var businessRequest = new BusinessRequest 
            {   
                ConsumerKey = ConfigurationManager.AppSettings["ConsumerKey"],
                ConsumerSecret = ConfigurationManager.AppSettings["ConsumerSecret"],
                Token = ConfigurationManager.AppSettings["Token"],
                TokenSecret = ConfigurationManager.AppSettings["TokenSecret"],
                BusinessId = "yelp-san-francisco"
            };

            using (var businessAdapter = new BusinessAdapter(businessRequest))
            {

                var response = businessAdapter.GetYelpBusinessResults();
                
                Console.WriteLine(response.Success);

                if(!response.Success)
                    Console.WriteLine(response.ErrorMessage);

                Console.WriteLine(response.YelpData);

                Console.ReadLine();

            }
            
```

## Motivation

The objective is to create a series of Service Wrappers to help developers leverage 
popular Web APIs--in this case Yelp.

## Installation
The downloadable zip is a solution that comes with the ServiceWrapper Project as well as a 
test Client project. To install you'll need VS2013 or greater, and be able to support
.Net 4.5.

To use the Service Wrapper project it's recommend you generate a dll (build the project)
and drop it into whatever solution you're working on. Also xml markup comments were 
included so if you go into the project properties and select generate xml markup file you 
can include that file along with the dll, which will grant you intellisense. 

Lastly since this project leverages the Yelp API you'll need to create a developer account
if you don't already have one. It's a quick 2 minute process. Once you've done that you'll
be able to generate a ConsumerKey, ConsumerSecret, Token, and TokenSecret access key.
You'll need to add these to your appsettings so that Yelp's API can authenticate you.

```
  <appSettings>
    <add key="ConsumerKey" value="" />
    <add key="ConsumerSecret" value="" />
    <add key="Token" value="" />
    <add key="TokenSecret" value="" />
  </appSettings>
 ```
  
## API Reference


## Business
###Properties

```
-BusinessId
type: string
description: The Id of the business you're request is being generated for. This id is 
usually obtained by first calling the Search Web API.
```

###Methods

```
-GetYelpBusinessResults function()
type: method
description: Gets the results from the Yelp Business Web API.
```

## Search
###Properties

```
-Term
type: string
description: Search term (e.g. "food", "restaurants"). If term isn’t included we search. 
everything.
```

```
-Limit
type: int
description: Number of business results to return.
```

```
-Offset
type: int
description: Offset the list of returned business results by this amount.
```

```
-Sort
type: int
description: Sort mode: 0=Best matched (default), 1=Distance, 2=Highest Rated.
```

```
-CategoryFilter
type: string
description: see https://www.yelp.com/developers/documentation/v2/all_category_list.
```

```
-RadiusFilter
type: string
description: Search radius in meters. If the value is too large, a AREA_TOO_LARGE error 
may be returned. The max value is 40000 meters (25 miles).
```

```
-CC
type: string
description: country code, see http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2.
```

```
-Lang
type: string
description: language, see http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes.
```

```
-DealsFilter
type: bool
description: Whether to exclusively search for businesses with deals.
```

```
-GeoCoordinates
type: object
description: contains querystring parmaters related to GeoCoordinates.
```

```
-Bounds
type: object
description: contains querystring parmaters related to Bounds.
```

```
-Location
type: object
description: contains querystring parmaters related to Location.
```


###Methods

```
-GetYelpSearchResults function()
type: method
description: Gets the results from the Yelp Search Web API.
```


## Tests
Included in the downloadable zip is a client test project.

## License

MIT
