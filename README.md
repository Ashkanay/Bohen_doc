# Bohen Third-Party API Documentation

## Overview
This API allows third-party applications to integrate with Bohen by authenticating, retrieving city information, and creating orders.

### Base URL
```
https://api.kurdishbohen.com/api/v1
```

---

## 1. Authorization
### Endpoint
**POST** `/integrations/third-party/auth/token`

### Request Body
```json
{
    "client_name": "abdulla_barez",
    "client_secret": "46a9bf3d-8671-4ce0-809f-00ace479663f"
}
```

### Response
```json
{
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjbGllbnRfaWQiOjM1NywiY2xpZW50X25hbWUiOiJhYmR1bGxhX2JhcmV6IiwiY29tcGFueV9pZCI6MSwiZXhwIjoxNzM4MjM4MDAwfQ.PD4wZM5y_sZjLERQkSdxJyH2F4DDx_Z9OVkyWuDBaUs",
    "expires_in": 3600,
    "refresh_expires_in": 0,
    "token_type": "Bearer"
}
```

### Headers
- Content-Type: `application/json`

---

## 2. Get Cities
### Endpoint
**GET** `/integrations/third-party/cities?language=ku`

### Query Parameters
| Parameter   | Type   | Description                          | Required |
|------------|--------|--------------------------------------|----------|
| language   | string | Language code (e.g., `ku`, `ar`)   | Yes      |

### Response
```json
{
    "count": 3,
    "data": [
        {
            "id": 1,
            "name": "ھەولیەر"
        },
        {
            "id": 2,
            "name": "سلەیمانی"
        },
        {
            "id": 3,
            "name": "دەھوک"
        }
    ]
}
```

### Headers
- Authorization: `Bearer {access_token}`

---

## 3. Create an Order
### Endpoint
**POST** `/integrations/third-party/orders`

### Request Headers
- Authorization: `Bearer {access_token}`
- Content-Type: `application/json`

### Request Body
```json
{
    "client_name": "John Doe",
    "client_code": 12345,
    "client_phone_no": "123-456-7890",
    "delivery_city_id": 1,
    "item_quantity": 2,
    "customer_name": "Jane Doe",
    "customer_address": null,
    "customer_phone_no": "987-654-3210",
    "customer_phone_no2": null,
    "total_amount": 50000,
    "note": null
}
```

### Response
```json
{
    "id": 3523,
    "code": "0293b81f"
}
```

---

## Authentication & Security
- API requests must include a **valid access token** in the Authorization header.
- Tokens expire after `3600 seconds` (1 hour).
- Use the `/integrations/third-party/auth/token` endpoint to request a new token.

## Error Handling
| Status Code | Description |
|-------------|-------------|
| 200 OK      | Successful request |
| 400 Bad Request | Invalid input |
| 401 Unauthorized | Missing or invalid token |
| 403 Forbidden | No access rights |
| 500 Internal Server Error | Unexpected server error |

---

## Contact & Support
For further inquiries, please contact support at **support@kurdishbohen.com**.

