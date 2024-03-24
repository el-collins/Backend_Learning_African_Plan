## Path Parameters:

1. **What are path parameters in FastAPI?**

   - Path parameters, also known as route parameters, allow you to capture values from the URL path.
   - They are part of the URL itself and are used to identify specific resources or endpoints.
   - For example, in the URL `/items/{item_id}`, `{item_id}` is a path parameter.

2. **How are path parameters defined in FastAPI route declarations?**

   - You can declare path parameters in FastAPI using the same syntax as Python format strings.
   - Example:

     ```python
     from fastapi import FastAPI

     app = FastAPI()

     @app.get("/items/{item_id}")
     async def read_item(item_id: str):
         return {"item_id": item_id}
     ```

3. **Can path parameters have default values? If yes, how can they be set?**

   - Path parameters cannot have default values. They are required by default.
   - If you want to make them optional, you can set their type to `Optional`.
   - Example:

     ```python
     from fastapi import FastAPI
     from typing import Optional

     app = FastAPI()

     @app.get("/items/{item_id}")
     async def read_item(item_id: Optional[str] = None):
         return {"item_id": item_id}
     ```

4. **Provide an example of a FastAPI route with path parameters.**

   - Example:

     ```python
     from fastapi import FastAPI

     app = FastAPI()

     @app.get("/items/{item_id}")
     async def read_item(item_id: str):
         return {"item_id": item_id}
     ```

## Query Parameters:

1. **What are query parameters in FastAPI?**

   - Query parameters are additional parameters sent in the URL after the `?` character.
   - They are used to filter, sort, or customize the response.
   - Example: `/items/?skip=0&limit=10`

2. **How are query parameters defined in FastAPI route declarations?**

   - Query parameters are automatically interpreted from function parameters that are not part of the path.
   - Example:

     ```python
     from fastapi import FastAPI

     app = FastAPI()

     @app.get("/items/")
     async def read_items(skip: int = 0, limit: int = 10):
         return {"skip": skip, "limit": limit}

     ```

3. **What is the difference between path parameters and query parameters?**

   - Path parameters are part of the URL path, while query parameters come after the `?` in the URL.
   - Path parameters are required, while query parameters can be optional.
   - Path parameters are used to identify specific resources, while query parameters are used for filtering or customization.

4. **Can query parameters have default values? If yes, how can they be set?**

   - Yes, query parameters can have default values.
   - Set the default value directly in the function parameter.
   - Example:

     ```python
     from fastapi import FastAPI

     app = FastAPI()

    fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}]


     @app.get("/items/")
     async def read_item(skip: int = 0, limit: int = 10):
         print("skip:", skip)
         print("limit:", limit)
         print(fake_items_db[skip : skip + limit])
         return fake_items_db[skip : skip + limit]
     ```

## Combining Path and Query Parameters:

1. **Can a FastAPI route have both path parameters and query parameters?**

   - Yes, a FastAPI route can have both path parameters and query parameters.
   - Example:

     ```python
     from fastapi import FastAPI

     app = FastAPI()

     @app.get("/items/{item_id}")
     async def read_item(item_id: str, skip: int = 0):
         return {"item_id": item_id, "skip": skip}
     ```

2. **What is the order of precedence if a parameter is defined both in the path and as a query parameter?**
   - The value from the path parameter takes precedence over the query parameter if both are defined.
   - If the path parameter is missing, the query parameter value is used.

### Data Types and Validation:

1. **How does FastAPI handle data types and validation for path and query parameters?**

   - FastAPI automatically converts and validates parameter values based on their declared types.
   - You can enforce additional validation rules using Pydantic models.

2. **What are some common data types that can be used for path and query parameters?**

   - Common data types include:
     - `str`: For strings (e.g., `/items/{item_id}`).
     - `int`: For integers (e.g., `/items/?page=1`).
     - `float`: For floating-point numbers (e.g., `/items/?price=19.99`).
     - `bool`: For boolean values (e.g., `/items/?active=true`).
     - Custom enums: To restrict values to a predefined set (e.g., `/items/?status=active`).

3. **How can you enforce validation rules on path and query parameters in FastAPI?**

   - Use Python type annotations to declare the expected data type.
   - Add additional validation rules using Pydantic models.
   - Example:

     ```python
     from fastapi import FastAPI
     from typing import Annotated
     from pydantic import constr

     app = FastAPI()

     @app.get("/items/")
     async def read_items(q: Annotated[str, Query(max_length=50)] = None):
         return {"q": q}
     ```

   - In this example, `max_length=50` enforces that the length of the `q` parameter does not exceed 50 characters.

## Combining Path and Query Parameters:

1. **Can a FastAPI route have both path parameters and query parameters?**

   - Yes, a FastAPI route can indeed have both path parameters and query parameters.
   - For example, consider the following route:

     ```python
     from fastapi import FastAPI

     app = FastAPI()

     @app.get("/items/{item_id}")
     async def read_item(item_id: str, skip: int = 0):
         return {"item_id": item_id, "skip": skip}
     ```

   - In this example, `{item_id}` is a path parameter, and `skip` is a query parameter.

2. **What is the order of precedence if a parameter is defined both in the path and as a query parameter?**
   - When a parameter is defined both in the path and as a query parameter, the value from the path parameter takes precedence.
   - If the path parameter is missing, the query parameter value is used.

## Data Types and Validation:

1. **How does FastAPI handle data types and validation for path and query parameters?**

   - FastAPI automatically converts and validates parameter values based on their declared types.
   - You can enforce additional validation rules using Pydantic models.

2. **What are some common data types that can be used for path and query parameters?**

   - Common data types include `str`, `int`, `float`, `bool`, and custom enums.
   - You can also use more complex types like UUIDs or custom Pydantic models.

3. **How can you enforce validation rules on path and query parameters in FastAPI?**
   - Use Python type annotations to declare the expected data type.
   - Add additional validation rules using Pydantic models.

## Usage and Benefits:

1. **In what scenarios would you use path parameters over query parameters, and vice versa?**

   - Use path parameters when the value is essential for identifying a specific resource (e.g., `/items/{item_id}`).
   - Use query parameters for optional filtering, sorting, or customization (e.g., `/items/?category=books&limit=10`).

2. **What are the benefits of using path and query parameters in API design?**

   - Path parameters provide a clear structure for resource identification.
   - Query parameters allow flexibility and customization without cluttering the URL path.

3. **Can you provide examples of real-world use cases where path and query parameters would be employed effectively?**
   - **Path Parameters**:
     - Retrieving a specific user profile: `/users/{user_id}`
     - Accessing a specific blog post: `/posts/{post_id}`
   - **Query Parameters**:
     - Filtering search results: `/search?query=fastapi&limit=10`
     - Sorting items: `/items/?sort=price&order=asc`

## Error Handling:

1. **How does FastAPI handle errors related to missing or invalid path/query parameters?**
   - FastAPI raises an `HTTPException` with the appropriate status code and error details.
   - You can customize error responses for missing or invalid parameters.
