# Lost In Translation

## Open Endpoints
Open endpoints do not require authentication.

### Lost in Translation Users `GET /translations`
#### Sample Response
```json
[
  {
    "id": 1,
    "username": "dewaldels",
    "translations": []
  }
]
```

### Translation Users `GET /translations?username=<query>`
You can filter results to get a specific user from the API. It uses the standard URL Query String syntax.

> **e.g.** Search for a user with username `victor` you can make a `GET` request to `apiUrl/trivia?username=victor`.
>
> This will return an array of **all users** that match the username of victor.

#### Sample Code
```javascript
const apiURL = 'your-api-url-goes-here'
const username = 'victor'

fetch(`${apiURL}/translations?username=${username}`)
    .then(response => response.json())
    .then(results => {
        // results will be an array of users that match the username of victor.
    })
    .catch(error => {
    })
```

## Protected Endpoints

Protected endpoints require the X-API-Key header with the API key as value.

### 🔒 Lost in Translation Users `POST /translations`

#### Sample Code
```javascript
const apiURL = 'your-api-url-goes-here'
const apiKey = 'your-public-api-key-goes-here'

fetch(`${apiURL}/translations`, {
        method: 'POST',
        headers: {
          'X-API-Key': apiKey,
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ 
            username: 'mega-mind', 
            translations: [] 
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
    "username": "mega-mind",
    "translations": []
}
```

### 🔒 Lost in Translation Users `PATCH /translations`
The `PATCH` method is used to update a single record

#### Sample Code
```javascript
const apiURL = 'your-api-url-goes-here'
const apiKey = 'your-public-api-key-goes-here'
const userId = 1 // Update user with id 1

fetch(`${apiURL}/translations/${userId}`, {
        method: 'PATCH', // NB: Set method to PATCH
        headers: {
            'X-API-Key': apiKey,
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            // Provide new translations to add to user with id 1
            translations: ['easy', 'i love javascript'] 
        })
    })
    .then(response => {
      if (!response.ok) {
        throw new Error('Could not update translations history')
      }
      return response.json()
    })
    .then(updatedUser => {
      // updatedUser is the user with the Patched data
    })
    .catch(error => {
    })
```