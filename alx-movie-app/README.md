## API Overview

MoviesDatabase is a free API that provides up-to-date information for 9 million+ movies, series, episodes, and 11 million+ actors/crew. You get details like trailers, awards, biographies, ratings, and more.

## Version

_Not specified in the documentation._

## Available Endpoints

- **GET** `/titles`  
  Returns a list of titles (movies, series, episodes) with optional filters (genre, year, sorting).
- **GET** `/x/titles-by-ids`  
  Returns multiple titles by providing an array of IMDb IDs.
- **GET** `/titles/{id}`  
  Returns detailed info for one title by its IMDb ID.
- **GET** `/titles/{id}/ratings`  
  Returns average rating and vote count for a title.
- **GET** `/titles/series/{id}`  
  Returns all episodes for a series (id = series IMDb ID).
- **GET** `/titles/seasons/{id}`  
  Returns total number of seasons for a series.
- **GET** `/titles/series/{id}/{season}`  
  Returns episodes for one season of a series.
- **GET** `/titles/episode/{id}`  
  Returns info for a single episode.
- **GET** `/titles/x/upcoming`  
  Returns upcoming titles.
- **GET** `/titles/search/keyword/{keyword}`  
  Search titles by keyword.
- **GET** `/titles/search/title/{title}`  
  Search titles by (partial) title.
- **GET** `/titles/search/akas/{aka}`  
  Search titles by exact AKA.
- **GET** `/actors`  
  Returns a list of actors with pagination.
- **GET** `/actors/{id}`  
  Returns details for one actor.
- **GET** `/title/utils/titleType`  
  Returns a list of title types (movie, series, etc.).
- **GET** `/title/utils/genres`  
  Returns a list of genres.
- **GET** `/title/utils/lists`  
  Returns predefined title lists (e.g., top-rated).

## Request and Response Format

- **Requests** use standard HTTP GET and optional query parameters (`page`, `limit`, `info`, `genre`, etc.).
- **Responses** are JSON objects with a `results` array and pagination fields (`page`, `next`, `entries`) when applicable.

**Example Request:**

```http
GET /titles?genre=Comedy&limit=5&page=1
Example Response:

json
Copy
Edit
{
  "results": [
    { 
      "id": "tt1234567", 
      "titleText": "Funny Movie", 
      … 
    }
  ],
  "page": 1,
  "next": "/titles?genre=Comedy&limit=5&page=2",
  "entries": 5
}
```

## Authentication
No authentication required for the BASIC plan. Just send requests to the base URL.

## Error Handling
**400 Bad Request** Invalid parameter values. Check query names/types.

**404 Not Found**
ID or path does not exist.

**429 Too Many Requests**
Rate limit exceeded. Retry after a pause.

**500 Server Error**
Server problem. Retry later or contact API support.

## Usage Limits and Best Practices
**Rate Limit:** Up to 50 items per page; overall call limits not specified.

**Batch Requests:** Use /x/titles-by-ids to fetch multiple titles in one call.

**Caching**: Cache repeated requests (e.g., static info) to reduce load.

**Filtering:** Use the info parameter to request only needed fields (e.g., mini_info, base_info).
