### API End Point

#### API 01: Mobile Number Login

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/01-mobno-login.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/01-mobno-login.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/mobno-login

:Header:
```javascript
{
    "Content-Type": "application/json"
}
```

:Request:
```javascript
{
    "mobno": "9798977767"
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```
### Sub Task (Primary)
- [ ] If Mobile Number exist in Database and [Status=2 or Status=3]
* - [ ] Return response status as 1. We can Navigate the screen to get password.
- [ ] If Mobile Number exist in Database and [Status=1]
* - [ ] Return response status will be 2. We can Navigate the screen to get OTP. 
* - [ ] Also API will send Generated OTP to respective mobile number. 
- [ ] If Mobile Number does not exist in Database we will throw 401 error 

### Sub Task (Secondary)
- [ ] Mobile Number Validation [10 numbers]
- [ ] Maximum OTP request for a mobile number is 3 [configurable] per day

------

#### API 02: Validate OTP and Set New Password

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/02-validate-otp-set-password.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/02-validate-otp-set-password.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/validate-otp-set-password

:Header:
```javascript
{
    "Content-Type": "application/json"
}
```

:Request:
```javascript
{
    "mobno": "979107099",
    "password": "Welcome123",
    "otp": "123456"
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```
### Sub Task (Primary)
- [ ] Mobile Number should exist in database and [status in 1,2,3]
- [ ] OTP Validation
- [ ] Store the password in db as password_hash and password_salt

### Sub Task (Secondary)
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]
- [ ] Password Validation

------

#### API 03: Login with Password

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/03-login-with-password.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/03-login-with-password.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/login

:Header:
```javascript
{
    "Content-Type": "application/json"
}
```

:Request:
```javascript
{
    "mobno": "9791079311",
    "password": "Welcome123",
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```

:Token:
```javascript
{
  "mobile": "9791070319",
  "iat": 1593658604,
  "exp": 1593676604,
  "role": "user"
}
```

### Sub Task (Primary)
- [ ] Mobile Number should exist in database and [status in 2,3]
- [ ] Check for Password Validity with hashed db password
- [ ] Return JWT Token with payload { mobno: 9791070990, role: user or admin or  }
- [ ] If invalid Mobile number or password then return Error Code 401: Invalid Login details

### Sub Task (Secondary)
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]

------

#### API 04: Payment

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/04-payment.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/04-payment.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/payment

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request
- [ ] Analysis needed. For test purpose we can make a entry in payment table

### Sub Task (Secondary)
- [ ] N/A

------

#### API 05: My Profile

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/05-my-profile.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/05-my-profile.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
GET | http://localhost/agro/api/user/myprofile

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
    "address": {
        "line1": "address line1",
        "line2": "address line2",
        "landmark": "landmark",
        "city": "city",
        "state": "state",
        "pin": "pin",
    },
    "pan": {
        "panno": "XXXXXXX78",
        "status": "Approved"
    },
    "address": {
        "proof_no": "XXX-XXXX-XX98",
        "status": "Approved",
    },
    "bank_details": {
        "acno": "XXXXXX56",
        "status": "Approved",
    }
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request
- [ ] Mask all the Id's
- [ ] Don't return document file url

### Sub Task (Secondary)
- [ ] My profile form data validation

------

#### API 05.01: My Profile :: Update Address

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/05_01-update-address.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/05_01-update-address.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/update-address

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Request:
```javascript
{
    "line1": "address line1",
    "line2": "address line2",
    "landmark": "landmark",
    "city": "city",
    "state": "state",
    "pin": "pin"
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request

### Sub Task (Secondary)
- [ ] My profile form data validation

------

#### API 05.02: My Profile :: Update Pan

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/05_02-update-pan.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/05_02-update-pan.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/update-pan

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Request:
```javascript
{
    "panno": "ALRRS9878",
    "panno_url": "..."
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request

### Sub Task (Secondary)
- [ ] My profile form data validation

------

#### API 05.03: My Profile :: Update Address Proof

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/05_03-update-address.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/05_03-update-address.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/update-addressproof

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Request:
```javascript
{
    "address_proof_type": "",
    "address_proof_no": "",
    "address_proof_url": ""
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request

### Sub Task (Secondary)
- [ ] My profile form data validation

------

#### API 05.04: My Profile :: Bank Details

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/05_04-update-bank.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/05_04-update-bank.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/update-bank

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Request:
```javascript
{
    "bank_cross_cheque_url": "",
    "passbook_leaf_url": "",
    "account_statement_url": "",
    "acno": "123456",
    "ifsc_code": "...",
    "branch": "",
    "city": ""
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request

### Sub Task (Secondary)
- [ ] My profile form data validation

------

#### API 05.05: Upload File

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/update

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Request:
```javascript
{
    "file_name": "",
    "file": ""
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok",
    "file_id": "35634653456345dfgdgdrg"
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request
- [ ] Upload the file and return the file upload id.
- [ ] Don't return the file upload url for security purpose.

### Sub Task (Secondary)
- [ ] My profile form data validation
- [ ] Resize Image to optimize size using NodeJS

------

#### API 06: Generate Referal

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/06-generate-referal.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/06-generate-referal.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
GET | http://localhost/agro/api/user/generate-referal

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Request:
```javascript
{
    "matrix": "A"
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok",
    "referal_code": "37857uefj83u58utfio340895ui930it"
}
```
### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request
- [ ] Mobile Number should exist in database and [status=3]
- [ ] Check for Matrix A is available
- [ ] Referal code is hashed with a combination of [mobno /_matrix eg: 9791070918A]

### Sub Task (Secondary)
- [x] No Task

------

#### API 07: View Transaction
GET: http://localhost/agro/api/user/view-tran

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok",
    "tran": {
        walletAmount: 500,
        list: [   
            { "dt":"12-JUL-2020", "desc": "Withdrawl", "cr": 0, "dr": 1000 },
            { "dt":"11-JUL-2020", "desc": "RAKESH Joined", "user_id": "23", "cr": 1000, "dr": 0 },
            { "dt":"10-JUL-2020", "desc": "Initial Wallet Credit", "cr": 500, "dr": 0 },
            { "dt":"10-JUL-2020", "desc": "Initial Payment", "cr": 0, "dr": 5000 }
        ]
    }
}
```
### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request

### Sub Task (Secondary)
- [x] No Task

------

#### API 08: Apply Withdrawl
POST: http://localhost/agro/api/user/apply-withdrawl

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Request:
```javascript
{
    "amount": "1000",
    "comments": "For Personal"
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request
- [ ] Check Withdrawl amount is available.
- [ ] Previous Withdrawal request should not be in pending.

### Sub Task (Secondary)
- [x] No Task

------

#### API 09: View Withdrawl
GET: http://localhost/agro/api/user/view-withdrawl

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok",
    "tran": [
        { "req_date": "15-JUL-2020", "req_amount": "1000", "req_status": "Pending", "comments": "" }
    ]
    
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request.
- [ ] Withdrawl request status will be Pending, Processed and Rejected.
- [ ] Previous Withdrawal request should not be in pending.

### Sub Task (Secondary)
- [x] No Task

------

#### API 10: Register with Referal Code

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/10-referal-registration.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/10-referal-registration.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/referal-registration

:Header:
```javascript
{
    "Content-Type": "application/json"
}
```

:Request:
```javascript
{
    "first_name": "Senthil", 
    "last_name": "Perumal",
    "email": "senthil@gmail.com",
    "mobno": "9791078777",
    "referal_code": "37857uefj83u58utfio340895ui930it",
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```
### Sub Task (Primary)
- [ ] Mobile Number should not exist in database and [status not in 1,2,3]
- [ ] Referal code should be valid and available for registration

### Sub Task (Secondary)
- [ ] First name, last name validation. Max Length: 50
- [ ] EMail Id Validation
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]
- [ ] Password Validation [Min Length 8] [Characters Allowed: A-Z a-z 0-0 _ -] [Must have one alphabet and one number]
- [ ] Validate Referal Code

------
