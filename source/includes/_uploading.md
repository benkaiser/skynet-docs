# Uploading to Skynet

## Uploading a File

```shell--curl
curl -X POST "https://siasky.net/skynet/skyfile" -F file=@image.jpg
```

```shell--cli
skynet upload "./image.jpg"
```

```javascript--browser
// TODO
```

```javascript--node
const skynet = require('@nebulous/skynet');

(async () => {
	const skylink = await skynet.UploadFile(
		"./image.jpg",
		skynet.DefaultUploadOptions
	);
	console.log(`Upload successful, skylink: ${skylink}`);
})();
```

```python
import siaskynet as skynet

skylink = skynet.upload_file("image.jpg")
print("Upload successful, skylink: " + skylink)
```

```go
package main

import (
	"fmt"
	skynet "github.com/NebulousLabs/go-skynet"
)

func main() {
	skylink, err := skynet.UploadFile("./image.jpg", skynet.DefaultUploadOptions)
	if err != nil {
		panic("Unable to upload: " + err.Error())
	}
	fmt.Printf("Upload successful, skylink: %v\n", skylink)
}
```

Uploading a file to Skynet can be done through a Skynet portal or your
local siad instance.

<aside class="notice">
If a file is uploaded through a portal, the portal owner is paying to host that file, and it will remain on the network for as long as that file contract is valid.
</aside>

### Settings

Field      | Description
---------- | -----------
`portal`   | The URL of the portal.
`filename` | Custom filename. This is the filename that will be returned when downloading the file in a browser.

### Response

```shell--curl
{
  "skylink": "CABAB_1Dt0FJsxqsu_J4TodNCbCGvtFf1Uys_3EgzOlTcg",
  "merkleroot": "QAf9Q7dBSbMarLvyeE6HTQmwhr7RX9VMrP9xIMzpU3I",
  "bitfield": 2048
}
```

```shell--cli
# TODO
```

```javascript--browser
// skylink = "CABAB_1Dt0FJsxqsu_J4TodNCbCGvtFf1Uys_3EgzOlTcg"
```

```javascript--node
// skylink = "CABAB_1Dt0FJsxqsu_J4TodNCbCGvtFf1Uys_3EgzOlTcg"
```

```python
# skylink = "CABAB_1Dt0FJsxqsu_J4TodNCbCGvtFf1Uys_3EgzOlTcg"
```

```go
// skylink = "CABAB_1Dt0FJsxqsu_J4TodNCbCGvtFf1Uys_3EgzOlTcg"
```

The response will contain some or all of these fields:

Field        | Description
------------ | -----------
`skylink`    | This is the skylink that can be used when downloading to retrieve the file that has been uploaded. It is a 46-character base64 encoded string that consists of the merkle root, offset, fetch size, and Skylink version which can be used to access the content.
`merkleroot` | This is the hash that is encoded into the skylink.
`bitfield`   | This is the bitfield that gets encoded into the skylink. The bitfield contains a version, an offset and a length in a heavily compressed and optimized format.

## Uploading a Directory

```shell--curl
curl "https://siasky.net/skynet/skyfile" -F files[]=@./images/image1.png -F files[]=@./images/image2.png
```

```shell--cli
skynet upload "source dir path"
```

```javascript--browser
// TODO
```

```javascript--node
const skynet = require('@nebulous/skynet');

(async () => {
	const url = await skynet.UploadDirectory(
		"./images",
		skynet.DefaultUploadOptions
	);
	console.log(`Upload successful, url: ${url}`);
})();
```

```python
import siaskynet as skynet

url = skynet.upload_directory("./images")
print("Upload successful, url: " + url)
```

```go
package main

import (
	"fmt"
	skynet "github.com/NebulousLabs/go-skynet"
)

func main() {
	url, err := skynet.UploadDirectory("./images", skynet.DefaultUploadOptions)
	if err != nil {
		panic("Unable to upload: " + err.Error())
	}
	fmt.Printf("Upload successful, url: %v\n", url)
}
```

It is possible to upload a directory as a single piece of content. Doing this
will allow you to address your content under one skylink, and access the files
by their path. This is especially useful for webapps.

Directory uploads work using multipart form upload.

### Settings

Field       | Description
----------- | -----------
`portal`    | The URL of the portal
`filename`  | Custom filename. This is the filename that will be returned when downloading the file in a browser

### Response

```shell--curl
{
  "skylink": "CABAB_1Dt0FJsxqsu_J4TodNCbCGvtFf1Uys_3EgzOlTcg",
  "merkleroot": "QAf9Q7dBSbMarLvyeE6HTQmwhr7RX9VMrP9xIMzpU3I",
  "bitfield": 2048
}
```

```shell--cli
# TODO
```

```javascript--browser
// url = sia://EAAV-eT8wBIF1EPgT6WQkWWsb3mYyEO1xz9iFueK5zCtqg
```

```javascript--node
// url = sia://EAAV-eT8wBIF1EPgT6WQkWWsb3mYyEO1xz9iFueK5zCtqg
```

```python
# url = sia://EAAV-eT8wBIF1EPgT6WQkWWsb3mYyEO1xz9iFueK5zCtqg
```

```go
// url = sia://EAAV-eT8wBIF1EPgT6WQkWWsb3mYyEO1xz9iFueK5zCtqg
```

Field        | Description
------------ | -----------
`skylink`    | This is the skylink that can be used when downloading to retrieve the file that has been uploaded. It is a 46-character base64 encoded string that consists of the merkle root, offset, fetch size, and Skylink version which can be used to access the content.
`merkleroot` | This is the hash that is encoded into the skylink.
`bitfield`   | This is the bitfield that gets encoded into the skylink. The bitfield contains a version, an offset and a length in a heavily compressed and optimized format.

## Uploading With Encryption

TODO