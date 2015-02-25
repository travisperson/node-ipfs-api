# IPFS API via NodeJS

The following is a simple documentation of the API command expoded in
the NodeJS module for IFPS. All callbacks respect nodes error style handling. The first argument is an error followed by the response.

## Level 1 Commands
Level 1 commands are simple commands

### Add
Add a file (where file is any data) to ipfs returning the hash and name. The name value will only be set if you are actually sending a file. A single or array of files can be used.

**Usage**
```javascript
ipfs.add(files, function(err, res) {
    if(err || !res) return console.error(err)
    
    res.forEach(function(file) {
        console.log(file.Hash)
        console.log(file.Name)
    })
})
```
`files` can be a mixed array of filenames or buffers of data. A single value is also acceptable.

Example
```
var files = ["../files/hello.txt", new Buffer("ipfs!")]
var files = "../files/hello.txt"
```

**Response**
```json
[{
    Hash: string,
    Name: string
}, ...]
```
*The name value will only be set for actual files*


### cat
Retreieve the contents of a single, or array of hashes

**Usage**
```javascript
ipfs.cat(hashs, function(err, res) {
    if(err || !res) return console.error(err)
    
    if(res.readable) {
        // Returned as a stream
        res.pipe(process.stdout)
    } else {
        // Returned as a string
        console.log(res)
    }
})
```

**Response**

The response is either a readable stream, or a string.

### ls
Get the node struchure of a hash, included in it is a hash and array to links.

**Usage**
```javascript
ipfs.ls(hashs, function(err, res) {
    if(err || !res) return console.error(err)
    
    res.Objects.forEach(function(node) {
        console.log(node.Hash)
        console.log("Links [%d]", node.Links.length)
        node.Links.forEach(function(link, i) {
            console.log("[%d]", i, link)
        })
    })
})
```

**Response**
```
{
    Objects: [
        { 
            Hash: string,
            Links: [{
                Name: string,
                Hash: string,
                Size: number
            }, ...]
        },
        ....
    ]
}
```

**version**

**commands**

## Level 2 Commands
Level 2 commands are simply named spaced wrapped commands

### Config

### Update

### Mount

### Diag

### Block

### Object

### Swarm

### Pin

### Gateway
