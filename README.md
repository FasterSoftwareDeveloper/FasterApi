### **API Read Function Documentation**  
**Base URL**: `https://fritemp.free.nf/api-v1/fasterread.php`  
**Authentication**: Token-based (generated via `/fastertokengenerator.php`).  

---

### **1. Show All Tables in the Database**  
**Endpoint**:  
`GET /fasterread.php?token={your-token}`  

**Example**:  
```url
https://fritemp.free.nf/api-v1/fasterread.php?token=ndjdbdbjkel572827
```  

**Response**:  
```json
{
    "status": "success",
    "tables": ["exampletablekey", "users", "products"]
}
```  

**Errors**:  
- `401 Unauthorized`: Invalid/missing token.  
- `404 Not Found`: No tables exist.  

---

### **2. Show All Data from a Specific Table**  
**Endpoint**:  
`GET /fasterread.php?tableKey={table-name}&token={your-token}`  

**Parameters**:  
- `tableKey`: Name of the table (e.g., `exampletablekey`).  

**Example**:  
```url
https://fritemp.free.nf/api-v1/fasterread.php?tableKey=exampletablekey&token=ndjdbdbjkel572827
```  

**Response**:  
```json
{
    "status": "success",
    "table": "exampletablekey",
    "data": [
        {"id": 1, "data_key": "testKey", "data_value": "hiiii"},
        {"id": 2, "data_key": "test", "data_value": "hello"}
    ]
}
```  

**Errors**:  
- `401 Unauthorized`: Invalid token.  
- `404 Not Found`: Table does not exist.  

---

### **3. Show Values from a Specific Column**  
**Endpoint**:  
`GET /fasterread.php?tableKey={table-name}&key={column-name}&token={your-token}`  

**Parameters**:  
- `tableKey`: Name of the table (e.g., `exampletablekey`).  
- `key`: Name of the column (e.g., `data_key`).  

**Example**:  
```url
https://fritemp.free.nf/api-v1/fasterread.php?tableKey=exampletablekey&key=data_value&token=ndjdbdbjkel572827
```  

**Response**:  
```json
{
    "status": "success",
    "table": "exampletablekey",
    "column": "data_value",
    "data": ["hiiii", "hello"]
}
```  

**Errors**:  
- `401 Unauthorized`: Invalid token.  
- `404 Not Found`: Column/table does not exist.  

---

### **4. Show All Tables + Column Data (Entire Database)**  
**Endpoint**:  
`GET /fasterread.php?all&token={your-token}`  

**Example**:  
```url
https://fritemp.free.nf/api-v1/fasterread.php?all&token=ndjdbdbjkel572827
```  

**Response**:  
```json
{
    "status": "success",
    "data": {
        "exampletablekey": [
            {"id": 1, "data_key": "testKey", "data_value": "hiiii"},
            {"id": 2, "data_key": "test", "data_value": "hello"}
        ],
        "users": [
            {"id": 1, "name": "John", "email": "john@example.com"}
        ]
    }
}
```  

**Errors**:  
- `401 Unauthorized`: Invalid token.  

---

### **Token Generation**  
**Endpoint**:  
```url
https://fritemp.free.nf/api-v1/fastertokengenerator.php
```  

**Response**:  
```json
{
    "status": "success",
    "token": "ndjdbdbjkel572827"
}
```  

**Notes**:  
- Tokens expire after **5 minutes** and are **one-time use**.  
- Always use HTTPS for secure requests.  

---

### **Error Codes**  
| Code | Message                          | Description                          |  
|------|----------------------------------|--------------------------------------|  
| 401  | `Access denied. Invalid token`   | Token missing, expired, or invalid.  |  
| 404  | `Table not found`                | Table/column does not exist.         |  
| 500  | `Internal server error`          | Database connection/query failure.   |  

---

### **Quick Start Guide**  
1. **Generate a Token**:  
   ```url
   https://fritemp.free.nf/api-v1/fastertokengenerator.php
   ```  
   Copy the token from the response.  

2. **Fetch Data**:  
   Use the token in your requests (e.g., `?token=ndjdbdbjkel572827`).  

3. **Example**:  
   ```url
   https://fritemp.free.nf/api-v1/fasterread.php?tableKey=exampletablekey&token=ndjdbdbjkel572827
   ```  

---

Let me know if you need further clarifications! 🚀
