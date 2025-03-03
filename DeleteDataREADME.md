### **API Delete Function Documentation**  
**Base URL**: `https://{your_domain}/api-v{api_version}/fasterdelete.php`  

This API allows you to delete **rows**, **tables**, or **all tables** from the database. It supports deleting single or multiple items at once.

---

### **Endpoints**

#### **1. Delete Rows by Key**
Delete rows from a table where `data_key` matches the provided keys.

**Endpoint**:  
`GET /fasterdelete.php?tableKey={table_name}&deleteKey={key1,key2}&token={on_time_token}`  

**Parameters**:  
- `tableKey`: The name of the table (e.g., `exampletablekey`).  
- `deleteKey`: Comma-separated list of keys to delete (e.g., `test,op`).  
- `token`: Your secure token (e.g., `ndjdbdbjkel572827`).  

**Example**:  
```url
https://{your_domain}/api-v1/fasterdelete.php?tableKey=exampletablekey&deleteKey=test,op&token=ndjdbdbjkel572827
```  

**Response**:  
```json
[
    {"key":"test","status":"success","message":"Row deleted successfully"},
    {"key":"op","status":"success","message":"Row deleted successfully"}
]
```  

**Errors**:  
- `401 Unauthorized`: Invalid/missing token.  
- `404 Not Found`: Table or key does not exist.  
- `500 Internal Server Error`: Database connection/query failure.  

---

#### **2. Delete Tables**
Delete one or more tables from the database.

**Endpoint**:  
`GET /fasterdelete.php?Tabledelete={table1,table2}&token={on_time_token}`  

**Parameters**:  
- `Tabledelete`: Comma-separated list of tables to delete (e.g., `exampletablekey,users`).  
- `token`: Your secure token (e.g., `ndjdbdbjkel572827`).  

**Example**:  
```url
https://{your_domain}/api-v1/fasterdelete.php?Tabledelete=exampletablekey,users&token=ndjdbdbjkel572827
```  

**Response**:  
```json
[
    {"table":"exampletablekey","status":"success","message":"Table deleted successfully"},
    {"table":"users","status":"success","message":"Table deleted successfully"}
]
```  

**Errors**:  
- `401 Unauthorized`: Invalid/missing token.  
- `404 Not Found`: Table does not exist.  
- `500 Internal Server Error`: Database connection/query failure.  

---

#### **3. Delete All Tables**
Delete all tables from the database.

**Endpoint**:  
`GET /fasterdelete.php?allDelete&token={on_time_token}`  

**Parameters**:  
- `allDelete`: Indicates that all tables should be deleted.  
- `token`: Your secure token (e.g., `ndjdbdbjkel572827`).  

**Example**:  
```url
https://{your_domain}/api-v1/fasterdelete.php?allDelete&token=ndjdbdbjkel572827
```  

**Response**:  
```json
[
    {"table":"exampletablekey","status":"success","message":"Table deleted successfully"},
    {"table":"users","status":"success","message":"Table deleted successfully"}
]
```  

**Errors**:  
- `401 Unauthorized`: Invalid/missing token.  
- `404 Not Found`: No tables exist in the database.  
- `500 Internal Server Error`: Database connection/query failure.  

---

### **How It Works**

1. **Delete Rows**:
   - The API deletes rows from the specified table where `data_key` matches the provided keys.

2. **Delete Tables**:
   - The API deletes the specified tables from the database.

3. **Delete All Tables**:
   - The API deletes all tables from the database.

---

### **Error Codes**

| Code | Message                          | Description                          |  
|------|----------------------------------|--------------------------------------|  
| 401  | `Access denied. Invalid token`   | Token missing, expired, or invalid.  |  
| 404  | `Table/Key not found`            | Table or key does not exist.         |  
| 500  | `Internal server error`          | Database connection/query failure.   |  

---

### **Quick Start Guide**

1. **Delete Rows**:
   ```url
   https://{your_domain}/api-v1/fasterdelete.php?tableKey=exampletablekey&deleteKey=test,op&token=ndjdbdbjkel572827
   ```

2. **Delete Tables**:
   ```url
   https://{your_domain}/api-v1/fasterdelete.php?Tabledelete=exampletablekey,users&token=ndjdbdbjkel572827
   ```

3. **Delete All Tables**:
   ```url
   https://{your_domain}/api-v1/fasterdelete.php?allDelete&token=ndjdbdbjkel572827
   ```

---

### **Example Workflow**

#### **1. Delete Rows**
**Request**:  
```url
https://{your_domain}/api-v1/fasterdelete.php?tableKey=exampletablekey&deleteKey=test,op&token=ndjdbdbjkel572827
```  

**Response**:  
```json
[
    {"key":"test","status":"success","message":"Row deleted successfully"},
    {"key":"op","status":"success","message":"Row deleted successfully"}
]
```

#### **2. Delete Tables**
**Request**:  
```url
https://{your_domain}/api-v1/fasterdelete.php?Tabledelete=exampletablekey,users&token=ndjdbdbjkel572827
```  

**Response**:  
```json
[
    {"table":"exampletablekey","status":"success","message":"Table deleted successfully"},
    {"table":"users","status":"success","message":"Table deleted successfully"}
]
```

#### **3. Delete All Tables**
**Request**:  
```url
https://{your_domain}/api-v1/fasterdelete.php?allDelete&token=ndjdbdbjkel572827
```  

**Response**:  
```json
[
    {"table":"exampletablekey","status":"success","message":"Table deleted successfully"},
    {"table":"users","status":"success","message":"Table deleted successfully"}
]
```

---

### **Notes**

- **Token Expiry**: Tokens expire after **5 minutes** and are **one-time use**.
- **Auto-Cleanup**: Expired tokens are automatically removed from the database.
- **One-Time Response**: The token and its expiry time are returned in a single response.
