# Social Share for Avazoo App

## Endpoints

Below is a list of available endpoints and how to use them:

### GET `/auth/twitter`

**Purpose:**  
Generate a Twitter OAuth2 authentication URL.

**Response (JSON):**
{
"url": "https://api.twitter.com/..."
}

**Description:**  
This endpoint creates a Twitter OAuth2 URL and saves the `codeVerifier` and `state` in the session. Redirect your user to the URL to begin the Twitter login process.

---

### GET `/callback`

**Purpose:**  
Handle Twitter OAuth2 callback.

**Query Parameters:**
- `code` (string): The authorization code provided by Twitter.
- `state` (string): The state parameter to verify against the session.

**Description:**  
This endpoint exchanges the OAuth2 code for an access token. On success, it stores the access token (and refresh token) in the session and redirects the user to `/callback.html?token=...`.

---

### GET `/auth/linkedin`

**Purpose:**  
Generate a LinkedIn OAuth2 authentication URL.

**Response (JSON):**
{
"url": "https://www.linkedin.com/oauth/v2/authorization?...&state=exampleState"
}


**Description:**  
This endpoint creates a LinkedIn OAuth2 URL with the necessary scopes and returns it as JSON. A random `state` value is stored in the session for later verification.

---

### GET `/callback/linkedin`

**Purpose:**  
Handle LinkedIn OAuth2 callback.

**Query Parameters:**
- `code` (string): The authorization code provided by LinkedIn.
- `state` (string): The state parameter to verify against the session.

**Description:**  
This endpoint exchanges the provided authorization code for an access token with LinkedIn. The access token is then stored in the session, and the user is redirected to `/callback.html?token=...`.

---

### POST `/api/tweet`

**Purpose:**  
Post a tweet on behalf of the authenticated Twitter user.

**Request Body (JSON):**
{
"title": "Your tweet content here"
}

**Response:**  
Returns the Twitter API response object for the posted tweet.

**Description:**  
Ensure the user has authenticated via `/auth/twitter`. This endpoint uses the Twitter access token stored in the session to post the tweet.

---

### POST `/api/linkedin`

**Purpose:**  
Create a LinkedIn UGC post.

**Request Body (JSON):**
{
"title": "Title of the post",
"description": "Description of the article",
"url": "https://example.com/article"
}

**Response:**  
Returns a JSON object indicating the success and details of the LinkedIn post.

**Description:**  
Ensure the user has authenticated via `/auth/linkedin`. The endpoint uses the LinkedIn access token stored in the session and posts on LinkedIn using their UGC API.
