### **API Write Function Documentation**  
**Base URL**: `https://{your_domain}/api-v{api_version}/fasterwrite.php`  
**Authentication**: Token-based (generated via `/fastertokengenerator.php`).  

---

### **1. Write Data to a Specific Table**  
**Endpoint**:  
`GET /fasterwrite.php?tableKey={table_name}&key={key1,key2}&value={value1,value2}&token={on_time_token}`  

**Parameters**:  
- `tableKey`: The name of the table (e.g., `fasttablekey`).  
- `key`: Comma-separated list of keys (e.g., `id,name,email`).  
- `value`: Comma-separated list of values (e.g., `faster,Takbir,takbir@gmail.com`).  
- `token`: Your secure token (e.g., `ndjdbdbjkel572827`).  

**Example**:  
```url
https://{your_domain}/api-v1/fasterwrite.php?tableKey=fasttablekey&key=id,name,email&value=faster,Takbir,takbir@gmail.com&token=ndjdbdbjkel572827
```  

**Response**:  
```json
[
    {"key":"id","status":"success","message":"Data written successfully"},
    {"key":"name","status":"success","message":"Data written successfully"},
    {"key":"email","status":"success","message":"Data written successfully"}
]
```  

**Errors**:  
- `401 Unauthorized`: Invalid/missing token.  
- `400 Bad Request`: Keys and values count mismatch.  
- `404 Not Found`: Table does not exist.  
- `500 Internal Server Error`: Database connection/query failure.  

---

### **2. Write Multiple Key-Value Pairs**  
**Endpoint**:  
`GET /fasterwrite.php?tableKey={table_name}&key={key1,key2,key3}&value={value1,value2,value3}&token={on_time_token}`  

**Parameters**:  
- `tableKey`: The name of the table (e.g., `fasttablekey`).  
- `key`: Comma-separated list of keys (e.g., `id,name,email,age`).  
- `value`: Comma-separated list of values (e.g., `faster,Takbir,takbir@gmail.com,25`).  
- `token`: Your secure token (e.g., `ndjdbdbjkel572827`).  

**Example**:  
```url
https://{your_domain}/api-v1/fasterwrite.php?tableKey=fasttablekey&key=id,name,email,age&value=faster,Takbir,takbir@gmail.com,25&token=ndjdbdbjkel572827
```  

**Response**:  
```json
[
    {"key":"id","status":"success","message":"Data written successfully"},
    {"key":"name","status":"success","message":"Data written successfully"},
    {"key":"email","status":"success","message":"Data written successfully"},
    {"key":"age","status":"success","message":"Data written successfully"}
]
```  

**Errors**:  
- `401 Unauthorized`: Invalid/missing token.  
- `400 Bad Request`: Keys and values count mismatch.  
- `404 Not Found`: Table does not exist.  
- `500 Internal Server Error`: Database connection/query failure.  

---

### **3. Update Existing Data**  
If a key already exists in the table, its value will be updated.  

**Example**:  
```url
https://{your_domain}/api-v1/fasterwrite.php?tableKey=fasttablekey&key=id,name,email&value=faster,Takbir,newemail@gmail.com&token=ndjdbdbjkel572827
```  

**Response**:  
```json
[
    {"key":"id","status":"success","message":"Data written successfully"},
    {"key":"name","status":"success","message":"Data written successfully"},
    {"key":"email","status":"success","message":"Data updated successfully"}
]
```  

---

### **Error Codes**

| Code | Message                          | Description                          |  
|------|----------------------------------|--------------------------------------|  
| 401  | `Access denied. Invalid token`   | Token missing, expired, or invalid.  |  
| 400  | `Keys and values count mismatch` | Number of keys and values do not match. |  
| 404  | `Table not found`                | The specified table does not exist.  |  
| 500  | `Internal server error`          | Database connection/query failure.   |  

---

### **Quick Start Guide**

1. **Generate a Token**:  
   ```url
   https://{your_domain}/api-v1/fastertokengenerator.php
   ```  
   Copy the token from the response.  

2. **Write Data to a Table**:  
   ```url
   https://{your_domain}/api-v1/fasterwrite.php?tableKey=fasttablekey&key=id,name,email&value=faster,Takbir,takbir@gmail.com&token=ndjdbdbjkel572827
   ```

3. **Write Multiple Key-Value Pairs**:  
   ```url
   https://{your_domain}/api-v1/fasterwrite.php?tableKey=fasttablekey&key=id,name,email,age&value=faster,Takbir,takbir@gmail.com,25&token=ndjdbdbjkel572827
   ```

4. **Verify Data**:  
   Use the `fasterread.php` endpoint to verify the data was written successfully.  
   Example:
   ```url
   https://{your_domain}/api-v1/fasterread.php?tableKey=fasttablekey&token=ndjdbdbjkel572827
   ```

---

### **Notes**

- **No Dynamic Table Creation**: The table must already exist. If it doesn’t, the API will return a `404 Not Found` error.
- **Multiple Key-Value Pairs**: You can write multiple key-value pairs in a single request.
- **Token Expiry**: Tokens expire after **5 minutes** and are **one-time use**.

---

### **Example Workflow**

1. **Generate Token**:  
   ```url
   https://{your_domain}/api-v1/fastertokengenerator.php
   ```  
   **Response**:  
   ```json
   {
       "status": "success",
       "token": "ndjdbdbjkel572827"
   }
   ```

2. **Write Data**:  
   ```url
   https://{your_domain}/api-v1/fasterwrite.php?tableKey=fasttablekey&key=id,name,email&value=faster,Takbir,takbir@gmail.com&token=ndjdbdbjkel572827
   ```  
   **Response**:  
   ```json
   [
       {"key":"id","status":"success","message":"Data written successfully"},
       {"key":"name","status":"success","message":"Data written successfully"},
       {"key":"email","status":"success","message":"Data written successfully"}
   ]
   ```

3. **Verify Data**:  
   ```url
   https://{your_domain}/api-v1/fasterread.php?tableKey=fasttablekey&token=ndjdbdbjkel572827
   ```  
   **Response**:  
   ```json
   {
       "status": "success",
       "table": "fasttablekey",
       "data": [
           {"id": 1, "data_key": "id", "data_value": "faster"},
           {"id": 2, "data_key": "name", "data_value": "Takbir"},
           {"id": 3, "data_key": "email", "data_value": "takbir@gmail.com"}
       ]
   }
   ```

---

Let me know if you need further assistance! 🚀
