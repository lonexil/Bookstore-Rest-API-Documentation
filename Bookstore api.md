# BOOKSTORE API
## OVERVIEW
The bookstore API allows developers to access data about books , authors and book sales.
You can use this API to retrieve book information, add new books, update existing records , and manage authors.
All response are returned in JSON format.

Base URL

``` https:// api.boookstore.example.com/v1 ```

## Authentication
This API use API key Authentication 
Include your API key in your request header for all authenticated endpoints.

Example

``` Authorization: Bearer YOUR_API_KEY ```

If an invalid API key is used, the server returns a 401 Unauthorized error.

## Endpoints
1. Get all books 

Endpoint:

``` GET/books ```

Description:

Fetches a paginated list of all book in the store.

Query parameters

|parameter|Type|Description
-------|---------|-----------
|page|integer|Page number (default 1)|
|limit|integer|Number of results per page (default-10)|
|author|string|Filter book by author"s name(optional)|

Example request

``` 
curl -X GET https://api.bookstore.example.com/v1/books?page=1&limit=5 Authorization:Bearer YOUR_API_KEY
 ```

 Example response:

 ``` JSON
 {
    "page" : 1,
    "limit" : 5,
    "total_books":123,
    
    {
        "id":101,
        "title":"The midnight library",
        "author": "Matt Haig",
        "price" : 14.99,
        "avaliable": true

    },
    {
        "id":102,
        "title":"Atomic Habits",
        "author": "James clear",
        "price":20.90,
        "available": true
    }.........
 } 
```
 2.  Get books by ID

 Endpoint:

 ``` GET/books/{id} ```

 Description:
 Retrieve detailed information about a specific book using it's ID.

 Example request:

 ``` 
 GET https://api.bookstore.com/v1/books/101 Authorizatiom: Baerer YOUR_API_KEY 

 ```
 Exanple response :
 
 ```
 {
    "id":101,
    "title": "The midnight library",
    "author":"Matt Haig"
    "genre": "fiction",
    "published_year":2020,
    "price": 14.99,
    "stock": 25
    
 } 
 ```
 3. Add a New Book
 Endpoint:

 ``` POST/ books ```

 Description:
 Adds a new book to the store catalog.

 Request Body:

 ``` 
 {
    "message": "The psychology of money",
    "author":"Morgan Housel",
    "genre":"finance",
    "price": 16.50,
    "stock": 40 
 } 
 ```

  Example Response

 ``` {
    "message": "Book sucessfully added"
    "book":{
    "id":125,
    "title":"Psychology of money"
    "Author":"Morgan Housel"
    "price":16.50,
    "stock":40
    }
  } 
   ```

  4. Get All Authors

  Endpoint:

  ```GET/authors```

  Description
  Returns a list of all registered authors.
  
  Example response:
  
  ```
  {
    "total_authors: 3,
    "data" :[
        {
            "id":1,"name':"Matt Haig","country":"UK"
        },
        {
            "id":2,"name":"James clear","Country":USA"
        },
        {
            "id":3,"name":"Morgan Housel","country":"USA"
        }
    ]
    
    
  }
  ```
  ## Error Codes
  |Status code|Meaning|Example cause|
  |--------|---------|-----------|
  |200 ok|sucessful request|Data retrieved sucessfully |
  |201 Created|New record created|New book added|
  |400 Bad request|Invalid input|Missing title or price|
  |401 Unauthorized|No/Invalid API key|Missing or wrong Authorization header|
  |404 Not found|Resource not found |Book Id does not exist|
  |500 internal server error| Server issue|Database or network problem|
