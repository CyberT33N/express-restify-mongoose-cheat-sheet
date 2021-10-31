# express-restify-mongoose-cheat-sheet
express-restify-mongoose-cheat-sheet




<br><br>

# query


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
