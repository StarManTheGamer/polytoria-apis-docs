# Polytoria New Website APIs

‼ Polytoria Offical API Documentation is out now https://api.polytoria.com/docs

something undocumented, so it's time to dig down. <img src="https://cdn3.emoji.gg/emojis/3244-trollface.png" height="30">

Notes
- Parameters is formatting like the following: `parameter_name` `datatype`
- URL Parameters is something like `someurl/parameter_value`
- Query Parameters is something like `?parameter_name=parameter_value`
- If Headers Payload is marked with `JSON`, It means that you'll have to send the data as stringified JSON Object
- Anything marked with requires authentication

Found some mistakes? Have new APIs endpoint? Issue and Pull request are welcome! <img src="https://cdn3.emoji.gg/emojis/7278-hutaopray.png" height="35">

By DevPixels(also known as [Hu Tao](https://polytoria.com/users/16342) <img src="https://cdn3.emoji.gg/emojis/1434-hutaomonkas.png" height="30">)

### Contents
Click the title to jump into!
|Title|Base URL|
|--|--|
|[Store APIs](#store-apis)|https://polytoria.com/api/store|
|[Feed APIs](#feed-apis)|https://polytoria.com/api/feed|
|[Games APIs](#games-apis)|https://polytoria.com/api/places|
|[Guilds APIs](#guilds-apis)|https://polytoria.com/api/guilds|
|[Avatar APIs](#avatar-apis)|https://polytoria.com/api/avatar|
|[Creations APIs](#creations-apis)|https://polytoria.com/api/library|
|[Friends APIs](#friends-apis)|https://polytoria.com/api/friends|
|[Inbox APIs](#inbox-apis)|https://polytoria.com/api/inbox|
|[Profile APIs](#profile-apis)|Unavailable|
|[Search APIs](#search-apis)|https://polytoria.com/api/search|


## Store APIs

### Fetch catalog
`GET` https://polytoria.com/api/store/items

**Example Response**
```json
{
  "meta": {
    "total": 192,
    "perPage": 15,
    "currentPage": 1,
    "lastPage": 13,
    "firstPage": 1,
    "firstPageURL": "/api/store/items?...",
    "lastPageURL": "/api/store/items?...",
    "nextPageURL": "/api/store/items?...",
    "previousPageURL": "/api/store/items?..."
  },
  "data": [
    {
      "id": 24414,
      "type": "shirt",
      "name": "[Hope] Polytoria Hat Shirt",
      "description": "Matching Shirt for the hat!",
      "price": 3,
      "isLimited": false,
      "creatorName": "hopefullness",
      "recentlyUploaded": true,
      "thumbnailUrl": "https://c0.ptacdn.com/thumbnails/assets/[...].png",
      "creatorUrl": "/users/..."
    }
  ]
}
```

**Query Parameters**

`types` `string` - Types of the catalog item.
Can have multiple parameter at once, example: `?types[]=hat&types[]=tool&types[]=face`

Types: 
- hat
- tool
- face
- shirt
- pants
---
`page` `int` - Page of the catalog

`search` `string` - Search query

---
`sort` `string` - Sorting type
Types: 
- `createdDesc` Newest
- `createdAsc` Oldest
- `updatedDesc` Updated (Newest)
- `updatedAsc` Updated (Oldest)
- `priceDesc` Price (Highest)
- `priceAsc` Price (Lowest)

---
`order` `string` - Ordering, seems like it's sort parameter dependent
`desc` is descending
`asc` is ascending

- `createdDesc` Newest = `desc`
- `createdAsc` Oldest = `asc`
- `updatedDesc` Updated (Newest) = `desc`
- `updatedAsc` Updated (Oldest) = `asc`
- `priceDesc` Price (Highest) = `desc`
- `priceAsc` Price (Lowest) = `asc`

notice: also look at the sort's ending, it always end with neither `Desc` or `Asc` so maybe you could use that too.

---
`showOffsale` `boolean` - self explanatory 

`collectiblesOnly` `boolean` - self explanatory 

`minPrice` `int` - self explanatory

`maxPrice` `int` - self explanatory

`creatorName` `string` - self explanatory

---

### Fetch item comments

`GET` https://polytoria.com/api/comments/asset/[ID]?page=1

**Example Response**
```json
{
  "meta": {
    "total": 12,
    "perPage": 5,
    "currentPage": 1,
    "lastPage": 3,
    "firstPage": 1,
    "firstPageURL": "/api/comments/asset/...?page=...",
    "lastPageURL": "/api/comments/asset/...?page=...",
    "nextPageURL": "/api/comments/asset/...?page=...",
    "previousPageURL": "/api/comments/asset/...?page=...",
  },
  "data": [
    {
      "id": 237,
      "content": "going limited",
      "postedAt": "2023-04-14T21:31:19.565+00:00",
      "author": {
        "id": 3,
        "username": "Bandito Burrito",
        "avatarID": "...",
        "isOnline": false,
        "avatarIconUrl": "https://c0.ptacdn.com/thumbnails/avatars/[...]-icon.png"
      }
    }
  ]
}
```

**URL Parameters**
`[ID]` `int` The catalog item ID

**Query Parameters**
`page` `int` Page of the comment, self explanatory


## Feed APIs

### Fetch user feed

`GET` https://polytoria.com/api/feed
**!! Requires user authentication**

**Example Response**
```json
{
  "meta": {
    "total": 7272,
    "perPage": 10,
    "currentPage": 1,
    "lastPage": 728,
    "firstPage": 1,
    "firstPageURL": "/api/feed?page=...",
    "lastPageURL": "/api/feed?page=...",
    "nextPageURL": "/api/feed?page=...",
    "previousPageURL": "/api/feed?page=...",
  },
  "data": [
    {
      "id": 45233,
      "content": "Follow @PolytoriaNews on Twitter!",
      "postedAt": "2023-04-15T00:00:17.282+00:00",
      "author": {
        "id": 2021,
        "username": "Jaye",
        "avatarID": "...",
        "isOnline": false,
        "avatarIconUrl": "https://c0.ptacdn.com/thumbnails/avatars/[...]-icon.png"
      },
      "likeCount": "1",
      "replyCount": "0",
      "isLiked": false,
      "mediaUrl": null
    }
  ]
}
```

**Query Parameters**
`page` `int` Page of the feed, self explanatory

---

### Create Feed
`POST` https://polytoria.com/api/feed/create
**!! Requires user authentication**

**Example Response**
```json
{"success":true}
```

**Headers Payload `JSON`**
`content` `string` - The feed's content


## Games APIs

### Fetch games

`GET` https://polytoria.com/api/places

**Example Response**
```json
{
  "meta": {
    "total": 2011,
    "perPage": 27,
    "currentPage": 1,
    "lastPage": 75,
    "firstPage": 1,
    "firstPageURL": "/?page=...",
    "lastPageURL": "/?page=...",
    "nextPageURL": "/?page=...",
    "previousPageURL": "/?page=...",
  },
  "data": [
    {
      "id": 1,
      "creatorType": "user",
      "creatorID": 2,
      "name": "Polytoria City",
      "description": "The city where everything happens!",
      "genre": "other",
      "genreIcon": "planet-ringed",
      "creatorName": "willemsteller",
      "creatorThumbnail": "https://c0.ptacdn.com/thumbnails/avatars/[...]-icon.png",
      "visits": "89",
      "playing": "1",
      "rating": 1,
      "iconUrl": "https://c0.ptacdn.com/places/icons/[...].png"
    }
  ]
}
```

**Query Parameters**
`page` `int` Page of the games, self explanatory

`search` `string` Search query

---

`genre` `string` Game genre

Types:
- `all` All Genres
- `adventure` Adventure
- `building` Building
- `competitive` Competitive
- `creative` Creative
- `fighting` Fighting
- `puzzle` Puzzle
- `strategy` Strategy
- `racing` Racing
- `sandbox` Sandbox
- `survival` Survival
- `showcase` Showcase
- `techdemo` TechDemo
- `simulator` Simulator
- `trading` Trading
- `hangout` Hangout
- `western` Western
- `sports` Sports
- `medieval` Medieval
- `tycoon` Tycoon
- `parkour` Parkour
- `roleplay` Roleplay
- `funny` Funny
- `other` Other

---

`sort` `string` Sorting type

Types:
- `visits` Most Visits
- `rating` Top Rated
- `newest` Newest
- `updated` Updated

---

### Fetch game comments

`GET` https://polytoria.com/api/comments/place/[ID]

**Example Response**
```json
{
  "meta": {
    "total": 133,
    "perPage": 5,
    "currentPage": 1,
    "lastPage": 27,
    "firstPage": 1,
    "firstPageURL": "/api/comments/place/...?page=...",
    "lastPageURL": "/api/comments/place/...?page=...",
    "nextPageURL": "/api/comments/place/...?page=...",
    "previousPageURL": "/api/comments/place/...?page=...",
  },
  "data": [
    {
      "id": 41,
      "content": "For anyone lookin' to download the client, click here:\ncdn.polytoria.com/releases/installer/windows/Polytoria.exe",
      "postedAt": "2023-04-15T00:51:26.322+00:00",
      "author": {
        "id": 32619,
        "username": "glutealCheeze",
        "avatarID": "...",
        "isOnline": true,
        "avatarIconUrl": "https://c0.ptacdn.com/thumbnails/avatars/[...]-icon.png"
      }
    }
  ]
}
```

**URL Parameters**
`[ID]` `int` The game's ID

**Query Parameters**
`page` `int` Page of the comment, self explanatory

---

### Toggle rating

`POST` https://polytoria.com/api/places/toggle-like
**!! Requires user authentication**

**Example Response**
```json
{"success":false,"message":"Please visit this place before rating it."}
```

**Headers Payload `JSON`**
`placeID` `int` - Game's ID
`value` `string` - Like or dislike?

Types:
- like
- dislike

---
### Join Game

`POST` https://polytoria.com/api/places/join

**Example Response**
```json
{"success":true,"token":"..."}
```

**Headers Payload `JSON`**
`placeID` `int` - Game's ID


## Guilds APIs

### Fetch guild members

`GET` https://polytoria.com/api/guilds/[ID]/members/[RANK_ID]

**Example Response**
```json
{
  "meta": {
    "total": 13,
    "perPage": 12,
    "currentPage": 1,
    "lastPage": 2,
    "firstPage": 1,
    "firstPageURL": "/?page=...",
    "lastPageURL": "/?page=...",
    "nextPageURL": "/?page=...",
    "previousPageURL": "/?page=...",
  },
  "data": [
    {
      "rankID": 1815,
      "userID": 4764,
      "user": {
        "id": 4764,
        "username": "Kengie",
        "avatarID": "...",
        "isOnline": false,
        "avatarUrl": "https://c0.ptacdn.com/thumbnails/avatars/[...].png",
        "avatarIconUrl": "https://c0.ptacdn.com/thumbnails/avatars/[...]-icon.png",
        "userLinkClass": "userlink-default"
      }
    }
  ]
}
```

**URL Parameters**
`[ID]` `int` The guild's ID
`[RANK_ID]` `int` The guild rank's ID

**Query Parameters**
`page` `int` Page of the members, self explanatory

---

### Fetch guild wall

`GET` https://polytoria.com/api/guilds/[ID]/wall

**Example Response**
```json
{
  "meta": {
    "total": 12,
    "perPage": 10,
    "currentPage": 1,
    "lastPage": 2,
    "firstPage": 1,
    "firstPageURL": "/?page=...",
    "lastPageURL": "/?page=...",
    "nextPageURL": "/?page=...",
    "previousPageURL": "/?page=...",
  },
  "data": [
    {
      "id": 8227,
      "content": "Epic 😎",
      "postedAt": "2022-06-03T13:32:41.000+00:00",
      "author": {
        "id": 4764,
        "username": "Kengie",
        "avatarID": "...",
        "isOnline": false,
        "avatarUrl": "https://c0.ptacdn.com/thumbnails/avatars/[...].png",
        "avatarIconUrl": "https://c0.ptacdn.com/thumbnails/avatars/[...]-icon.png",
        "userLinkClass": "userlink-default"
      }
    }
  ]
}
```

**URL Parameters**
`[ID]` `int` The guild's ID

**Query Parameters**
`page` `int` Page of the wall, self explanatory

---

### Fetch guild assets

`GET` https://polytoria.com/api/guilds/[ID]/assets

**Example Response**
```json
{
  "meta": {
    "total": 0,
    "perPage": 16,
    "currentPage": 1,
    "lastPage": 1,
    "firstPage": 1,
    "firstPageURL": "/?page=...",
    "lastPageURL": "/?page=...",
    "nextPageURL": "/?page=...",
    "previousPageURL": "/?page=..."
  },
  "data": []
}
```
*at the time I'm writing this, there aren't any catalog items uploaded into the guild right now, it's prob the same as the one in the store api*

**URL Parameters**
`[ID]` `int` The guild's ID

**Query Parameters**
`page` `int` Page of the assets, self explanatory

---

### Fetch guild shouts

`GET` https://polytoria.com/api/guilds/[ID]/shouts

**URL Parameters**
`[ID]` `int` The guild's ID

**Query Parameters**
`page` `int` Page of the shouts, self explanatory

---

## Avatar APIs

### Fetch currently wearing

`GET` https://polytoria.com/api/avatar/wearing
**!! Requires user authentication**

**Example Response**
```json
{
  "meta": {
    "total": 3,
    "perPage": 12,
    "currentPage": 1,
    "lastPage": 1,
    "firstPage": 1,
    "firstPageURL": "/?page=...",
    "lastPageURL": "/?page=...",
    "nextPageURL": "/?page=...",
    "previousPageURL": "/?page=..."
  },
  "data": [
    {
      "id": 24122,
      "type": "hat",
      "name": "Polytoria Cap",
      "description": "Show your support for Polytoria with this slick brown cap!",
      "accessoryType": "hat",
      "creatorName": "Polytoria",
      "thumbnailUrl": "https://c0.ptacdn.com/thumbnails/assets/[...].png",
      "creatorUrl": "/users/1"
    }
  ]
}
```

---

### Fetch body colors preset

`GET` https://polytoria.com/api/avatar/colors

**Example Response**
```json
[
  "#f2f3f3",
  "#d7c59a",
  "#e8bac8",
  "#80bbdb",
  ...
]
```

Note: This API does not fetch your current body colors, It fetch body color preset appears in the body color selection menu.

---

### Fetch user's wardrobe

`GET` https://polytoria.com/api/avatar/wardrobe
**!! Requires user authentication**

**Example Response**
```json
{
  "meta": {
    "total": 1,
    "perPage": 12,
    "currentPage": 1,
    "lastPage": 1,
    "firstPage": 1,
    "firstPageURL": "/?page=...",
    "lastPageURL": "/?page=...",
    "nextPageURL": "/?page=...",
    "previousPageURL": "/?page=...",
  },
  "data": [
    {
      "id": 24122,
      "type": "hat",
      "name": "Polytoria Cap",
      "description": "Show your support for Polytoria with this slick brown cap!",
      "accessoryType": "hat",
      "creatorName": "Polytoria",
      "thumbnailUrl": "https://c0.ptacdn.com/thumbnails/assets/[...].png",
      "creatorUrl": "/users/1"
    }
  ]
}
```

**Query Parameters**

`type` `string` - Type of the catalog item.

Types: 
- hat
- tool
- face
- shirt
- pants
---
`page` `int` - Page of the catalog

`search` `string` - Search query

---

### Fetch user's outfits

`GET` https://polytoria.com/api/avatar/outfits
**!! Requires user authentication**

**Example Response**
```json
{
  "meta": {
    "total": 1,
    "perPage": 12,
    "currentPage": 1,
    "lastPage": 1,
    "firstPage": 1,
    "firstPageURL": "/?page=...",
    "lastPageURL": "/?page=...",
    "nextPageURL": "/?page=...",
    "previousPageURL": "/?page=..."
  },
  "data": [
    {
      "id": 94,
      "name": "first",
      "avatar": {
        "thumbnail": "https://c0.ptacdn.com/thumbnails/avatars/[...].png"
      }
    }
  ]
}
```

---

### Create user outfit

`POST` https://polytoria.com/api/avatar/outfits/create
**!! Requires user authentication**

**Example Response**
```json
{"success":true}
```

---

### Wear user outfit

`POST`  https://polytoria.com/api/avatar/outfits/wear
**!! Requires user authentication**

**Example Response**
```json
{"success":true,"avatar":"..."}
```

**Headers Payload `JSON`**
`id` `int` - ID of the outfit

---

### Delete user outfit

`POST`  https://polytoria.com/api/avatar/outfits/delete
**!! Requires user authentication**

**Example Response**
```json
{"success":true}
```

**Headers Payload `JSON`**
`id` `int` - ID of the outfit

---

### Redraw user avatar

`POST`  https://polytoria.com/api/avatar/redraw
**!! Requires user authentication**

**Example Response**
```json
{"avatar":"..."}
```

---

### Set body color

`POST` https://polytoria.com/api/avatar/paint
**!! Requires user authentication**

**Example Response**
```json
{"avatar":"..."}
```

**Headers Payload `JSON`**
`bodyPart` `string` - Body part type

Types:
- head
- torso
- rightArm
- leftArm
- rightLeg
- leftLeg
---

---

### Wear item

`POST` https://polytoria.com/api/avatar/wear
**!! Requires user authentication**

**Example Response**
```json
{"avatar":"..."}
```

**Headers Payload `JSON`**
`assetID` `int` - The item's ID

---

### Unwear item

`POST` https://polytoria.com/api/avatar/unwear
**!! Requires user authentication**

**Example Response**
```json
{"avatar":"..."}
```

**Headers Payload `JSON`**
`assetID` `int` - The item's ID



## Creations APIs

### Fetch Community creations

`GET` https://polytoria.com/api/library

**Example Response**
```json
{
  "meta": {
    "total": 655,
    "perPage": 15,
    "currentPage": 1,
    "lastPage": 44,
    "firstPage": 1,
    "firstPageURL": "/?page=...",
    "lastPageURL": "/?page=...",
    "nextPageURL": "/?page=...",
    "previousPageURL": "/?page=...",
  },
  "data": [
    {
      "id": 24114,
      "creatorID": 17064,
      "name": "Ambience Wind.mp3",
      "creatorName": "Emir",
      "thumbnailUrl": "https://c0.ptacdn.com/thumbnails/assets/[...].png",
      "creatorUrl": "/users/17064"
    }
  ]
}
```

**Query Parameters**

`types` `string` - Types of the library item.

Types: 
- model
- audio
- decal
- mesh
---
`page` `int` - Page of the library

`search` `string` - Search query


## Friends APIs

### Request Friend/Accept Friend request
`POST` https://polytoria.com/api/friends/send
**!! Requires user authentication**

**Headers Payload `JSON`**
`userID` `int` - The friend's user ID

---

### Unfriend/Decline Friend request
`POST`  https://polytoria.com/api/friends/remove
**!! Requires user authentication**

**Headers Payload `JSON`**
`userID` `int` - The friend's user ID

## Inbox APIs

### Toggle bookmark message

`POST` https://polytoria.com/inbox/messages/[ID]/bookmark

**Example Response**
```json
{"bookmarked":true}
```

**URL Parameters**
`[ID]` `int` The message ID

---


### Put message to the trash

`POST` https://polytoria.com/inbox/messages/[ID]/delete

**Example Response**
```json
{"deleted":true}
```

**URL Parameters**
`[ID]` `int` The message ID

## Profile APIs

### Fetch User's wall

`GET` https://polytoria.com/api/wall/[ID]?page=1
**Example Response**
```json
{
  "meta": {
    "total": 120,
    "perPage": 5,
    "currentPage": 1,
    "lastPage": 24,
    "firstPage": 1,
    "firstPageURL": "/?page=...",
    "lastPageURL": "/?page=...",
    "nextPageURL": "/?page=...",
    "previousPageURL": "/?page=...",
  },
  "data": [
    {
      "id": 1947,
      "content": "Hey! Feel free to leave a post on my Wall. I often read my wall and I might reply! :-)",
      "isPinned": true,
      "postedAt": "2021-03-28T22:50:18.000+00:00",
      "author": {
        "id": 7348,
        "username": "baggy",
        "avatarIconUrl": "https://c0.ptacdn.com/thumbnails/avatars/[...]-icon.png",
        "userLinkClass": "userlink-admin"
      }
  ]
}
```

**URL Parameters**
`[ID]` `int` The user's ID

**Query Parameters**
`page` `int` - Page of the wall


## Search APIs

`GET` https://polytoria.com/api/search

**Example Response**
```json
[
  {
    "id": 7348,
    "name": "baggy",
    "image": "...",
    "searchtype": "user"
  }
]
```

**Query Parameters**
`q` `string` - Search query

---
and more to come™
hi qqq
