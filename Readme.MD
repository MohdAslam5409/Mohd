# Add Product to Custom Collection API Test
## Objective:
Ensure that the API correctly adds a product to a custom collection.
## Preconditions:
1. The API is running.
2. Authentication credentials (API key or access token) with appropriate permissions should be available.
3. There is an existing custom collection in the store.
4. There is at least one product in the store.
## Test Steps:
1. **Send a POST request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/collects.json`
   - **Method:** `POST`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Request Body:**
     ```json
     {
       "collect": {
         "product_id": [ExistingProductId],
         "collection_id": [ExistingCustomCollectionId],
         "position": [DesiredPositionInCollection]
       }
     }
     ```
2. **Verify the HTTP response status code:**
   - **Expected:** `201 Created` - The product should be successfully added to the custom collection.

3. **Check the response format:**
   - **Expected:** Valid JSON data with the product details should be returned, indicating the success of the operation.

4. **Negative Test - Invalid Product ID:**
   - Send a request with an invalid product ID (e.g., non-existing product) and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).

5. **Negative Test - Invalid Collection ID:**
   - Send a request with an invalid collection ID (e.g., non-existing collection) and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).

6. **Negative Test - Invalid Position:**
   - Send a request with an invalid position value and ensure that the API returns an appropriate error response (e.g., `400 Bad Request`).

7. **Negative Test - Unauthorized Access:**
   - Attempt to add a product to a custom collection without providing valid authentication credentials and ensure that the API returns a `401 Unauthorized` status code.

# Retrieve List of Collects API Test

## Objective:
Ensure that the API correctly retrieves a list of collects.

## Preconditions:
1. The API is running.
2. Authentication credentials (API key or access token) with appropriate permissions should be available.
3. There is at least one collect in the store.

## Test Steps:
1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/collects.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the list of collects.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the collects.

4. **Verify the presence of collects:**
   - **Expected:** The response should contain a non-empty array of collects.

5. **Verify specific collect details (Optional):**
   - If you have known collect IDs, you can send additional requests to retrieve details for specific collects.
   - **Endpoint:** `/admin/api/2024-01/collects/[CollectId].json` for each collect ID.
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** Details for each specific collect should be returned.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Non-existing Collects:**
   - **Send a request for collects with a specific filter or parameters that result in an empty list.**
   - **Expected:** The API should return a response with an empty array.

8. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---
# Retrieve Specific Collect by ID API Test

## Objective:
Ensure that the API correctly retrieves a specific collect by its ID.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one collect in the store.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/collects/{collect_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the specific collect by its ID.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the specific collect.

4. **Verify the correctness of the retrieved collect:**
   - Send a separate request to retrieve the list of collects and identify the expected collect by its ID.
   - **Endpoint:** `/admin/api/2024-01/collects.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the specific collect with the provided ID.

5. **Negative Test - Non-existing Collect ID:**
   - **Send a request with a non-existing collect ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---
# Retrieve Count of Collects API Test

## Objective:
Ensure that the API correctly retrieves the count of collects.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one collect in the store.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/collects/count.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the count of collects.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing the count of collects.

4. **Verify the correctness of the retrieved count:**
   - Send a separate request to retrieve the list of collects and identify the expected count.
   - **Endpoint:** `/admin/api/2024-01/collects.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include a non-empty array of collects, and the count should match the count retrieved from the `/count.json` endpoint.

5. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

6. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---

 # Remove Product from Collection API Test

## Objective:
Ensure that the API correctly removes a product from a collection.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one product in the store.
- There is an existing collection with at least one product.

## Test Steps:

1. **Send a DELETE request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/collects/{collect_id}.json`
   - **Method:** `DELETE`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `204 No Content` - The API should successfully remove the product from the collection.

3. **Verify the correctness of the removal:**
   - Send a separate request to retrieve the list of collects and verify that the specified product is no longer associated with the collection.
   - **Endpoint:** `/admin/api/2024-01/collects.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should not include the product associated with the specified `{collect_id}`.

4. **Negative Test - Non-existing Collect ID:**
   - **Send a DELETE request with a non-existing collect ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

5. **Negative Test - Unauthorized Access:**
   - **Send a DELETE request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

6. **Negative Test - Invalid Endpoint:**
   - **Send a DELETE request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---
# Retrieve Single Collection by ID API Test

## Objective:
Ensure that the API correctly retrieves a single collection by its ID.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one collection in the store.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/collections/{collection_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the specific collection by its ID.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the specific collection.

4. **Verify the correctness of the retrieved collection:**
   - Send a separate request to retrieve the list of collections and identify the expected collection by its ID.
   - **Endpoint:** `/admin/api/2024-01/collections.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the specific collection with the provided `{collection_id}`.

5. **Negative Test - Non-existing Collection ID:**
   - **Send a request with a non-existing collection ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---
# Retrieve List of Products in a Collection API Test

## Objective:
Ensure that the API correctly retrieves a list of products belonging to a specific collection.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one collection in the store.
- The collection has at least one associated product.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/collections/{collection_id}/products.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the list of products belonging to the specified collection.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the products in the collection.

4. **Verify the presence of products:**
   - **Expected:** The response should contain a non-empty array of products associated with the specified collection.

5. **Negative Test - Non-existing Collection ID:**
   - **Send a request with a non-existing collection ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

8. **Negative Test - Empty Collection:**
   - **Ensure that the collection has no associated products, and then send a request to retrieve products from that collection.**
   - **Expected:** The API should return a response with an empty array of products.

---
# Create Custom Collection API Test

## Objective:
Ensure that the API correctly creates a custom collection.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.

## Test Steps:

1. **Send a POST request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/custom_collections.json`
   - **Method:** `POST`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Request Body:**
    json
     {
       "custom_collection": {
         "title": "New Custom Collection",
         "body_html": "<p>Description of the collection.</p>",
         "published": true
       }
     }

2. **Verify the HTTP response status code:**
   - **Expected:** `201 Created` - The API should successfully create the custom collection.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the newly created custom collection.

4. **Verify the correctness of the created collection:**
   - Send a separate request to retrieve the list of custom collections and verify that the specified collection is present.
   - **Endpoint:** `/admin/api/2024-01/custom_collections.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the newly created custom collection.

5. **Negative Test - Unauthorized Access:**
   - **Send a POST request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

6. **Negative Test - Invalid Endpoint:**
   - **Send a POST request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

7. **Negative Test - Missing Required Fields:**
   - **Send a POST request with missing or incomplete required fields in the request body.**
   - **Expected:** The API should return a response with an appropriate error message, indicating the missing or invalid parameter.

8. **Negative Test - Duplicate Collection Title:**
   - **Ensure there is an existing custom collection with the same title as the one being created, then attempt to create a new collection with the same title.**
   - **Expected:** The API should return a response with an appropriate error message, indicating that a custom collection with the same title already exists.

---
 # Retrieve List of Custom Collections by IDs API Test

## Objective:
Ensure that the API correctly retrieves a list of custom collections by their IDs.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There are custom collections in the store with the specified IDs.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/custom_collections.json?ids=395646240,691652237,841564295`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the list of custom collections.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the custom collections.

4. **Verify the presence of custom collections:**
   - **Expected:** The response should contain a non-empty array of custom collections with the specified IDs.

5. **Negative Test - Non-existing Collection IDs:**
   - **Send a request with non-existing collection IDs and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

8. **Negative Test - Empty Collection IDs:**
   - **Send a GET request without specifying any collection IDs.**
   - **Expected:** The API should return a response with an empty array of collections.

---
 # Retrieve Single Custom Collection by ID API Test

## Objective:
Ensure that the API correctly retrieves a single custom collection by its ID.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one custom collection in the store.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/custom_collections/{custom_collection_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the specific custom collection by its ID.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the specific custom collection.

4. **Verify the correctness of the retrieved custom collection:**
   - Send a separate request to retrieve the list of custom collections and identify the expected custom collection by its ID.
   - **Endpoint:** `/admin/api/2024-01/custom_collections.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the specific custom collection with the provided `{custom_collection_id}`.

5. **Negative Test - Non-existing Custom Collection ID:**
   - **Send a request with a non-existing custom collection ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---

 # Retrieve Count of Custom Collections API Test

## Objective:
Ensure that the API correctly retrieves the count of custom collections.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one custom collection in the store.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/custom_collections/count.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the count of custom collections.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing the count of custom collections.

4. **Verify the correctness of the retrieved count:**
   - Send a separate request to retrieve the list of custom collections and identify the expected count.
   - **Endpoint:** `/admin/api/2024-01/custom_collections.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include a non-empty array of custom collections, and the count should match the count retrieved from the `/count.json` endpoint.

5. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

6. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---
 # Delete Custom Collection API Test

## Objective:
Ensure that the API correctly deletes a custom collection.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one custom collection in the store with the specified ID (841564295 in this case).

## Test Steps:

1. **Send a DELETE request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/custom_collections/841564295.json`
   - **Method:** `DELETE`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `204 No Content` - The API should successfully delete the custom collection.

3. **Verify the deletion of the custom collection:**
   - Send a separate request to retrieve the list of custom collections or try to retrieve the specific custom collection by its ID.
   - **Endpoint (List):** `/admin/api/2024-01/custom_collections.json`
   - **Endpoint (Specific):** `/admin/api/2024-01/custom_collections/841564295.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The custom collection with the specified ID should no longer exist, and the API should return a `404 Not Found` status code.

4. **Negative Test - Non-existing Custom Collection ID:**
   - **Send a DELETE request with a non-existing custom collection ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

5. **Negative Test - Unauthorized Access:**
   - **Send a DELETE request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

6. **Negative Test - Invalid Endpoint:**
   - **Send a DELETE request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---
# Create New Product API Test

## Objective:
Ensure that the API correctly creates a new product.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.

## Test Steps:

1. **Send a POST request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/products.json`
   - **Method:** `POST`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Request Body:**
     ```json
     {
       "product": {
         "title": "New Product",
         "body_html": "<p>Description of the product.</p>",
         "vendor": "VendorName",
         "product_type": "Type",
         "variants": [
           {
             "title": "Variant 1",
             "price": "19.99",
             "inventory_quantity": 100
           }
         ],
         "options": [
           {
             "name": "Color",
             "values": ["Red", "Blue", "Green"]
           }
         ],
         "images": [
           {
             "src": "https://example.com/image1.jpg",
             "position": 1
           },
           {
             "src": "https://example.com/image2.jpg",
             "position": 2
           }
         ]
       }
     }
     ```

2. **Verify the HTTP response status code:**
   - **Expected:** `201 Created` - The API should successfully create the new product.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the newly created product.

4. **Verify the correctness of the created product:**
   - Send a separate request to retrieve the list of products and verify that the specified product is present.
   - **Endpoint:** `/admin/api/2024-01/products.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the newly created product.

5. **Negative Test - Unauthorized Access:**
   - **Send a POST request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

6. **Negative Test - Invalid Endpoint:**
   - **Send a POST request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

7. **Negative Test - Missing Required Fields:**
   - **Send a POST request with missing or incomplete required fields in the request body.**
   - **Expected:** The API should return a response with an appropriate error message, indicating the missing or invalid parameter.

8. **Negative Test - Duplicate Product Title:**
   - **Ensure there is an existing product with the same title as the one being created, then attempt to create a new product with the same title.**
   - **Expected:** The API should return a response with an appropriate error message, indicating that a product with the same title already exists.

---
 # Retrieve List of Products by IDs API Test

## Objective:
Ensure that the API correctly retrieves a list of products by their IDs.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There are products in the store with the specified IDs.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/products.json?ids=632910392,921728736`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the list of products.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the products.

4. **Verify the presence of products:**
   - **Expected:** The response should contain a non-empty array of products with the specified IDs.

5. **Negative Test - Non-existing Product IDs:**
   - **Send a request with non-existing product IDs and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

8. **Negative Test - Empty Product IDs:**
   - **Send a GET request without specifying any product IDs.**
   - **Expected:** The API should return a response with an empty array of products.

---
# Retrieve Single Product by ID API Test

## Objective:
Ensure that the API correctly retrieves a single product by its ID.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one product in the store.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the specific product by its ID.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the specific product.

4. **Verify the correctness of the retrieved product:**
   - Send a separate request to retrieve the list of products and identify the expected product by its ID.
   - **Endpoint:** `/admin/api/2024-01/products.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the specific product with the provided `{product_id}`.

5. **Negative Test - Non-existing Product ID:**
   - **Send a request with a non-existing product ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---
 # Retrieve Count of Products API Test

## Objective:
Ensure that the API correctly retrieves the count of products.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one product in the store.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/products/count.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the count of products.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing the count of products.

4. **Verify the correctness of the retrieved count:**
   - Send a separate request to retrieve the list of products and identify the expected count.
   - **Endpoint:** `/admin/api/2024-01/products.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include a non-empty array of products, and the count should match the count retrieved from the `/count.json` endpoint.

5. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

6. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---
# Modify Existing Product Image API Test

## Objective:
Ensure that the API correctly modifies an existing product image.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is an existing product with the specified `{product_id}`.
- There is an existing image for the product with the specified `{image_id}`.

## Test Steps:

1. **Send a PUT request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}/images/{image_id}.json`
   - **Method:** `PUT`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Request Body:**
     ```json
     {
       "image": {
         "src": "https://example.com/new_image.jpg",
         "position": 1
       }
     }
     ```

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully modify the existing product image.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the modified product image.

4. **Verify the correctness of the modified product image:**
   - Send a separate request to retrieve the product details, including the images.
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the modified image details with the specified `{image_id}`.

5. **Negative Test - Non-existing Product ID:**
   - **Send a PUT request with a non-existing product ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Non-existing Image ID:**
   - **Send a PUT request with a non-existing image ID for the specified product and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

7. **Negative Test - Unauthorized Access:**
   - **Send a PUT request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

8. **Negative Test - Invalid Endpoint:**
   - **Send a PUT request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

--- 
# Remove Existing Product Image API Test

## Objective:
Ensure that the API correctly removes an existing product image.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is an existing product with the specified `{product_id}`.
- There is an existing image for the product with the specified `{image_id}`.

## Test Steps:

1. **Send a DELETE request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}/images/{image_id}.json`
   - **Method:** `DELETE`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `204 No Content` - The API should successfully remove the existing product image.

3. **Verify the removal of the product image:**
   - Send a separate request to retrieve the product details, including the images.
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should not include the image details with the specified `{image_id}`.

4. **Negative Test - Non-existing Product ID:**
   - **Send a DELETE request with a non-existing product ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

5. **Negative Test - Non-existing Image ID:**
   - **Send a DELETE request with a non-existing image ID for the specified product and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a DELETE request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a DELETE request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---
# Create New Product Variant API Test

## Objective:
Ensure that the API correctly creates a new product variant.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is an existing product with the specified `{product_id}`.

## Test Steps:

1. **Send a POST request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}/variants.json`
   - **Method:** `POST`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Request Body:**
     ```json
     {
       "variant": {
         "title": "New Variant",
         "price": "29.99",
         "inventory_quantity": 50
       }
     }
     ```

2. **Verify the HTTP response status code:**
   - **Expected:** `201 Created` - The API should successfully create the new product variant.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the newly created product variant.

4. **Verify the correctness of the created product variant:**
   - Send a separate request to retrieve the product details, including the variants.
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the newly created variant details.

5. **Negative Test - Non-existing Product ID:**
   - **Send a POST request with a non-existing product ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a POST request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a POST request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

8. **Negative Test - Missing Required Fields:**
   - **Send a POST request with missing or incomplete required fields in the request body.**
   - **Expected:** The API should return a response with an appropriate error message, indicating the missing or invalid parameter.

9. **Negative Test - Duplicate Variant Title:**
   - **Ensure there is an existing variant with the same title as the one being created, then attempt to create a new variant with the same title.**
   - **Expected:** The API should return a response with an appropriate error message, indicating that a variant with the same title already exists.

---

 # Retrieve List of Product Variants API Test

## Objective:
Ensure that the API correctly retrieves a list of product variants for a specific product.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is an existing product with the specified `{product_id}`.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}/variants.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the list of product variants.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the product variants.

4. **Verify the presence of product variants:**
   - Send a separate request to retrieve the product details, including the variants.
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include a non-empty array of product variants.

5. **Verify specific product variant details (Optional):**
   - If you have known variant IDs, you can send additional requests to retrieve details for specific variants.
   - **Endpoint:** `/admin/api/2024-01/variants/{variant_id}.json` for each variant ID.
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** Details for each specific product variant should be returned.

6. **Negative Test - Non-existing Product ID:**
   - **Send a GET request with a non-existing product ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

7. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

8. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---

 # Receive Count of Product Variants API Test

## Objective:
Ensure that the API correctly receives the count of all product variants for a specific product.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is an existing product with the specified `{product_id}`.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}/variants/count.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully receive the count of all product variants.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing the count of product variants.

4. **Verify the correctness of the received count:**
   - Send a separate request to retrieve the list of product variants for the same product.
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}/variants.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include a non-empty array of product variants, and the count should match the count received from the `/count.json` endpoint.

5. **Negative Test - Non-existing Product ID:**
   - **Send a GET request with a non-existing product ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---

 # Receive Single Product Variant API Test

## Objective:
Ensure that the API correctly receives a single product variant by its ID.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is an existing product variant with the specified `{variant_id}`.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/variants/{variant_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully receive the details of the specified product variant.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the specified product variant.

4. **Verify the correctness of the received product variant details:**
   - Ensure that the response includes the expected details such as `id`, `title`, `price`, etc., for the specified `{variant_id}`.

5. **Negative Test - Non-existing Variant ID:**
   - **Send a GET request with a non-existing variant ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---

 # Modify Existing Product Variant API Test

## Objective:
Ensure that the API correctly modifies an existing product variant.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is an existing product variant with the specified `{variant_id}`.

## Test Steps:

1. **Send a PUT request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/variants/{variant_id}.json`
   - **Method:** `PUT`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Request Body:**
     ```json
     {
       "variant": {
         "title": "Modified Variant",
         "price": "39.99",
         "inventory_quantity": 30
       }
     }
     ```

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully modify the existing product variant.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the modified product variant.

4. **Verify the correctness of the modified product variant:**
   - Send a separate request to retrieve the product variant details.
   - **Endpoint:** `/admin/api/2024-01/variants/{variant_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the modified details for the specified `{variant_id}`.

5. **Negative Test - Non-existing Variant ID:**
   - **Send a PUT request with a non-existing variant ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a PUT request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a PUT request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

8. **Negative Test - Missing Required Fields:**
   - **Send a PUT request with missing or incomplete required fields in the request body.**
   - **Expected:** The API should return a response with an appropriate error message, indicating the missing or invalid parameter.

9. **Negative Test - Invalid Price Format:**
   - **Send a PUT request with an invalid price format (e.g., non-numeric) and ensure that the API returns an appropriate error response (e.g., `400 Bad Request`).**
   - **Expected:** The API should return a `400 Bad Request` status code.

---

 # Remove Existing Product Variant API Test

## Objective:
Ensure that the API correctly removes an existing product variant.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is an existing product variant with the specified `{variant_id}`.

## Test Steps:

1. **Send a DELETE request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}/variants/{variant_id}.json`
   - **Method:** `DELETE`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `204 No Content` - The API should successfully remove the existing product variant.

3. **Verify the removal of the product variant:**
   - Send a separate request to retrieve the product details, including the variants.
   - **Endpoint:** `/admin/api/2024-01/products/{product_id}/variants.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should not include the variant details with the specified `{variant_id}`.

4. **Negative Test - Non-existing Product ID:**
   - **Send a DELETE request with a non-existing product ID and variant ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

5. **Negative Test - Non-existing Variant ID:**
   - **Send a DELETE request with an existing product ID but a non-existing variant ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a DELETE request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a DELETE request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---

 # Create Smart Collection API Test

## Objective:
Ensure that the API correctly creates a smart collection.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.

## Test Steps:

1. **Send a POST request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/smart_collections.json`
   - **Method:** `POST`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Request Body:**
     ```json
     {
       "smart_collection": {
         "title": "New Smart Collection",
         "rules": [
           {
             "column": "tag",
             "relation": "equals",
             "condition": "clothing"
           },
           {
             "column": "price",
             "relation": "greater_than",
             "condition": "50.00"
           }
         ]
       }
     }
     ```

2. **Verify the HTTP response status code:**
   - **Expected:** `201 Created` - The API should successfully create the new smart collection.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the newly created smart collection.

4. **Verify the correctness of the created smart collection:**
   - Send a separate request to retrieve the details of the newly created smart collection.
   - **Endpoint:** `/admin/api/2024-01/smart_collections/{smart_collection_id}.json` (replace `{smart_collection_id}` with the actual ID returned in the response)
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the details of the newly created smart collection.

5. **Negative Test - Unauthorized Access:**
   - **Send a POST request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

6. **Negative Test - Missing Required Fields:**
   - **Send a POST request with missing or incomplete required fields in the request body.**
   - **Expected:** The API should return a response with an appropriate error message, indicating the missing or invalid parameter.

7. **Negative Test - Invalid Rule Condition:**
   - **Send a POST request with an invalid rule condition in the request body.**
   - **Expected:** The API should return a response with an appropriate error message, indicating the invalid rule condition.

8. **Negative Test - Invalid Rule Relation:**
   - **Send a POST request with an invalid rule relation in the request body.**
   - **Expected:** The API should return a response with an appropriate error message, indicating the invalid rule relation.

9. **Negative Test - Invalid Endpoint:**
   - **Send a POST request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---

 # Retrieve List of Smart Collections API Test

## Objective:
Ensure that the API correctly retrieves a list of smart collections.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one smart collection in the store.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/smart_collections.json?since_id=482865238`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the list of smart collections.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the smart collections.

4. **Verify the presence of smart collections:**
   - **Expected:** The response should contain a non-empty array of smart collections.

5. **Verify specific smart collection details (Optional):**
   - If you have known smart collection IDs, you can send additional requests to retrieve details for specific smart collections.
   - **Endpoint:** `/admin/api/2024-01/smart_collections/{smart_collection_id}.json` for each smart collection ID.
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** Details for each specific smart collection should be returned.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Non-existing Smart Collections:**
   - **Send a request for smart collections with a specific filter or parameters that result in an empty list.**
   - **Expected:** The API should return a response with an empty array.

8. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---

 # Retrieve Single Smart Collection API Test

## Objective:
Ensure that the API correctly retrieves a single smart collection by its ID.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is an existing smart collection with the specified `{smart_collection_id}`.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/smart_collections/{smart_collection_id}.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the details of the specified smart collection.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the specified smart collection.

4. **Verify the correctness of the received smart collection details:**
   - Ensure that the response includes the expected details such as `id`, `title`, `rules`, etc., for the specified `{smart_collection_id}`.

5. **Negative Test - Non-existing Smart Collection ID:**
   - **Send a GET request with a non-existing smart collection ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---

 # Retrieve Count of Smart Collections API Test

## Objective:
Ensure that the API correctly retrieves a count of smart collections.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is at least one smart collection in the store.

## Test Steps:

1. **Send a GET request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/smart_collections/count.json`
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully retrieve the count of smart collections.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing the count of smart collections.

4. **Verify the correctness of the received count:**
   - Ensure that the response includes the expected count of smart collections.

5. **Negative Test - Unauthorized Access:**
   - **Send a GET request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

6. **Negative Test - Invalid Endpoint:**
   - **Send a GET request to an invalid endpoint.**
   - **Expected:** The API should return a `404 Not Found` status code.

---
# Update Existing Smart Collection API Test

## Objective:
Ensure that the API correctly updates an existing smart collection.

## Preconditions:

- The API is running.
- Authentication credentials (API key or access token) with appropriate permissions should be available.
- There is an existing smart collection with the specified `{smart_collection_id}`.

## Test Steps:

1. **Send a PUT request to the API endpoint:**
   - **Endpoint:** `/admin/api/2024-01/smart_collections/{smart_collection_id}.json`
   - **Method:** `PUT`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Request Body:**
     ```json
     {
       "smart_collection": {
         "title": "Updated Smart Collection Title",
         "rules": [
           {
             "column": "tag",
             "relation": "equals",
             "condition": "shoes"
           },
           {
             "column": "price",
             "relation": "less_than",
             "condition": "100.00"
           }
         ]
       }
     }
     ```

2. **Verify the HTTP response status code:**
   - **Expected:** `200 OK` - The API should successfully update the existing smart collection.

3. **Check the response format:**
   - **Expected:** Valid JSON data should be returned, containing information about the updated smart collection.

4. **Verify the correctness of the updated smart collection details:**
   - Send a separate request to retrieve the details of the updated smart collection.
   - **Endpoint:** `/admin/api/2024-01/smart_collections/{smart_collection_id}.json` (replace `{smart_collection_id}` with the actual ID returned in the response)
   - **Method:** `GET`
   - **Headers:**
     - `Content-Type: application/json`
     - `Authorization: Bearer [YourAccessToken]`
   - **Verify:** The response should include the updated details of the smart collection.

5. **Negative Test - Non-existing Smart Collection ID:**
   - **Send a PUT request with a non-existing smart collection ID and ensure that the API returns an appropriate error response (e.g., `404 Not Found`).**
   - **Expected:** The API should return a `404 Not Found` status code.

6. **Negative Test - Unauthorized Access:**
   - **Send a PUT request without valid authentication credentials.**
   - **Expected:** The API should return a `401 Unauthorized` status code.

7. **Negative Test - Missing Required Fields:**
   - **Send a PUT request with missing or incomplete required fields in the request body.**
   - **Expected:** The API should return a response with an appropriate error message, indicating the missing or invalid parameter.

8. **Negative Test - Invalid Rule Condition:**
   - **Send a PUT request with an invalid rule condition in the request body.**
   - **Expected:** The API should return a response with an appropriate error message, indicating the invalid rule condition.

9. **Negative Test - Invalid Rule Relation:**
   - **Send a PUT request with an invalid rule relation in the request body.**
   - **Expected:** The API should return a response with an appropriate error message, indicating the invalid rule relation.

10. **Negative Test - Invalid Endpoint:**
    - **Send a PUT request to an invalid endpoint.**
    - **Expected:** The API should return a `404 Not Found` status code.

---

 

 







 


 








 




 
