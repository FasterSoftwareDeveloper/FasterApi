### **API Token Generator Documentation**  
**Base URL**: `https://{your_domain}/api-v{api_version}/fastertokengenerator.php`  

This API generates a secure token that expires after **5 minutes**. The token can be used for authentication in other API endpoints. Expired tokens are automatically removed from the database.

---

### **Endpoint**
```
GET /fastertokengenerator.php
```

---

### **Response**
The API returns a JSON response with the following fields:

| Field         | Description                          | Example Value                     |
|---------------|--------------------------------------|-----------------------------------|
| `status`      | Status of the request (`success`).   | `"success"`                       |
| `token`       | The generated secure token.          | `"ndjdbdbjkel572827"`             |
| `expiry_time` | The expiry time of the token.        | `"2023-10-15 12:34:56"`           |

**Example Response**:
```json
{
    "status": "success",
    "token": "ndjdbdbjkel572827",
    "expiry_time": "2023-10-15 12:34:56"
}
```

---

### **How It Works**

1. **Auto-Create Table**:
   - If the `api_tokens` table does not exist, it is created automatically with the following structure:
     ```sql
     CREATE TABLE api_tokens (
         id INT AUTO_INCREMENT PRIMARY KEY,
         token VARCHAR(64) NOT NULL,
         expiry_time DATETIME NOT NULL
     );
     ```

2. **Delete Expired Tokens**:
   - Before generating a new token, the API deletes all tokens that have expired (i.e., `expiry_time` is older than the current time).

3. **Generate Token**:
   - A secure token is generated using `bin2hex(random_bytes(16))`.

4. **Set Expiry Time**:
   - The token’s expiry time is set to **5 minutes** from the current time.

5. **Store Token**:
   - The token and its expiry time are stored in the `api_tokens` table.

6. **Return Token**:
   - The token and its expiry time are returned in the JSON response.

---

### **Error Handling**

| Code | Message                          | Description                          |  
|------|----------------------------------|--------------------------------------|  
| 500  | `Failed to create api_tokens table` | Table creation failed.               |  
| 500  | `Failed to delete expired tokens` | Expired token cleanup failed.        |  
| 500  | `Error generating token`         | Token insertion failed.              |  

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
       "token": "ndjdbdbjkel572827",
       "expiry_time": "2023-10-15 12:34:56"
   }
   ```

2. **Use Token**:
   - Use the generated token in other API endpoints for authentication.  
   Example:
   ```url
   https://{your_domain}/api-v1/fasterread.php?tableKey=exampletablekey&token=ndjdbdbjkel572827
   ```

3. **Token Expiry**:
   - After 5 minutes, the token will expire and be automatically deleted from the database.

---

### **Testing the Endpoint**

#### **1. Generate Token**
**Endpoint**:  
```url
https://{your_domain}/api-v1/fastertokengenerator.php
```  

**Response**:  
```json
{
    "status": "success",
    "token": "ndjdbdbjkel572827",
    "expiry_time": "2023-10-15 12:34:56"
}
```

#### **2. Verify Expired Tokens**
- After 5 minutes, the token will expire and be automatically deleted from the database.

#### **3. Verify Table Cleanup**
- Use a tool like phpMyAdmin or run the following SQL query to verify that expired tokens are deleted:
  ```sql
  SELECT * FROM api_tokens;
  ```

---

### **Notes**

- **Token Expiry**: Tokens expire after **5 minutes** and are **one-time use**.
- **Auto-Cleanup**: Expired tokens are automatically removed from the database.
- **One-Time Response**: The token and its expiry time are returned in a single response.
