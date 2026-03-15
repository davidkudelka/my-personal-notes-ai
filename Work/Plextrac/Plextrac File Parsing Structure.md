  * Main
  * ```javascript
[
  {
    "id": "b21040bf-cc46-4ea8-9e5c-064eeecf88e3",
    "reportMe": {
      "description": "Mitre framework",
      "name": "Mitre",
      "source": {
        "id": "methodologyId",
        "key": "methodologyKey",
        "type": "Mitre"
      },
      "type": "rb-cat"
    }
  }
]  ```
  * 2020-08-04T07:10:24.505Z
  * Europe/Prague
  * curl localhost:4350/graphql \
  -F operations='{ "query": "mutation fileUpload($file: Upload!) { runbookEngagementActivityAttachmentUpload(file: $file) { key } }", "variables": { "file": null } }' \
  -F map='{ "0": ["variables.file"] }' \
  -F 0=@test.jpg

  * { "query":"mutation ($file: Upload){ runbookEngagementActivityAttachmentUpload(file: $file) {key} }","variables": { "file": null} }