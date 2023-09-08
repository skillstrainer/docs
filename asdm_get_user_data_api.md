## ASDM Data API

**Endpoint:** _/get_asdm_user_data_

**Base Url:** “*https://adminapi.skillstrainer.in/api/<endpoint>*”

**Method:** POST

**Payload:**

```
{
    “secret”: <YOUR_SECRET_KEY>,
    "items_per_page": <ITEMS PER PAGE>,
    "page_index": <PAGE INDEX>
}
```

**Response:**
You will receive a Base64 encoded encrypted AES key against the "encrypted_aes_key" key which can be decrypted using the private key sent to you. The decrypted AES key can then be used to decrypt the Base64 encoded encrypted data against the "encrypted_data" key

```
{
  "data": {
    "encrypted_aes_key": <BASE64_ENCODED_AES_KEY>,
    "encrypted_data": <BASE64_ENCODED_DATA>
  },
  "success": true
}
```
