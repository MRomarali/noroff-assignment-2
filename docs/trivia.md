# Trivia API

## Open Endpoints
Open endpoints do not require authentication.

### Trivia Users `GET /trivia`
#### Sample Response
```json
[
  {
    "id": 1,
    "username": "dewaldels",
    "highScore": 0
  }
]
```

### Trivia Users `GET /trivia?username=<query>`
You can filter results to get a specific user from the API. It uses the standard URL Query String syntax. 

> **e.g.** Search for a user with username `mega-mind` you can make a `GET` request to `apiUrl/trivia?username=mega-mind`.
> 
> This will return an array of **all users** that match the username of mega-mind.

#### Sample Code
```javascript
const apiURL = 'your-api-url-goes-here'
const username = 'mega-mind'

fetch(`${apiURL}/trivia?username=${username}`)
    .then(response => response.json())
    .then(results => {
        // results will be an array of users that match the username of mega-mind.
    })
    .catch(error => {
    })
```

## Protected Endpoints

Protected endpoints require the X-API-Key header with the API key as value.

### 🔒 Trivia Users `POST /trivia`

#### Sample Code
```javascript
const apiURL = 'your-api-url-goes-here'
const apiKey = 'your-public-api-key-goes-here'

fetch(`${apiURL}/trivia`, {
        method: 'POST',
        headers: {
            'X-API-Key': apiKey,
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ 
            username: 'the-trivia-master', 
            highScore: 0 
        })
    })
    .then(response => {
      if (!response.ok) {
        throw new Error('Could not create new user')
      }
      return response.json()
    })
    .then(newUser => {
      // newUser is the new user with an id
    })
    .catch(error => {
    })
```

#### Sample response
```json
{
    "id": 2,
    "username": "the-trivia-master",
    "highScore": 0
}
```

### 🔒 Trivia Users `PATCH /trivia`
The `PATCH` method is used to update a single record

#### Sample Code
```javascript
const apiURL = 'your-api-url-goes-here'
const apiKey = 'your-public-api-key-goes-here'
const userId = 1 // Update user with id 1

fetch(`${apiURL}/trivia/${userId}`, {
        method: 'PATCH', // NB: Set method to PATCH
        headers: {
            'X-API-Key': apiKey,
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            // Provide new highScore to add to user with id 1
            highScore: 100  
        })
    })
    .then(response => {
      if (!response.ok) {
        throw new Error('Could not update high score')
      }
      return response.json()
    })
    .then(updatedUser => {
      // updatedUser is the user with the Patched data
    })
    .catch(error => {
    })
```