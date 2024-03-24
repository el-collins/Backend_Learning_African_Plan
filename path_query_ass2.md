## Code Writing: Path Parameters

**Write a FastAPI route that accepts a path parameter for user identification (user_id) and returns the user's profile information.**
**Implement error handling for the case when the user_id path parameter is missing.**

```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

# Example user profiles (for demonstration purposes)
user_profiles = {
    1: {"username": "alice", "email": "alice@example.com"},
    2: {"username": "bob", "email": "bob@example.com"},
}

@app.get("/users/{user_id}")
async def read_user_profile(user_id: int):
    if user_id not in user_profiles:
        raise HTTPException(status_code=404, detail="User not found")
    return user_profiles[user_id]
```

## Code Writing: Query Parameters

**Create a FastAPI route that accepts query parameters for filtering a list of products by category and price range.**
**Implement default values for the query parameters (category defaulting to 'all' and price_range defaulting to a specific range).**

```python
@app.get("/products/")
async def filter_products(category: str = "all", price_range: str = "0-100"):
    return {"category": category, "price_range": price_range}
```

## Combining Path and Query Parameters

**Write a FastAPI route that accepts a path parameter for city (city_id) and query parameters for filtering restaurants by cuisine type (cuisine) and rating (min_rating).**

**Ensure that the city ID is a path parameter while cuisine type and minimum rating are query parameters.**
```python
@app.get("/restaurants/{city_id}")
async def filter_restaurants(
city_id: int, cuisine: str = None, min_rating: float = 3.5
): # Your logic here (filter restaurants based on city, cuisine, and rating)
return {
"city_id": city_id,
"cuisine": cuisine,
"min_rating": min_rating,
}
```

## Data Validation

**Modify an existing FastAPI route that accepts a path parameter for user_id to ensure that user_id is an integer and greater than zero.**

**Add validation to a query parameter start_date to ensure it is a valid date format.**
``` python
@app.get("/users/{user_id}")
async def read_user_profile(user_id: int):
if user_id <= 0:
raise HTTPException(status_code=400, detail="Invalid user ID")
return user_profiles.get(user_id, {})
```

## Usage and Benefits

**Analyze a given FastAPI application and identify instances where using path parameters would be more appropriate than query parameters, and vice versa.**
**Discuss the benefits of using path and query parameters in the provided FastAPI application and how it enhances API design.**

