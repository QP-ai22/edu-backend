# API Documentation

## Base URL

- `http://localhost:5000/api`

## Postman Setup

Create a Postman environment with these variables:

- `base_url`: `http://localhost:5000/api`
- `access_token`: *(filled after login)*
- `refresh_token`: *(optional if using cookies manually)*

### Common headers

- `Content-Type`: `application/json`
- `Authorization`: `Bearer {{access_token}}` *(for authenticated requests)*

> Postman note: the `refresh_token` endpoint reads the refresh token from the cookie `refreshtoken`. Use Postman's cookie jar, or set the header `Cookie: refreshtoken={{refresh_token}}` if needed.

---

## Authentication Endpoints

### Register User

- Method: `POST`
- URL: `{{base_url}}/register`
- Auth: no

#### Request Body

```json
{
  "fullname": "Jane Doe",
  "username": "janedoe",
  "email": "jane@example.com",
  "password": "password123",
  "gender": "female"
}
```

#### Successful Response

```json
{
  "msg": "Register Success!",
  "access_token": "<jwt>",
  "user": {
    "_id": "...",
    "fullname": "Jane Doe",
    "username": "janedoe",
    "email": "jane@example.com",
    "gender": "female",
    "avatar": "",
    "role": "user",
    "mobile": "",
    "address": "",
    "story": "",
    "website": "",
    "followers": [],
    "following": [],
    "saved": [],
    "createdAt": "...",
    "updatedAt": "..."
  }
}
```

### Login User

- Method: `POST`
- URL: `{{base_url}}/login`
- Auth: no

#### Request Body

```json
{
  "email": "jane@example.com",
  "password": "password123"
}
```

#### Successful Response

```json
{
  "msg": "Login Success!",
  "access_token": "<jwt>",
  "user": {
    "_id": "...",
    "fullname": "Jane Doe",
    "username": "janedoe",
    "email": "jane@example.com",
    "gender": "female",
    "avatar": "",
    "role": "user",
    "mobile": "",
    "address": "",
    "story": "",
    "website": "",
    "followers": [],
    "following": [],
    "saved": [],
    "createdAt": "...",
    "updatedAt": "..."
  }
}
```

### Logout User

- Method: `POST`
- URL: `{{base_url}}/logout`
- Auth: no

#### Successful Response

```json
{
  "msg": "Logged out!"
}
```

### Refresh Access Token

- Method: `POST`
- URL: `{{base_url}}/refresh_token`
- Auth: cookie-based refresh token

#### Successful Response

```json
{
  "access_token": "<jwt>",
  "user": { ... }
}
```

---

## User Endpoints

### Search Users

- Method: `GET`
- URL: `{{base_url}}/search?username=jane`
- Auth: yes

#### Response

```json
{
  "users": [
    {
      "fullname": "Jane Doe",
      "username": "janedoe",
      "avatar": ""
    }
  ]
}
```

### Get User by ID

- Method: `GET`
- URL: `{{base_url}}/user/:id`
- Auth: yes

#### Response

```json
{
  "user": {
    "_id": "...",
    "fullname": "Jane Doe",
    "username": "janedoe",
    "email": "jane@example.com",
    "gender": "female",
    "avatar": "",
    "role": "user",
    "mobile": "",
    "address": "",
    "story": "",
    "website": "",
    "followers": [...],
    "following": [...],
    "saved": [...],
    "createdAt": "...",
    "updatedAt": "..."
  }
}
```

### Update Logged-in User

- Method: `PATCH`
- URL: `{{base_url}}/user`
- Auth: yes

#### Request Body

```json
{
  "avatar": "https://example.com/avatar.jpg",
  "fullname": "Jane B. Doe",
  "mobile": "1234567890",
  "address": "123 Street",
  "story": "Hello world!",
  "website": "https://janedoe.com",
  "gender": "female"
}
```

#### Successful Response

```json
{
  "msg": "Update Success!"
}
```

### Follow User

- Method: `PATCH`
- URL: `{{base_url}}/user/:id/follow`
- Auth: yes

#### Successful Response

```json
{
  "newUser": { ... }
}
```

### Unfollow User

- Method: `PATCH`
- URL: `{{base_url}}/user/:id/unfollow`
- Auth: yes

#### Successful Response

```json
{
  "newUser": { ... }
}
```

### Suggested Users

- Method: `GET`
- URL: `{{base_url}}/suggestionsUser?num=10`
- Auth: yes

#### Response

```json
{
  "users": [...],
  "result": 10
}
```

---

## Post Endpoints

### Create Post

- Method: `POST`
- URL: `{{base_url}}/posts`
- Auth: yes

#### Request Body

```json
{
  "content": "This is a new post",
  "images": [
    {
      "url": "https://example.com/photo.jpg",
      "public_id": "abc123"
    }
  ]
}
```

#### Successful Response

```json
{
  "msg": "Created Post!",
  "newPost": { ... }
}
```

### Get Timeline Posts

- Method: `GET`
- URL: `{{base_url}}/posts?page=1&limit=9`
- Auth: yes

#### Response

```json
{
  "msg": "Success!",
  "result": 9,
  "posts": [ ... ]
}
```

### Get Post by ID

- Method: `GET`
- URL: `{{base_url}}/post/:id`
- Auth: yes

#### Response

```json
{
  "post": { ... }
}
```

### Update Post

- Method: `PATCH`
- URL: `{{base_url}}/post/:id`
- Auth: yes

#### Request Body

```json
{
  "content": "Updated content",
  "images": [ ... ]
}
```

#### Successful Response

```json
{
  "msg": "Updated Post!",
  "newPost": { ... }
}
```

### Delete Post

- Method: `DELETE`
- URL: `{{base_url}}/post/:id`
- Auth: yes

#### Successful Response

```json
{
  "msg": "Deleted Post!",
  "newPost": { ... }
}
```

### Like Post

- Method: `PATCH`
- URL: `{{base_url}}/post/:id/like`
- Auth: yes

#### Successful Response

```json
{
  "msg": "Liked Post!"
}
```

### Unlike Post

- Method: `PATCH`
- URL: `{{base_url}}/post/:id/unlike`
- Auth: yes

#### Successful Response

```json
{
  "msg": "UnLiked Post!"
}
```

### Get User Posts

- Method: `GET`
- URL: `{{base_url}}/user_posts/:id?page=1&limit=9`
- Auth: yes

#### Response

```json
{
  "posts": [ ... ],
  "result": 3
}
```

### Discover Posts

- Method: `GET`
- URL: `{{base_url}}/post_discover?num=9`
- Auth: yes

#### Response

```json
{
  "msg": "Success!",
  "result": 9,
  "posts": [ ... ]
}
```

### Save Post

- Method: `PATCH`
- URL: `{{base_url}}/savePost/:id`
- Auth: yes

#### Successful Response

```json
{
  "msg": "Saved Post!"
}
```

### Unsave Post

- Method: `PATCH`
- URL: `{{base_url}}/unSavePost/:id`
- Auth: yes

#### Successful Response

```json
{
  "msg": "unSaved Post!"
}
```

### Get Saved Posts

- Method: `GET`
- URL: `{{base_url}}/getSavePosts?page=1&limit=9`
- Auth: yes

#### Response

```json
{
  "savePosts": [ ... ],
  "result": 5
}
```

---

## Comment Endpoints

### Create Comment

- Method: `POST`
- URL: `{{base_url}}/comment`
- Auth: yes

#### Request Body

```json
{
  "postId": "<post_id>",
  "content": "Nice post!",
  "tag": { "_id": "...", "username": "john" },
  "reply": "<comment_id>",
  "postUserId": "<post_owner_id>"
}
```

#### Successful Response

```json
{
  "newComment": { ... }
}
```

### Update Comment

- Method: `PATCH`
- URL: `{{base_url}}/comment/:id`
- Auth: yes

#### Request Body

```json
{
  "content": "Updated comment text"
}
```

#### Successful Response

```json
{
  "msg": "Update Success!"
}
```

### Like Comment

- Method: `PATCH`
- URL: `{{base_url}}/comment/:id/like`
- Auth: yes

#### Successful Response

```json
{
  "msg": "Liked Comment!"
}
```

### Unlike Comment

- Method: `PATCH`
- URL: `{{base_url}}/comment/:id/unlike`
- Auth: yes

#### Successful Response

```json
{
  "msg": "UnLiked Comment!"
}
```

### Delete Comment

- Method: `DELETE`
- URL: `{{base_url}}/comment/:id`
- Auth: yes

#### Successful Response

```json
{
  "msg": "Deleted Comment!"
}
```

---

## Data Schemas

### User Schema

| Field | Type | Notes |
|---|---|---|
| `_id` | ObjectId | Unique ID |
| `fullname` | String | required |
| `username` | String | required, unique |
| `email` | String | required, unique |
| `password` | String | hashed |
| `avatar` | String | optional |
| `role` | String | default `user` |
| `gender` | String | default `male` |
| `mobile` | String | optional |
| `address` | String | optional |
| `story` | String | optional |
| `website` | String | optional |
| `followers` | [ObjectId] | references `user` |
| `following` | [ObjectId] | references `user` |
| `saved` | [ObjectId] | saved post ids |
| `createdAt`, `updatedAt` | Date | timestamps |

### Post Schema

| Field | Type | Notes |
|---|---|---|
| `_id` | ObjectId | Unique ID |
| `content` | String | optional |
| `images` | Array | required |
| `likes` | [ObjectId] | references `user` |
| `comments` | [ObjectId] | references `comment` |
| `user` | ObjectId | references `user` |
| `createdAt`, `updatedAt` | Date | timestamps |

### Comment Schema

| Field | Type | Notes |
|---|---|---|
| `_id` | ObjectId | Unique ID |
| `content` | String | required |
| `tag` | Object | optional |
| `reply` | ObjectId | optional, reply parent comment |
| `likes` | [ObjectId] | references `user` |
| `user` | ObjectId | references `user` |
| `postId` | ObjectId | referenced post |
| `postUserId` | ObjectId | post owner |
| `createdAt`, `updatedAt` | Date | timestamps |

---

## Postman File Schema

This repository includes a Postman collection file: `postman_collection.json`.

Import it into Postman to quickly load all routes, headers, and sample bodies.

- `base_url` variable is set to `http://localhost:5000/api`
- `Authorization` header uses `Bearer {{access_token}}`

### Recommended workflow

1. Register a new user with `/register`
2. Login with `/login`
3. Copy the returned `access_token` into Postman environment
4. Send protected requests with the Authorization header
5. Use `/refresh_token` to obtain a new access token when needed
