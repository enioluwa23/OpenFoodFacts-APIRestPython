# Open Food Facts API Rest Python #

OFF API provides programmatic access to Open Food Facts functionality and content.<br/>

To try the API : https://offapi.herokuapp.com/ <br/>
Or if you want to try in localhost, see below.

The API is [REST API](http://en.wikipedia.org/wiki/Representational_State_Transfer "RESTful").
Currently, return format for all endpoints is [JSON](http://json.org/ "JSON").

## What is this repository for? 

This piece of software’s main goals are :
* To make it easy to retrieve data using HTTP requests
* To provide filters in the API
* To provide custom filters


## Setup for localhost

* Install python 3
* Install mongodb
* Install pip
* Install requirements : `$ pip install -r requirements.txt`
* Download the database from : http://world.openfoodfacts.org/data/openfoodfacts-mongodbdump.tar.gz
* Import to local mongodb : `$ mongorestore -d off -c products /foldertobsonfile/products.bson`
* Launch api : `$ python3 runApiRESTServer.py`
* That's all !

## Documentation
### How to use it?

Simple filter : `/products?origins=United Kingdom` <br/>
Complex filter : `/products?nutrition_grade_fr=a&origins=United Kingdom` <br/>
For arrays, a “.” will be used as a separator like so : `/products?nutrient_levels.salt=low`
Searchs can be inexact like :`/products?ingredients_text=beef`<br/>
It will retrieve tags like “beef braising steak”, “beef steak”...

/!\ By default the objects will be sorted by `created_t` in order to have the most important objects first

URL to query                   | Description
------------------------------ | ---------------------------
<code>GET</code> `/product/<barcode>`           | Get a product by barcode eg. `/product/737628064502`
<code>GET</code> `/products/brands`             | If you want to know how many brands there are in the list you have just to do a request like that : `/products/brands?count=1`. If you want to query brands, to do for example an autocomplete field in ajax, query the API like : `/products/brands?query=Auch` or `/products/brands?query=Sains`.
<code>GET</code> `/products/categories`         | If you want to know how many categories there are in the list you have just to do a request like that : `/products/categories?count=1`. If you want to query categories, to do for example an autocomplete field in ajax, query the API like : `/products/categories?query=Ric` or `/products/categories?query=plant`.
<code>GET</code> `/products/countries`          | If you want to know how many countries there are in the list you have just to do a request like that : `/products/countries?count=1`. If you want to query countries, to do for example an autocomplete field in ajax, query the API like : `/products/countries?query=Fra` or `/products/countries?query=Aus`.
<code>GET</code> `/products/additives`          | If you want to know how many additives there are in the list you have just to do a request like that : `/products/additives?count=1`. If you want to query additives, to do for example an autocomplete field in ajax, query the API like : `/products/additives?query=Citric` or `/products/additives?query=acid`.
<code>GET</code> `/products/allergens`          | If you want to know how many allergens there are in the list you have just to do a request like that : `/products/allergens?count=1`. If you want to query allergens, to do for example an autocomplete field in ajax, query the API like : `/products/allergens?query=milk` or `/products/allergens?query=oil`. 

### Options

Field         | Value by default | Value type
------------- | ---------------- | ---------
limit=        | 50               | limit the number of products returned
skip=         | 0                | skips the specified number of products returned
count=        | 0                | if 1 then returns the number of rows
short=        | 0                | Filters rows retrieved, make it faster for lists for example, if 1 columns projection on `code`, `lang` and `product_name`
q    =        | none             | search text on indexed fields

### Indexed fields

Some fields are described here : http://world.openfoodfacts.org/data/data-fields.txt 

## Creators

**Scot Scriven**
- <https://github.com/itchix>

## Copyright and license

    Copyright 2015 Scriven Scot
    
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
    
        http://www.apache.org/licenses/LICENSE-2.0
    
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
