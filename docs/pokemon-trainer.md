# Pokémon Trainer API

## Open Endpoints
Open endpoints do not require authentication.

### Pokémon Trainer Users `GET /trainers`
#### Sample Response
```json
[
  {
    "id": 1,
    "username": "dewaldels",
    "pokemon": []
  }
]
```

### Pokémon Users `GET /trainers?username=<query>`
You can filter results to get a specific user from the API. It uses the standard URL Query String syntax.

> **e.g.** Search for a user with username `mega-mind` you can make a `GET` request to `apiUrl/trivia?username=ash`.
>
> This will return an array of **all users** that match the username of ash.

#### Sample Code
```javascript
const apiURL = 'your-api-url-goes-here'
const username = 'ash'

fetch(`${apiURL}/trainers?username=${username}`)
    .then(response => response.json())
    .then(results => {
        // results will be an array of users that match the username of ash.
    })
    .catch(error => {
    })
```

## Protected Endpoints

Protected endpoints require the X-API-Key header with the API key as value.

### 🔒 Pokémon Trainer Users `POST /trainers`

Use the `POST` method to create a new Pokémon trainer in the API database.

#### Sample Code
```javascript
const apiURL = 'your-api-url-goes-here'
const apiKey = 'your-public-api-key-goes-here'

fetch(`${apiURL}/trainers`, {
        method: 'POST',
        headers: {
            'X-API-Key': apiKey,
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ 
            username: 'victor',
            pokemon: [] 
        })
    })
    .then(response => {
      if (!response.ok) {
        throw new Error('Could not create new Trainer')
      }
      return response.json()
    })
    .then(newUser => {
      // newUser is the new trainer user with an id
    })
    .catch(error => {
    })
```

#### Sample response
```json
{
    "id": 2,
    "username": "victor",
    "pokemon": []
}
```

### 🔒 Pokémon Trainer Users `PATCH /trainers`
The `PATCH` method is used to update a single record

#### Sample Code
```javascript
const apiURL = 'your-api-url-goes-here'
const apiKey = 'your-public-api-key-goes-here'
const userId = 1 // Update user with id 1

fetch(`${apiURL}/trainers/${userId}`, {
        method: 'PATCH', // NB: Set method to PATCH
        headers: {
            'X-API-Key': apiKey,
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            // Provide new Pokémon to add trainer with id 1
            pokemon: ['charizard', 'squirtle'] 
        })
    })
    .then(response => {
      if (!response.ok) {
        throw new Error('Could not update trainer')
      }
      return response.json()
    })
    .then(updatedTrainer => {
      // updatedTrainer is the trainer user the Patched data
    })
    .catch(error => {
    })
```