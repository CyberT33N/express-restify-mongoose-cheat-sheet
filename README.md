# express-restify-mongoose-cheat-sheet
express-restify-mongoose-cheat-sheet






<br><br>

# populate

<br><br>

## populate property in all documents
- 127.0.0.1:3050/v1/cs/Emails?populate=templateId

<br><br>

## Populate property in specific document
- 127.0.0.1:3050/v1/cs/Emails/60ec3b94dc86a75a5450e101?populate=templateId

<br><br>

## Use match after populate (https://mongoosejs.com/docs/populate.html#query-conditions)
- The match option doesn't filter out Story documents. If there are no documents that satisfy match, you'll get a Story document with an empty fans array.
- http://127.0.0.1:3000/v1/ms/Datasources?populate={"path":"tags","match":{"name":"sample"}}
- http://127.0.0.1:3050/v1/ms/Datasources?populate={"path":"tags","match":{"name":{"$eq":"sample"}}}

<br><br>
<br><br>
## select after populate
- 127.0.0.1:3050/v1/ms/Datasources?populate=tags&select=tags.name







<br><br>
<br><br>
____________________________________________________
____________________________________________________
<br><br>
<br><br>

# query

## Search value inside of array with object
- http://127.0.0.1:3050/v1/ms/Datasources?query={"tags":{"$elemMatch":{"key":"tag2"}}}
- http://127.0.0.1:3000/v1/ms/Datasources?query={"tags.key":"tag2"}
```
{
    "_id": ObjectId("60ec3b94dc86a75a5450c2d2"),
    "__v": 0,
    "tags": [{
        "key": "tag1",
        "value": "value1"
    }, {
        "key": "tag2",
        "value": "value2"
     }],
    "_createdAt": ISODate("2021-07-12T12:54:44.374Z"),
    "_createdBy": {
        "username": "system",
        "userid": "system"
    },
    "_updatedAt": ISODate("2021-07-12T12:54:44.374Z"),
    "_updatedBy": {
        "username": "system",
        "userid": "system"
    },
    "_deletedAt": null,
    "_deletedBy": null
}
```

<br><br>
<br><br>

## Check if field contains any specific element of array
```javascript
// method #1 - Search 1 specific element
it('should get all settings that have specific tag', async () => {
    const tags = ["apple"]
    const query = { tags: {$in: tags} }

    const uri =`${url}?query=${JSON.stringify(query)}`
    const res = await axiosP1.get(uri)
})

// method #2 - Search any element of array
it('should get all settings that have specific tag', async () => {
    const tags = ["apple", "social"]
    const query = { tags: {$in: tags} }

    const uri =`${url}?query=${JSON.stringify(query)}`
    const res = await axiosP1.get(uri)
})

// method #3 - Search all elements of array
it.only('should get all settings that contains all tags', async () => {
    const tags = [apple", "social"]
    const query = { tags: {$all: tags} }

    const uri =`${url}?query=${JSON.stringify(query)}`
    const res = await axiosP1.get(uri)
})
```

<br><br>
<br><br>

## Only reply with documents between dates
```javascript
api/test/modelName?query={"$and" : [{"_createdAt": {"$gt" : "2022-11-02T08:35:27.000Z"}},{"_createdAt": {"$lt" : "2022-11-08T08:35:27.000Z"}}]}
```
