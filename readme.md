
# Falcon Backend API
## User API
The User API provides endpoints to manage user-related functionalities. 
## API Reference
### User Signup 
This API endpoint allows users to create a new account by providing their basic information, including first name, last name, email address, contact number, and a strong password that meets specific criteria.
|![Static Badge](https://img.shields.io/badge/Method-POST-GREEN)| ``` /api/user/``` |
| :-------- | :------------------------- |

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `first_name` | `string` | **Required.** Your first name |
| `last_name` | `string` | **Required.** Your last name |
| `email`| `string`  | **Required.** Your Email |
| `contact_no`| `string`  | **Required.** Your contact no |
| `password`| `string`  |**Required.** Password should contain at least:<br>- One uppercase letter<br>- One lowercase letter<br>- One digit<br>- One special character (@$!%*#?&)<br>- Length between 8 and 15 characters  |

**Response**
|Data | Response Type     | Respnonse Message                |
|  :-------|  :------- | :------------------------- |
|Valid Data| ![Static Badge](https://img.shields.io/badge/SUCCESS-GREEN) | `{"message":"You have successfully signed up"}` |
|Duplicate| ![Static Badge](https://img.shields.io/badge/ERROR-red)| `{"error":"User with this email already exists"}` |
|Invalid Email| ![Static Badge](https://img.shields.io/badge/ERROR-red)| `{"error":"Invalid Email"}` |
|Invalid Passowrd| ![Static Badge](https://img.shields.io/badge/ERROR-red)| `{"error":"Invalid Password"}` |

**Example**
```http
{
    "first_name": "first_name",
    "last_name": "last_name",
    "email": "testemail@gmail.com",
    "contact_no": "1234123412",
    "password": "Password@12"
}
```
### User Login 
This API endpoint allows users to log in to their account by providing their registered email and password. Upon successful login, the user receives an access token that should be included in the headers of subsequent authenticated requests.
|![Static Badge](https://img.shields.io/badge/Method-POST-GREEN)| ``` /api/user/login/``` |
| :-------- | :------------------------- |

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `email`| `string`  | **Required.** Your Email |
| `password`| `string`  |**Required.** Your Password |

**Response**
|Data | Response Type     | Respnonse Message                |
|  :-------|  :------- | :------------------------- |
|Valid Data| ![Static Badge](https://img.shields.io/badge/SUCCESS-GREEN) | {"data": {<br>"refresh": "(refresh_token)",<br>"access": "(access_token)",<br>"User":{User info},<br>"Integration":{""},<br>"message":"Logged in successfully"} |
|Invalid Email| ![Static Badge](https://img.shields.io/badge/ERROR-red)| `{"error":"Invalid Email"}` |
|Invalid Passowrd| ![Static Badge](https://img.shields.io/badge/ERROR-red)| `{"error":"Invalid Password"}` |

**Example**
```http
{
    "email": "testemail@gmail.com",
    "password": "Password@12"
}
```
### User Update 
This API endpoint allows authenticated users to update their profile information. You can modify your first name, last name, and contact number.
|![Static Badge](https://img.shields.io/badge/Authenticated%20User-blue)|![Static Badge](https://img.shields.io/badge/Method-PATCH-yellow)| ``` /api/user/update/``` |
| :-------- | :-------- | :------------------------- |

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `first_name` | `string` | Your first name |
| `last_name` | `string` |  Your last name |
| `email`| `string`  |  Your Email |
| `contact_no`| `string`  | Your contact no |
| `password`| `string`  |Password should contain at least:<br>- One uppercase letter<br>- One lowercase letter<br>- One digit<br>- One special character (@$!%*#?&)<br>- Length between 8 and 15 characters  |
| `Bearer`| `Access token`  | **Required.** Your have to pass the access token in the authorization header which was received after login|

**Response**
|Data | Response Type     | Respnonse Message                |
|  :-------|  :------- | :------------------------- |
|Valid Data| ![Static Badge](https://img.shields.io/badge/SUCCESS-GREEN) | `{"message":"You have successfully updated your profile"}` |
|Invalid Email| ![Static Badge](https://img.shields.io/badge/ERROR-red)| `{"error":"Invalid Email"}` |
|Invalid Passowrd| ![Static Badge](https://img.shields.io/badge/ERROR-red)| `{"error":"Invalid Password"}` |

**Example**
```http
{
"first_name":"new_first_name",
}
```
### User Gdrive link 
This API endpoint allows authenticated users to upload the gdrive tokens.
|![Static Badge](https://img.shields.io/badge/Authenticated%20User-blue)|![Static Badge](https://img.shields.io/badge/Method-POST-GREEN)| ``` /api/user/gdrive/``` |
| :-------- | :-------- | :------------------------- |

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `gdrive_accesstoken` | `string` | **Required.** User gdrive access token |
| `gdrive_refreshtoken` | `string` | **Required.** User gdrive refresh token |
| `gdrive_expiry_time`| `string`  |  **Required.** User gdrive expiry time |
| `Bearer`| `Access token`  | **Required.** Your have to pass the access token in the authorization header which was received after login |

**Response**
|Data | Response Type     | Respnonse Message                |
|  :-------|  :------- | :------------------------- |
|Valid Data| ![Static Badge](https://img.shields.io/badge/SUCCESS-GREEN) | `{"message":"Gdrive linked successfully"}` |
|Token Missing| ![Static Badge](https://img.shields.io/badge/ERROR-red)| `{"error":"Access / Refresh token missing"}` |
|Expiry time missing| ![Static Badge](https://img.shields.io/badge/ERROR-red)| `{"error":"Expiry time is missing"}` |

**Example**
```http
{
"gdrive_accesstoken":"access_token",
"gdrive_refreshtoken":"refresh_token",
"gdrive_expiry_time":"expiry_time",
}
```
### User Get Gdrive Token
This API endpoint allows authenticated users to get the gdrive token.
|![Static Badge](https://img.shields.io/badge/Authenticated%20User-blue)|![Static Badge](https://img.shields.io/badge/Method-GET-blue)| ``` /api/user/gdrive/token/``` |
| :-------- | :-------- | :------------------------- |

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Bearer`| `Access token`  | **Required.** Your have to pass the access token in the authorization header which was received after login |

**Response**
| Response Type     | Respnonse Message                |
|  :------- | :------------------------- |
| ![Static Badge](https://img.shields.io/badge/SUCCESS-GREEN) | {"data":{<br>"gdrive_accesstoken":"access_token",<br>"gdrive_refreshtoken":"refresh_token",<br>"gdrive_expiry_time":"expiry_time",}<br>} |




