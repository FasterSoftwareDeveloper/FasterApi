### **API Authentication System Documentation**  
**Base URL**: `https://{your_domain}/api-v{api_version}/fasterauthentication.php`  

This API provides **sign-up** and **sign-in** functionality for users. It uses a **token-based authentication system** and stores user data securely in a database.

---

### **Endpoints**

#### **1. Sign Up**  
Create a new user account.

**Endpoint**:  
```url
GET /fasterauthentication.php?action=signup&email={email}&password={password}&token={on_time_token}
```

**Parameters**:  
| Parameter | Description                          | Example Value               |
|-----------|--------------------------------------|-----------------------------|
| `action`  | Must be set to `signup`.             | `signup`                    |
| `email`   | User’s email address.                | `user@example.com`          |
| `password`| User’s password.                     | `securepassword123`         |
| `token`   | Your secure token (optional).        | `ndjdbdbjkel572827`         |

**Response**:  
```json
{
    "status": "success",
    "uid": "550e8400-e29b-41d4-a716-446655440000",
    "email": "user@example.com",
    "created_at": "2023-10-15 12:34:56"
}
```

**Errors**:  
| Code | Message                          | Description                          |  
|------|----------------------------------|--------------------------------------|  
| 400  | `Email and password are required`| Missing email or password.           |  
| 409  | `Email already exists`           | Email is already registered.         |  
| 500  | `Internal server error`          | Database connection/query failure.   |  

---

#### **2. Sign In**  
Authenticate an existing user.

**Endpoint**:  
```url
GET /fasterauthentication.php?action=signin&email={email}&password={password}&token={on_time_token}
```

**Parameters**:  
| Parameter | Description                          | Example Value               |
|-----------|--------------------------------------|-----------------------------|
| `action`  | Must be set to `signin`.             | `signin`                    |
| `email`   | User’s email address.                | `user@example.com`          |
| `password`| User’s password.                     | `securepassword123`         |
| `token`   | Your secure token (optional).        | `ndjdbdbjkel572827`         |

**Response**:  
```json
{
    "status": "success",
    "uid": "550e8400-e29b-41d4-a716-446655440000",
    "email": "user@example.com",
    "created_at": "2023-10-15 12:34:56"
}
```

**Errors**:  
| Code | Message                          | Description                          |  
|------|----------------------------------|--------------------------------------|  
| 400  | `Email and password are required`| Missing email or password.           |  
| 404  | `User not found`                 | Email is not registered.             |  
| 401  | `Invalid password`               | Incorrect password.                  |  
| 500  | `Internal server error`          | Database connection/query failure.   |  

---

### **Database Table Structure**

The `users` table is automatically created if it doesn’t exist. It has the following structure:

| Column Name      | Data Type        | Description                          |
|------------------|------------------|--------------------------------------|
| `uid`            | VARCHAR(36)      | Unique user ID (auto-generated UUID).|
| `email`          | VARCHAR(255)     | User’s email address (unique).       |
| `password`       | VARCHAR(255)     | Hashed password.                     |
| `created_at`     | DATETIME         | Account creation time.               |

---

### **How It Works**

1. **Sign Up**:
   - The API checks if the email is already registered.
   - If not, it generates a unique `uid`, hashes the password, and stores the user data in the `users` table.

2. **Sign In**:
   - The API verifies the email and password.
   - If the credentials are valid, it returns the user’s details.

3. **Auto-Create Table**:
   - If the `users` table doesn’t exist, it is created automatically.

---

### **Testing the Endpoint**

#### **1. Sign Up**
**Request**:  
```url
https://fritemp.free.nf/api-v1/fasterauthentication.php?action=signup&email=user@example.com&password=securepassword123&token=ndjdbdbjkel572827
```  

**Response**:  
```json
{
    "status": "success",
    "uid": "550e8400-e29b-41d4-a716-446655440000",
    "email": "user@example.com",
    "created_at": "2023-10-15 12:34:56"
}
```

#### **2. Sign In**
**Request**:  
```url
https://fritemp.free.nf/api-v1/fasterauthentication.php?action=signin&email=user@example.com&password=securepassword123&token=ndjdbdbjkel572827
```  

**Response**:  
```json
{
    "status": "success",
    "uid": "550e8400-e29b-41d4-a716-446655440000",
    "email": "user@example.com",
    "created_at": "2023-10-15 12:34:56"
}
```

---

### **Error Handling**

| Code | Message                          | Description                          |  
|------|----------------------------------|--------------------------------------|  
| 400  | `Email and password are required`| Missing email or password.           |  
| 409  | `Email already exists`           | Email is already registered.         |  
| 404  | `User not found`                 | Email is not registered.             |  
| 401  | `Invalid password`               | Incorrect password.                  |  
| 500  | `Internal server error`          | Database connection/query failure.   |  

---

### **Quick Start Guide**

1. **Sign Up**:
   ```url
   https://{your_domain}/api-v1/fasterauthentication.php?action=signup&email=user@example.com&password=securepassword123&token=ndjdbdbjkel572827
   ```

2. **Sign In**:
   ```url
   https://{your_domain}/api-v1/fasterauthentication.php?action=signin&email=user@example.com&password=securepassword123&token=ndjdbdbjkel572827
   ```

---

### **Notes**

- **Password Hashing**: Passwords are securely hashed using `password_hash()` and verified using `password_verify()`.
- **Unique UID**: Each user is assigned a unique UUID (`uid`) during sign-up.
- **Auto-Create Table**: The `users` table is created automatically if it doesn’t exist.
- **Token Usage**: The `token` parameter is included in the URL for authentication (you can validate it using your existing token system).
