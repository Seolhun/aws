## API Gateway Model
```json
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "Company",
    "type": "object",
    "properties": {
        "id": { "type": "string" },
        "type": { "type": "string" },
        "name": { "type": "string" },
        "tags": {
            "type": "array",
            "items": { "type": "string" }
        },
        "descriptions": { "type": "string" },
        "content_counts": { "type": "integer" },
        "followers": { "type": "integer" },
        "timestamp": { "type": "integer" },
        "created_by": { "type": "string" },
        "created_date": { "type": "string" },
        "lastes_modified_date": { "type": "string" }
    },
    "required": ["id", "type", "name", "description", "timestamp", "created_by", "created_date"]
}
```


## API Gateway 통합요청 - Body Mapping
```aws
#set($inputRoot = $input.path('$'))
{
  "id" : "$inputRoot.id",
  "index" : "$inputRoot.index",
  "type" : "$inputRoot.type",
  "name" : "$inputRoot.name",
  "tags" : [
#foreach($elem in "$inputRoot.tags")
 $elem
#if($foreach.hasNext),#end
#end
],
  "descriptions" : "$inputRoot.descriptions",
  "content_counts" : "$inputRoot.content_counts",
  "followers" : "$inputRoot.followers",
  "created_by" : "$inputRoot.created_by",
  "created_date" : "$inputRoot.created_date",
  "lastes_modified_date" : "$inputRoot.lastes_modified_date"
}
```

## Lambda Code 
```nodjes
const AWS = require("aws-sdk");
const uuid = require('uuid');
const dynamodb = new AWS.DynamoDB({region: "ap-northeast-2", apiVersion: "2012-08-10"})

exports.handler = (event, context, callback) => {
    const params = {
        TableName: 'cb-company',
        Item: {
            "id": {
                S: uuid.v1()
            },
            "index" : {
                N : "" + new Date().getTime()
            },
            "type" : {
                S : event.type
            },
            "name" : {
                S : event.name
            },
            "descriptions" : {
                S : event.descriptions
            },
            "created_by" : {
                S : event.created_by
            },
            "created_date" : {
                S : event.created_date
            },
        }
    }
    dynamodb.putItem(params, function(err, data) {
        if (err) {
            console.log(err);
            callback(err)
        } else {
            console.log(data);
            callback(null, data)
        }
    });
};

```

## API Gateway Test
```json
{
    "type": "ZIGZAG",
    "name": "ZIGZAG",
    "descriptions": "ZIGZAG",
    "created_by": "ZIGZAG",
    "created_date": "ZIGZAG"
}
```