```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-jp039a@email.com",
    "username": "author-jp039a",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-jp039a@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1qcDAzOWEiLCJpYXQiOjE1NDA2NjU0NzYsImV4cCI6MTU0MDgzODI3Nn0.K8gHwdAYq8AwYrTqiGk3O82vaFZw21ZuvrDZdTwkfvg",
    "username": "author-jp039a",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-a6dx0x@email.com",
    "username": "authoress-a6dx0x",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-a6dx0x@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy1hNmR4MHgiLCJpYXQiOjE1NDA2NjU0NzYsImV4cCI6MTU0MDgzODI3Nn0.xFGNeC6GDAtybfdpfauz3f1OlgkO70eI0VHxMts_3Dw",
    "username": "authoress-a6dx0x",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-syv4ld@email.com",
    "username": "non-author-syv4ld",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-syv4ld@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3Itc3l2NGxkIiwiaWF0IjoxNTQwNjY1NDc3LCJleHAiOjE1NDA4MzgyNzd9.clbl2Da2cqNEa-sTSaRjC8JfwiewhAHydqH-PdYjEfI",
    "username": "non-author-syv4ld",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ll6mg3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665477090,
    "updatedAt": 1540665477090,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-c350sy",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665477154,
    "updatedAt": 1540665477154,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-ll6mg3
```
```
200 OK

{
  "article": {
    "createdAt": 1540665477090,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-ll6mg3",
    "updatedAt": 1540665477090,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-c350sy
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1540665477154,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-c350sy",
    "updatedAt": 1540665477154,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/ej1wdk
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [ej1wdk]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-c350sy

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1540665477154,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-c350sy",
    "updatedAt": 1540665477154,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-c350sy

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1540665477154,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-c350sy",
    "updatedAt": 1540665477154,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-c350sy

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1540665477154,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-c350sy",
    "updatedAt": 1540665477154,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-c350sy

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-c350sy

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-c350sy

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-c350sy

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-c350sy]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-c350sy

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-jp039a]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-ll6mg3/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1540665477090,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-ll6mg3",
    "updatedAt": 1540665477090,
    "favoritedBy": [
      "non-author-syv4ld"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-ll6mg3
```
```
200 OK

{
  "article": {
    "createdAt": 1540665477090,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-ll6mg3",
    "updatedAt": 1540665477090,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-ll6mg3/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-ll6mg3_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-ll6mg3_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-ll6mg3/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1540665477090,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-ll6mg3",
    "updatedAt": 1540665477090,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-ll6mg3
```
```
200 OK

{}
```
```
GET /articles/title-ll6mg3
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-ll6mg3]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-c350sy
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-jp039a]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "yfoeqe",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-kzja72",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478305,
    "updatedAt": 1540665478305,
    "author": {
      "username": "authoress-a6dx0x",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "yfoeqe",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "9r5bze",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-c4noqp",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478334,
    "updatedAt": 1540665478334,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "9r5bze",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7rtpz",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-aahgwr",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478368,
    "updatedAt": 1540665478368,
    "author": {
      "username": "authoress-a6dx0x",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7rtpz",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "n671kz",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ft1qyf",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478397,
    "updatedAt": 1540665478397,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "n671kz",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "31mhwh",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ril6ec",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478427,
    "updatedAt": 1540665478427,
    "author": {
      "username": "authoress-a6dx0x",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "31mhwh",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "x4hrsn",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-hh3j7x",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478467,
    "updatedAt": 1540665478467,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "x4hrsn",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "nd03k0",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-98s596",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478508,
    "updatedAt": 1540665478508,
    "author": {
      "username": "authoress-a6dx0x",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "nd03k0",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "nopq79",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-q4xaeu",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478547,
    "updatedAt": 1540665478547,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "nopq79",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "afc83p",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-95uatj",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478584,
    "updatedAt": 1540665478584,
    "author": {
      "username": "authoress-a6dx0x",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "afc83p",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "dvfvzx",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-2sowhn",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478624,
    "updatedAt": 1540665478624,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dvfvzx",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "p4dr34",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-uiyuma",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478663,
    "updatedAt": 1540665478663,
    "author": {
      "username": "authoress-a6dx0x",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "p4dr34",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "p6dspw",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3cj9zp",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478700,
    "updatedAt": 1540665478700,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "p6dspw",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "15etjf",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-eeiowm",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478737,
    "updatedAt": 1540665478737,
    "author": {
      "username": "authoress-a6dx0x",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "15etjf",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "oll4eq",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-uk2q5x",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478773,
    "updatedAt": 1540665478773,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "oll4eq",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "jonmts",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-pimz2a",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478810,
    "updatedAt": 1540665478810,
    "author": {
      "username": "authoress-a6dx0x",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "jonmts",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "374j9i",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-xuwjp2",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478848,
    "updatedAt": 1540665478848,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "374j9i",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "wnkv3u",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-fzss7b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478896,
    "updatedAt": 1540665478896,
    "author": {
      "username": "authoress-a6dx0x",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "wnkv3u",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "q7v75q",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-k41e00",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478949,
    "updatedAt": 1540665478949,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "q7v75q",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "httnk3",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-74yfl9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665478987,
    "updatedAt": 1540665478987,
    "author": {
      "username": "authoress-a6dx0x",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "httnk3",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "mylig",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-f1gj8c",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665479056,
    "updatedAt": 1540665479056,
    "author": {
      "username": "author-jp039a",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "mylig",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "mylig",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665479056,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f1gj8c",
      "updatedAt": 1540665479056,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "httnk3",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478987,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-74yfl9",
      "updatedAt": 1540665478987,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q7v75q",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478949,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-k41e00",
      "updatedAt": 1540665478949,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wnkv3u"
      ],
      "createdAt": 1540665478896,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fzss7b",
      "updatedAt": 1540665478896,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "374j9i",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478848,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xuwjp2",
      "updatedAt": 1540665478848,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jonmts",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478810,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pimz2a",
      "updatedAt": 1540665478810,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oll4eq",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478773,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uk2q5x",
      "updatedAt": 1540665478773,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "15etjf",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478737,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eeiowm",
      "updatedAt": 1540665478737,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p6dspw",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478700,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3cj9zp",
      "updatedAt": 1540665478700,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p4dr34",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478663,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uiyuma",
      "updatedAt": 1540665478663,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dvfvzx",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478624,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2sowhn",
      "updatedAt": 1540665478624,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "afc83p",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478584,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-95uatj",
      "updatedAt": 1540665478584,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nopq79",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478547,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q4xaeu",
      "updatedAt": 1540665478547,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nd03k0",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478508,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-98s596",
      "updatedAt": 1540665478508,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "x4hrsn"
      ],
      "createdAt": 1540665478467,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hh3j7x",
      "updatedAt": 1540665478467,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "31mhwh",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478427,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ril6ec",
      "updatedAt": 1540665478427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n671kz",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478397,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ft1qyf",
      "updatedAt": 1540665478397,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7rtpz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478368,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-aahgwr",
      "updatedAt": 1540665478368,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9r5bze",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478334,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c4noqp",
      "updatedAt": 1540665478334,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "yfoeqe"
      ],
      "createdAt": 1540665478305,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kzja72",
      "updatedAt": 1540665478305,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "nopq79",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478547,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q4xaeu",
      "updatedAt": 1540665478547,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "q7v75q",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478949,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-k41e00",
      "updatedAt": 1540665478949,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jonmts",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478810,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pimz2a",
      "updatedAt": 1540665478810,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p6dspw",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478700,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3cj9zp",
      "updatedAt": 1540665478700,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "afc83p",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478584,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-95uatj",
      "updatedAt": 1540665478584,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "x4hrsn"
      ],
      "createdAt": 1540665478467,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hh3j7x",
      "updatedAt": 1540665478467,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7rtpz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478368,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-aahgwr",
      "updatedAt": 1540665478368,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-a6dx0x
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "httnk3",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478987,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-74yfl9",
      "updatedAt": 1540665478987,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wnkv3u"
      ],
      "createdAt": 1540665478896,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fzss7b",
      "updatedAt": 1540665478896,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jonmts",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478810,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pimz2a",
      "updatedAt": 1540665478810,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "15etjf",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478737,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eeiowm",
      "updatedAt": 1540665478737,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p4dr34",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478663,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uiyuma",
      "updatedAt": 1540665478663,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "afc83p",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478584,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-95uatj",
      "updatedAt": 1540665478584,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nd03k0",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478508,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-98s596",
      "updatedAt": 1540665478508,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "31mhwh",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478427,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ril6ec",
      "updatedAt": 1540665478427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7rtpz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478368,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-aahgwr",
      "updatedAt": 1540665478368,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "yfoeqe"
      ],
      "createdAt": 1540665478305,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kzja72",
      "updatedAt": 1540665478305,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-syv4ld
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-jp039a&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "mylig",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665479056,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f1gj8c",
      "updatedAt": 1540665479056,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q7v75q",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478949,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-k41e00",
      "updatedAt": 1540665478949,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-jp039a&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "374j9i",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478848,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xuwjp2",
      "updatedAt": 1540665478848,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oll4eq",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478773,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uk2q5x",
      "updatedAt": 1540665478773,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "mylig",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665479056,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f1gj8c",
      "updatedAt": 1540665479056,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "httnk3",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478987,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-74yfl9",
      "updatedAt": 1540665478987,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q7v75q",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478949,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-k41e00",
      "updatedAt": 1540665478949,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wnkv3u"
      ],
      "createdAt": 1540665478896,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fzss7b",
      "updatedAt": 1540665478896,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "374j9i",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478848,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xuwjp2",
      "updatedAt": 1540665478848,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jonmts",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478810,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pimz2a",
      "updatedAt": 1540665478810,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oll4eq",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478773,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uk2q5x",
      "updatedAt": 1540665478773,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "15etjf",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478737,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eeiowm",
      "updatedAt": 1540665478737,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p6dspw",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478700,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3cj9zp",
      "updatedAt": 1540665478700,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p4dr34",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478663,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uiyuma",
      "updatedAt": 1540665478663,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dvfvzx",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478624,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2sowhn",
      "updatedAt": 1540665478624,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "afc83p",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478584,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-95uatj",
      "updatedAt": 1540665478584,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nopq79",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478547,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q4xaeu",
      "updatedAt": 1540665478547,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nd03k0",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478508,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-98s596",
      "updatedAt": 1540665478508,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "x4hrsn"
      ],
      "createdAt": 1540665478467,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hh3j7x",
      "updatedAt": 1540665478467,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "31mhwh",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478427,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ril6ec",
      "updatedAt": 1540665478427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n671kz",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478397,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ft1qyf",
      "updatedAt": 1540665478397,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7rtpz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478368,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-aahgwr",
      "updatedAt": 1540665478368,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9r5bze",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478334,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c4noqp",
      "updatedAt": 1540665478334,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "yfoeqe"
      ],
      "createdAt": 1540665478305,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kzja72",
      "updatedAt": 1540665478305,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-a6dx0x/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-a6dx0x",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "httnk3",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478987,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-74yfl9",
      "updatedAt": 1540665478987,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wnkv3u"
      ],
      "createdAt": 1540665478896,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fzss7b",
      "updatedAt": 1540665478896,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jonmts",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478810,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pimz2a",
      "updatedAt": 1540665478810,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "15etjf",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478737,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eeiowm",
      "updatedAt": 1540665478737,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p4dr34",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478663,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uiyuma",
      "updatedAt": 1540665478663,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "afc83p",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478584,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-95uatj",
      "updatedAt": 1540665478584,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nd03k0",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478508,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-98s596",
      "updatedAt": 1540665478508,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "31mhwh",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478427,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ril6ec",
      "updatedAt": 1540665478427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7rtpz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478368,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-aahgwr",
      "updatedAt": 1540665478368,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "yfoeqe"
      ],
      "createdAt": 1540665478305,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kzja72",
      "updatedAt": 1540665478305,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-jp039a/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-jp039a",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "mylig",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665479056,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f1gj8c",
      "updatedAt": 1540665479056,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "httnk3",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478987,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-74yfl9",
      "updatedAt": 1540665478987,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q7v75q",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478949,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-k41e00",
      "updatedAt": 1540665478949,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wnkv3u"
      ],
      "createdAt": 1540665478896,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fzss7b",
      "updatedAt": 1540665478896,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "374j9i",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478848,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xuwjp2",
      "updatedAt": 1540665478848,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jonmts",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478810,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pimz2a",
      "updatedAt": 1540665478810,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oll4eq",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478773,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uk2q5x",
      "updatedAt": 1540665478773,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "15etjf",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478737,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eeiowm",
      "updatedAt": 1540665478737,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p6dspw",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478700,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3cj9zp",
      "updatedAt": 1540665478700,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p4dr34",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478663,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uiyuma",
      "updatedAt": 1540665478663,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dvfvzx",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478624,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2sowhn",
      "updatedAt": 1540665478624,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "afc83p",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478584,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-95uatj",
      "updatedAt": 1540665478584,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nopq79",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478547,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q4xaeu",
      "updatedAt": 1540665478547,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nd03k0",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478508,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-98s596",
      "updatedAt": 1540665478508,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "x4hrsn"
      ],
      "createdAt": 1540665478467,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hh3j7x",
      "updatedAt": 1540665478467,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "31mhwh",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478427,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ril6ec",
      "updatedAt": 1540665478427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n671kz",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1540665478397,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ft1qyf",
      "updatedAt": 1540665478397,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7rtpz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1540665478368,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-aahgwr",
      "updatedAt": 1540665478368,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9r5bze",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1540665478334,
      "author": {
        "username": "author-jp039a",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c4noqp",
      "updatedAt": 1540665478334,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "yfoeqe"
      ],
      "createdAt": 1540665478305,
      "author": {
        "username": "authoress-a6dx0x",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kzja72",
      "updatedAt": 1540665478305,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "tag_16",
    "tag_mod_2_0",
    "tag_mod_3_1",
    "wnkv3u",
    "nopq79",
    "tag_7",
    "tag_mod_2_1",
    "afc83p",
    "tag_8",
    "tag_mod_3_2",
    "374j9i",
    "tag_15",
    "tag_mod_3_0",
    "q7v75q",
    "tag_17",
    "tag_5",
    "x4hrsn",
    "15etjf",
    "tag_12",
    "p4dr34",
    "tag_10",
    "9r5bze",
    "tag_1",
    "tag_a",
    "tag_b",
    "nd03k0",
    "tag_6",
    "oll4eq",
    "tag_13",
    "p6dspw",
    "tag_11",
    "dvfvzx",
    "tag_9",
    "httnk3",
    "tag_18",
    "mylig",
    "tag_19",
    "tag_0",
    "yfoeqe",
    "31mhwh",
    "tag_4",
    "n671kz",
    "tag_3",
    "jonmts",
    "tag_14",
    "7rtpz",
    "tag_2"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-h4gzi4@email.com",
    "username": "author-h4gzi4",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-h4gzi4@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1oNGd6aTQiLCJpYXQiOjE1NDA2NjU0ODAsImV4cCI6MTU0MDgzODI4MH0.SM27-3KbBZF8FeqavDlU3EIqutleTmHaktvDiKhh49E",
    "username": "author-h4gzi4",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-1ynl5k@email.com",
    "username": "commenter-1ynl5k",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-1ynl5k@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci0xeW5sNWsiLCJpYXQiOjE1NDA2NjU0ODAsImV4cCI6MTU0MDgzODI4MH0.hrFG0yvbRa6N6CC5rw0QwJVaxUonfiurSkx8M1y3pMw",
    "username": "commenter-1ynl5k",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-uvd2pn",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1540665480729,
    "updatedAt": 1540665480729,
    "author": {
      "username": "author-h4gzi4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-uvd2pn/comments

{
  "comment": {
    "body": "test comment mn4lie"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "bca01773-9b66-41d6-b8df-29ba8dfa5ca5",
    "slug": "title-uvd2pn",
    "body": "test comment mn4lie",
    "createdAt": 1540665480758,
    "updatedAt": 1540665480758,
    "author": {
      "username": "commenter-1ynl5k",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-uvd2pn/comments

{
  "comment": {
    "body": "test comment ohlyal"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f1e0500e-7ecd-4a16-89dd-4a9a585a27f0",
    "slug": "title-uvd2pn",
    "body": "test comment ohlyal",
    "createdAt": 1540665480794,
    "updatedAt": 1540665480794,
    "author": {
      "username": "commenter-1ynl5k",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-uvd2pn/comments

{
  "comment": {
    "body": "test comment g25xl8"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "0af19cf1-0de3-43b1-acf7-a535ce1a91a2",
    "slug": "title-uvd2pn",
    "body": "test comment g25xl8",
    "createdAt": 1540665480822,
    "updatedAt": 1540665480822,
    "author": {
      "username": "commenter-1ynl5k",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-uvd2pn/comments

{
  "comment": {
    "body": "test comment dqn7gm"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "80583b37-7f9a-4f02-ad91-e32e4fb34ec1",
    "slug": "title-uvd2pn",
    "body": "test comment dqn7gm",
    "createdAt": 1540665480854,
    "updatedAt": 1540665480854,
    "author": {
      "username": "commenter-1ynl5k",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-uvd2pn/comments

{
  "comment": {
    "body": "test comment 9yz201"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "fa8d4149-aaaf-4554-b8ac-cf1a26f4b631",
    "slug": "title-uvd2pn",
    "body": "test comment 9yz201",
    "createdAt": 1540665480896,
    "updatedAt": 1540665480896,
    "author": {
      "username": "commenter-1ynl5k",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-uvd2pn/comments

{
  "comment": {
    "body": "test comment -z5k79h"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "49d43605-97f3-4c4f-8d12-97396fe7ff5d",
    "slug": "title-uvd2pn",
    "body": "test comment -z5k79h",
    "createdAt": 1540665480928,
    "updatedAt": 1540665480928,
    "author": {
      "username": "commenter-1ynl5k",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-uvd2pn/comments

{
  "comment": {
    "body": "test comment 5zm8vw"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e9659e65-a4e1-483f-b114-79b5a246908c",
    "slug": "title-uvd2pn",
    "body": "test comment 5zm8vw",
    "createdAt": 1540665480960,
    "updatedAt": 1540665480960,
    "author": {
      "username": "commenter-1ynl5k",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-uvd2pn/comments

{
  "comment": {
    "body": "test comment 6s76a5"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "ba40d3a6-3f9f-4034-a914-66fc544f04a0",
    "slug": "title-uvd2pn",
    "body": "test comment 6s76a5",
    "createdAt": 1540665481009,
    "updatedAt": 1540665481009,
    "author": {
      "username": "commenter-1ynl5k",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-uvd2pn/comments

{
  "comment": {
    "body": "test comment 51b06y"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "7056b3d2-a90e-4fbe-b692-0f37ad6bf881",
    "slug": "title-uvd2pn",
    "body": "test comment 51b06y",
    "createdAt": 1540665481049,
    "updatedAt": 1540665481049,
    "author": {
      "username": "commenter-1ynl5k",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-uvd2pn/comments

{
  "comment": {
    "body": "test comment 1cjku"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "32603d4e-3c5e-4939-9aa6-2a0867bf5d54",
    "slug": "title-uvd2pn",
    "body": "test comment 1cjku",
    "createdAt": 1540665481078,
    "updatedAt": 1540665481078,
    "author": {
      "username": "commenter-1ynl5k",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-uvd2pn/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-uvd2pn/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment 18tloe"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-uvd2pn/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1540665480854,
      "id": "80583b37-7f9a-4f02-ad91-e32e4fb34ec1",
      "body": "test comment dqn7gm",
      "slug": "title-uvd2pn",
      "author": {
        "username": "commenter-1ynl5k",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1540665480854
    },
    {
      "createdAt": 1540665480758,
      "id": "bca01773-9b66-41d6-b8df-29ba8dfa5ca5",
      "body": "test comment mn4lie",
      "slug": "title-uvd2pn",
      "author": {
        "username": "commenter-1ynl5k",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1540665480758
    },
    {
      "createdAt": 1540665481009,
      "id": "ba40d3a6-3f9f-4034-a914-66fc544f04a0",
      "body": "test comment 6s76a5",
      "slug": "title-uvd2pn",
      "author": {
        "username": "commenter-1ynl5k",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1540665481009
    },
    {
      "createdAt": 1540665480794,
      "id": "f1e0500e-7ecd-4a16-89dd-4a9a585a27f0",
      "body": "test comment ohlyal",
      "slug": "title-uvd2pn",
      "author": {
        "username": "commenter-1ynl5k",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1540665480794
    },
    {
      "createdAt": 1540665480928,
      "id": "49d43605-97f3-4c4f-8d12-97396fe7ff5d",
      "body": "test comment -z5k79h",
      "slug": "title-uvd2pn",
      "author": {
        "username": "commenter-1ynl5k",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1540665480928
    },
    {
      "createdAt": 1540665481049,
      "id": "7056b3d2-a90e-4fbe-b692-0f37ad6bf881",
      "body": "test comment 51b06y",
      "slug": "title-uvd2pn",
      "author": {
        "username": "commenter-1ynl5k",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1540665481049
    },
    {
      "createdAt": 1540665480896,
      "id": "fa8d4149-aaaf-4554-b8ac-cf1a26f4b631",
      "body": "test comment 9yz201",
      "slug": "title-uvd2pn",
      "author": {
        "username": "commenter-1ynl5k",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1540665480896
    },
    {
      "createdAt": 1540665481078,
      "id": "32603d4e-3c5e-4939-9aa6-2a0867bf5d54",
      "body": "test comment 1cjku",
      "slug": "title-uvd2pn",
      "author": {
        "username": "commenter-1ynl5k",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1540665481078
    },
    {
      "createdAt": 1540665480822,
      "id": "0af19cf1-0de3-43b1-acf7-a535ce1a91a2",
      "body": "test comment g25xl8",
      "slug": "title-uvd2pn",
      "author": {
        "username": "commenter-1ynl5k",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1540665480822
    },
    {
      "createdAt": 1540665480960,
      "id": "e9659e65-a4e1-483f-b114-79b5a246908c",
      "body": "test comment 5zm8vw",
      "slug": "title-uvd2pn",
      "author": {
        "username": "commenter-1ynl5k",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1540665480960
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-uvd2pn/comments/bca01773-9b66-41d6-b8df-29ba8dfa5ca5
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-uvd2pn/comments/f1e0500e-7ecd-4a16-89dd-4a9a585a27f0
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-1ynl5k]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-uvd2pn/comments/f1e0500e-7ecd-4a16-89dd-4a9a585a27f0
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-uvd2pn/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.1nyptph1vsk@email.com",
    "username": "user1-0.1nyptph1vsk",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.1nyptph1vsk@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuMW55cHRwaDF2c2siLCJpYXQiOjE1NDA2NjU0ODEsImV4cCI6MTU0MDgzODI4MX0.RzKe4tn4_fPctbo7vD-77seJhEYJ02ArjReaQVQqWuI",
    "username": "user1-0.1nyptph1vsk",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.1nyptph1vsk@email.com",
    "username": "user1-0.1nyptph1vsk",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.1nyptph1vsk]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.1nyptph1vsk@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.1nyptph1vsk@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.1nyptph1vsk@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.1nyptph1vsk@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuMW55cHRwaDF2c2siLCJpYXQiOjE1NDA2NjU0ODEsImV4cCI6MTU0MDgzODI4MX0.RzKe4tn4_fPctbo7vD-77seJhEYJ02ArjReaQVQqWuI",
    "username": "user1-0.1nyptph1vsk",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.sa9rvvfs4yg",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.sa9rvvfs4yg]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.1nyptph1vsk@email.com",
    "password": "0.l70kv2k0hjc"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.1nyptph1vsk@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuMW55cHRwaDF2c2siLCJpYXQiOjE1NDA2NjU0ODEsImV4cCI6MTU0MDgzODI4MX0.RzKe4tn4_fPctbo7vD-77seJhEYJ02ArjReaQVQqWuI",
    "username": "user1-0.1nyptph1vsk",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.1nyptph1vsk
```
```
200 OK

{
  "profile": {
    "username": "user1-0.1nyptph1vsk",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.2997pvh4wx
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.2997pvh4wx]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1NDA2NjU0ODEsImV4cCI6MTU0MDgzODI4MX0.IzQMjqY0j1IWVSXH9uWGTKOxwXbjciAsfcV3SsgpCD0",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.l4wsnc5bco",
    "email": "user2-0.l4wsnc5bco@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.l4wsnc5bco@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAubDR3c25jNWJjbyIsImlhdCI6MTU0MDY2NTQ4MSwiZXhwIjoxNTQwODM4MjgxfQ.xHUVf6XMho4oq8CDyQ1t_Vs97-C04cXcYxHH_6tzpwk",
    "username": "user2-0.l4wsnc5bco",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.1nyptph1vsk@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.1nyptph1vsk",
    "email": "updated-user1-0.1nyptph1vsk@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuMW55cHRwaDF2c2siLCJpYXQiOjE1NDA2NjU0ODEsImV4cCI6MTU0MDgzODI4MX0.RzKe4tn4_fPctbo7vD-77seJhEYJ02ArjReaQVQqWuI"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.1nyptph1vsk",
    "email": "updated-user1-0.1nyptph1vsk@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuMW55cHRwaDF2c2siLCJpYXQiOjE1NDA2NjU0ODEsImV4cCI6MTU0MDgzODI4MX0.RzKe4tn4_fPctbo7vD-77seJhEYJ02ArjReaQVQqWuI"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.1nyptph1vsk",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuMW55cHRwaDF2c2siLCJpYXQiOjE1NDA2NjU0ODEsImV4cCI6MTU0MDgzODI4MX0.RzKe4tn4_fPctbo7vD-77seJhEYJ02ArjReaQVQqWuI"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.1nyptph1vsk",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuMW55cHRwaDF2c2siLCJpYXQiOjE1NDA2NjU0ODEsImV4cCI6MTU0MDgzODI4MX0.RzKe4tn4_fPctbo7vD-77seJhEYJ02ArjReaQVQqWuI"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.blmcp90dj6h@email.com",
    "username": "user2-0.blmcp90dj6h",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.blmcp90dj6h@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuYmxtY3A5MGRqNmgiLCJpYXQiOjE1NDA2NjU0ODIsImV4cCI6MTU0MDgzODI4Mn0.qpYdaqvPOw1E35FLMoFM_Z1oHPxMQOj0-c9AjYDqxuQ",
    "username": "user2-0.blmcp90dj6h",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.blmcp90dj6h@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.blmcp90dj6h@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2018-10-27T18:38:02.216Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
