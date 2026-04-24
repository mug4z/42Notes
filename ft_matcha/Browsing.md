Check the twitter recommendation algorithm [Github](https://github.com/twitter/the-algorithm) and [Blog](https://blog.x.com/engineering/en_us/topics/open-source/2023/twitter-recommendation-algorithm)
[k-nearest neighbors](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm)
[Gale-Shapley algorithm](https://en.wikipedia.org/wiki/Gale%E2%80%93Shapley_algorithm)

All the the above links can  help me to do the browsing system.
# Fame rating
>[!warning] Probably with it's own service ?

Check the [Elo system](https://en.wikipedia.org/wiki/Elo_rating_system#Theory).
A score that evaluate the fame of a person.
## How to base the score

# Operation
## Input

- User location
- Tags
- fame rating
- Age
- gender
- Sexuality (undefined => bisexual)
- Already matched ?
Example of input json
```json
{
  "userId": 12,
  "userLocation":{
    "Longitude": 1234,
    "Latitude": 1234
  },

  "tags":{
    "categories": ["actual_category_tag"],
    "sport": ["#Rugby","#Swim","#Badminton"],
    "videoGames": ["#ClairObscure","#BorderLands2","#TeamFortress2"]
  },
  
  "fameRating": 1234,
  "age":29,
  "gender":"male",
  "sexuality":"Bisexual",
  "UserIdMatched":[1233,21312]
}
```

## Transformation
- filter out based on the location.
- Filter the first dataset based on the gender, sexuality and useridmatched. Filter out the one that are incompatible.
- Filter out the one that are already matched with the current user.
- Now the dataset contain people that should match or not.
- Output the json.

## Output

```json
{
  "browsResult":{
    "people":{
      "user-id0":1234,
      "user-id1":2134
    }
  }
}
```


# Events
## Inbound
Exemple: User data change
If fame rating, tags, age, gender, sexuality the score would change.
## Outbound

# Resources
[indtroducing- JSON](https://www.json.org/json-en.html)
[Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API)
