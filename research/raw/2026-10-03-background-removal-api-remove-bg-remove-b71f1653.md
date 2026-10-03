---
url: https://www.remove.bg/sv/api
retrieved: 2026-10-03
command: firecrawl scrape https://www.remove.bg/sv/api --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title:      Background Removal API – remove.bg   
---
[Hoppa till huvudinnehåll](https://www.remove.bg/sv/api#page-content)

remove.bgs bakgrundsborttagning flyttas till [Canva](https://www.canva.com/features/background-remover/?utm_source=RBG_website&utm_medium=removebg&utm_content=RBG_sunsetting_banner_page). Den fristående webbplatsen kommer inte längre att vara tillgänglig från den 1 december 2026 kl. 9:00 CET. Du kan [läsa mer här](https://www.remove.bg/faq) och se våra uppdaterade [allmänna villkor](https://www.remove.bg/gtc).

# Remove.bg API Documentation

![](https://static.remove.bg/remove-bg-web/dbfaec02d1e8bd04f1f132c4a92e4623d49a47a7/assets/leonardo_logo-e06c9d9a418a4cb1a3a21352985d1e0d43ff12aa44c7b06807d5c9f7f805fb25.svg)

## Do more with your background removal API

Starting December 1, 2026, background removal moves to Leonardo.Ai, also part of Canva. Same simple integration, plus a full creative toolkit that picks up right where background removal leaves off.


- Upscale automatically.Sharpen low-res product photos into marketplace-ready assets.

- Generate new scenes.
Place your cutout into any background, for lifestyle shots, seasonal refreshes, or A/B tests.



- Turn stills into video.
Animate product images with motion, transitions, and sound.


- Chain it into one call.
Combine all of the above and much more into a single Blueprint.


[Go to Leonardo.ai](https://docs.leonardo.ai/docs/remove-bg?utm_source=RBG_website&utm_medium=removebg&utm_content=RBG_api_docs) [Migration helper](https://docs.leonardo.ai/docs/migrate-from-the-removebg-api-to-leonardoai?utm_source=RBG_website&utm_medium=removebg&utm_content=RBG_api_docs)

## Remove Background automatically with 1 API call

Explore our API documentation and examples to integrate remove.bg into your application or workflow.


[Get API Key](https://www.remove.bg/sv/dashboard#api-key)

Not a developer?
There are plenty ready to use [Tools & Apps](https://www.remove.bg/sv/tools-api) by remove.bg and our community.


Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


## Easy to integrate

Our API is a simple HTTP interface with various options:


Source images:Direct uploads or URL referenceResult images:Image file or JSON-encoded dataOutput resolution:up to 50 megapixels
Requires images that [have a foreground (e.g. people, products, animals, cars, etc.)](https://www.remove.bg/sv/help/a/which-photos-work-best-for-high-quality-background-removal)

Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


![](https://static.remove.bg/remove-bg-web/dbfaec02d1e8bd04f1f132c4a92e4623d49a47a7/assets/api_thumb-450fd4fc2befdf499fa4c560f8f74aa2d6356013de373e8267f6b0bc7a5768ff.png)

## Get started

Our API is a simple HTTP interface with various options:


1. [Get your API Key](https://www.remove.bg/sv/dashboard#api-key).

Your first 50 API calls per month are on us (see [Pricing](https://www.remove.bg/sv/pricing)).

2. Use the following code samples to get started quickly

3. Review the reference docs to adjust any parameters


Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


![](https://static.remove.bg/remove-bg-web/dbfaec02d1e8bd04f1f132c4a92e4623d49a47a7/assets/api-docs/get-started-3f88bb44e89ead4d4873f18afadd6dab6dead7d94162632824a67cdd7d337451.png)

## Sample Code

Image FileImage URL

cURLNode.jsPythonRubyPHPJava.NETSwiftObjective-C

```bash
$ curl -H 'X-API-Key: INSERT_YOUR_API_KEY_HERE'           \
       -F 'image_file=@/path/to/file.jpg'                 \
       -F 'size=auto'                                     \
       -f https://api.remove.bg/v1.0/removebg -o no-bg.png
```

```javascript
import fs from "node:fs";

async function removeBg(blob) {
  const formData = new FormData();
  formData.append("size", "auto");
  formData.append("image_file", blob);

  const response = await fetch("https://api.remove.bg/v1.0/removebg", {
    method: "POST",
    headers: { "X-Api-Key": "INSERT_YOUR_API_KEY_HERE" },
    body: formData,
  });

  if (response.ok) {
    return await response.arrayBuffer();
  } else {
    throw new Error(`${response.status}: ${response.statusText}`);
  }
}

const inputPath = "/path/to/file.jpg";
const fileBlob = await fs.openAsBlob(inputPath)
const rbgResultData = await removeBg(fileBlob);
fs.writeFileSync("no-bg.png", Buffer.from(rbgResultData));
```

```python
# Requires "requests" to be installed (see python-requests.org)
import requests

response = requests.post(
    'https://api.remove.bg/v1.0/removebg',
    files={'image_file': open('/path/to/file.jpg', 'rb')},
    data={'size': 'auto'},
    headers={'X-Api-Key': 'INSERT_YOUR_API_KEY_HERE'},
)
if response.status_code == requests.codes.ok:
    with open('no-bg.png', 'wb') as out:
        out.write(response.content)
else:
    print("Error:", response.status_code, response.text)
```

```ruby
# Install "remove_bg" first (https://github.com/remove-bg/ruby)
require "remove_bg"

RemoveBg.from_file("/path/to/file.jpg",
  api_key: "INSERT_YOUR_API_KEY_HERE"
).save("no-bg.png")
```

```php
// Requires "guzzle" to be installed (see guzzlephp.org)
// If you have problems with our SSL certificate with error 'Uncaught GuzzleHttp\Exception\RequestException: cURL error 60: SSL certificate problem: unable to get local issuer certificate (see https://curl.haxx.se/libcurl/c/libcurl-errors.html) for https://api.remove.bg/v1.0/removebg'
// follow these steps to use the latest cacert certificate for cURL: https://github.com/guzzle/guzzle/issues/1935#issuecomment-371756738

$client = new GuzzleHttp\Client();
$res = $client->post('https://api.remove.bg/v1.0/removebg', [\
    'multipart' => [\
        [\
            'name'     => 'image_file',\
            'contents' => fopen('/path/to/file.jpg', 'r')\
        ],\
        [\
            'name'     => 'size',\
            'contents' => 'auto'\
        ]\
    ],\
    'headers' => [\
        'X-Api-Key' => 'INSERT_YOUR_API_KEY_HERE'\
    ]\
]);

$fp = fopen("no-bg.png", "wb");
fwrite($fp, $res->getBody());
fclose($fp);
```

```java
// Requires "Apache HttpComponents" to be installed (see hc.apache.org)

Response response = Request.Post("https://api.remove.bg/v1.0/removebg")
    .addHeader("X-Api-Key", "INSERT_YOUR_API_KEY_HERE")
    .body(
        MultipartEntityBuilder.create()
        .addBinaryBody("image_file", new File("/path/to/file.jpg"))
        .addTextBody("size", "auto")
        .build()
    ).execute();
response.saveContent(new File("no-bg.png"));
```

```objectivec
// Requires AFNetworking to be installed (see https://github.com/AFNetworking/AFNetworking)

NSURL *fileUrl = [NSBundle.mainBundle URLForResource:@"file" withExtension:@"jpg"];
NSData *data = [NSData dataWithContentsOfURL:fileUrl];
if (!data) {
    return;
}

AFHTTPSessionManager *manager =
[[AFHTTPSessionManager alloc] initWithSessionConfiguration:\
 NSURLSessionConfiguration.defaultSessionConfiguration];

manager.responseSerializer = [AFImageResponseSerializer serializer];
[manager.requestSerializer setValue:@"INSERT_YOUR_API_KEY_HERE"\
                 forHTTPHeaderField:@"X-Api-Key"];

NSURLSessionDataTask *dataTask = [manager\
                                  POST:@"https://api.remove.bg/v1.0/removebg"\
                                  parameters:nil\
                                  constructingBodyWithBlock:^(id  _Nonnull formData) {\
                                      [formData appendPartWithFileData:data\
                                                                  name:@"image_file"\
                                                              fileName:@"file.jpg"\
                                                              mimeType:@"image/jpeg"];\
                                  }\
                                  progress:nil\
                                  success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {\
                                      if ([responseObject isKindOfClass:UIImage.class] == false) {\
                                          return;\
                                      }\
\
                                      self.imageView.image = responseObject;\
                                  } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {\
                                      // Handle error here\
                                  }];

[dataTask resume];
```

```swift
// Requires Alamofire 5 to be installed (see https://github.com/Alamofire/Alamofire)

guard let fileUrl = Bundle.main.url(forResource: "file", withExtension: "jpg"),
  let imageData = try? Data(contentsOf: fileUrl)
else { return false }

struct HTTPBinResponse: Decodable { let url: String }

AF.upload(
  multipartFormData: { builder in
    builder.append(
      data: imageData,
      withName: "image_file",
      fileName: "file.jpg",
      mimeType: "image/jpeg"
    )
  },
  to: URL(string: "https://api.remove.bg/v1.0/removebg")!,
  headers: [\
    "X-Api-Key": "INSERT_YOUR_API_KEY_HERE"\
  ]
).responseDecodable(of: HTTPBinResponse.self) { imageResponse in
  guard let imageData = imageResponse.data,
    let image = UIImage(data: imageData)
  else { return }

  self.imageView.image = image
}
```

```csharp
using (var client = new HttpClient())
using (var formData = new MultipartFormDataContent())
{
    formData.Headers.Add("X-Api-Key", "INSERT_YOUR_API_KEY_HERE");
    formData.Add(new ByteArrayContent(File.ReadAllBytes("/path/to/file.jpg")), "image_file", "file.jpg");
    formData.Add(new StringContent("auto"), "size");
    var response = client.PostAsync("https://api.remove.bg/v1.0/removebg", formData).Result;

    if(response.IsSuccessStatusCode) {
        FileStream fileStream = new FileStream("no-bg.png", FileMode.Create, FileAccess.Write, FileShare.None);
        response.Content.CopyToAsync(fileStream).ContinueWith((copyTask) =>{ fileStream.Close(); });
    } else {
        Console.WriteLine("Error: " + response.Content.ReadAsStringAsync().Result);
    }
}
```

```bash
$ curl -H 'X-API-Key: INSERT_YOUR_API_KEY_HERE'           \
       -F 'image_url=https://www.remove.bg/example.jpg'   \
       -F 'size=auto'                                     \
       -f https://api.remove.bg/v1.0/removebg -o no-bg.png
```

```javascript
import fs from "node:fs";

async function removeBg(imageURL) {
  const formData = new FormData();
  formData.append("size", "auto");
  formData.append("image_url", imageURL);

  const response = await fetch("https://api.remove.bg/v1.0/removebg", {
    method: "POST",
    headers: { "X-Api-Key": "INSERT_YOUR_API_KEY_HERE" },
    body: formData,
  });

  if (response.ok) {
    return await response.arrayBuffer();
  } else {
    throw new Error(`${response.status}: ${response.statusText}`);
  }
}

const rbgResultData = await removeBg("https://www.remove.bg/example.jpg");
fs.writeFileSync("no-bg.png", Buffer.from(rbgResultData));
```

```python
# Requires "requests" to be installed (see python-requests.org)
import requests

response = requests.post(
    'https://api.remove.bg/v1.0/removebg',
    data={
        'image_url': 'https://www.remove.bg/example.jpg',
        'size': 'auto'
    },
    headers={'X-Api-Key': 'INSERT_YOUR_API_KEY_HERE'},
)
if response.status_code == requests.codes.ok:
    with open('no-bg.png', 'wb') as out:
        out.write(response.content)
else:
    print("Error:", response.status_code, response.text)
```

```ruby
# Install "remove_bg" first (https://github.com/remove-bg/ruby)
require "remove_bg"

RemoveBg.from_url("https://www.remove.bg/example.jpg",
  api_key: "INSERT_YOUR_API_KEY_HERE"
).save("no-bg.png")
```

```php
// Requires "guzzle" to be installed (see guzzlephp.org)
// If you have problems with our SSL certificate getting the error 'Uncaught GuzzleHttp\Exception\RequestException: cURL error 60: SSL certificate problem: unable to get local issuer certificate (see https://curl.haxx.se/libcurl/c/libcurl-errors.html) for https://api.remove.bg/v1.0/removebg'
// follow these steps to use the latest cacert certificate for cURL: https://github.com/guzzle/guzzle/issues/1935#issuecomment-371756738

$client = new GuzzleHttp\Client();
$res = $client->post('https://api.remove.bg/v1.0/removebg', [\
    'multipart' => [\
        [\
            'name'     => 'image_url',\
            'contents' => 'https://www.remove.bg/example.jpg'\
        ],\
        [\
            'name'     => 'size',\
            'contents' => 'auto'\
        ]\
    ],\
    'headers' => [\
        'X-Api-Key' => 'INSERT_YOUR_API_KEY_HERE'\
    ]\
]);

$fp = fopen("no-bg.png", "wb");
fwrite($fp, $res->getBody());
fclose($fp);
```

```java
// Requires "Apache HttpComponents" to be installed (see hc.apache.org)

Response response = Request.Post("https://api.remove.bg/v1.0/removebg")
    .addHeader("X-Api-Key", "INSERT_YOUR_API_KEY_HERE")
    .body(
        MultipartEntityBuilder.create()
        .addTextBody("image_url", "https://www.remove.bg/example.jpg")
        .addTextBody("size", "auto")
        .build()
    ).execute();
response.saveContent(new File("no-bg.png"));
```

```objectivec
// Requires AFNetworking to be installed (see https://github.com/AFNetworking/AFNetworking)

AFHTTPSessionManager *manager =
[[AFHTTPSessionManager alloc] initWithSessionConfiguration:\
 NSURLSessionConfiguration.defaultSessionConfiguration];

manager.responseSerializer = [AFImageResponseSerializer serializer];
[manager.requestSerializer setValue:@"INSERT_YOUR_API_KEY_HERE"\
                 forHTTPHeaderField:@"X-Api-Key"];

NSURLSessionDataTask *dataTask = [manager\
                                  POST:@"https://api.remove.bg/v1.0/removebg"\
                                  parameters:@{@"image_url": @"https://www.remove.bg/example.jpg"}\
                                  progress:nil\
                                  success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {\
                                      if ([responseObject isKindOfClass:UIImage.class] == false) {\
                                          return;\
                                      }\
\
                                      self.imageView.image = responseObject;\
                                  } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {\
                                      NSLog(@"ERROR");\
                                  }];
[dataTask resume];
```

```swift
// Requires Alamofire 5 to be installed (see https://github.com/Alamofire/Alamofire)

AF.request(
  URL(string: "https://api.remove.bg/v1.0/removebg")!,
  method: .post,
  parameters: ["image_url": "https://www.remove.bg/example.jpg"],
  encoding: URLEncoding(),
  headers: [\
    "X-Api-Key": "INSERT_YOUR_API_KEY_HERE"\
  ]
)
.responseData { imageResponse in
  guard let imageData = imageResponse.data,
    let image = UIImage(data: imageData)
  else { return }

  self.imageView.image = image
}
```

```csharp
using (var client = new HttpClient())
using (var formData = new MultipartFormDataContent())
{
    formData.Headers.Add("X-Api-Key", "INSERT_YOUR_API_KEY_HERE");
    formData.Add(new StringContent("https://www.remove.bg/example.jpg"), "image_url");
    formData.Add(new StringContent("auto"), "size");
    var response = client.PostAsync("https://api.remove.bg/v1.0/removebg", formData).Result;

    if(response.IsSuccessStatusCode) {
        FileStream fileStream = new FileStream("no-bg.png", FileMode.Create, FileAccess.Write, FileShare.None);
        response.Content.CopyToAsync(fileStream).ContinueWith((copyTask) =>{ fileStream.Close(); });
    } else {
        Console.WriteLine("Error: " + response.Content.ReadAsStringAsync().Result);
    }
}
```

Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


## Libraries

Get up and running faster with official and third-party libraries.


Not a developer?
There are plenty ready to use [Tools & Apps](https://www.remove.bg/sv/tools-api) by remove.bg and our community.


Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


[Official\\
\\
\\
**Commandline Tool**\\
Official\\
\\
\\
by remove.bg](https://github.com/remove-bg/remove-bg-cli) [Official\\
\\
\\
**Ruby Gem**\\
Official\\
\\
\\
by remove.bg](https://github.com/remove-bg/ruby) [**PHP/Laravel Library**\\
\\
by @mtownsend5512](https://github.com/mtownsend5512/remove-bg) [**Node.js: remove.bg**\\
\\
by @eddyverbruggen](https://www.npmjs.com/package/remove.bg) [**Node.js: removd**\\
\\
by @przemyslawpluta](https://www.npmjs.com/package/removd) [**Python: remove.bg**\\
\\
by Brian Lam](https://github.com/brilam/remove-bg)

## Output formats

You can request one of four formats via the `format` parameter:


| Format | Resolution | Pros and cons | Example |
| --- | --- | --- | --- |
| PNG | Up to 10 Megapixels<br>e.g. 4000x2500 | \+ Simple integration<br> \+ Supports transparency<br> \- Large file size | [**Download**\<br>\<br>7 MB](https://static.remove.bg/remove-bg-web/dbfaec02d1e8bd04f1f132c4a92e4623d49a47a7/assets/api-docs/example-tiger-9e6b2856e0b8c62af1e4c1a2b7b7d759f4653c7ba1f8f8e9b9fcc92edd25338a.png) |
| JPG | Up to 50 Megapixels<br>e.g. 8000x6250 | \+ Simple Integration<br> \+ Smallest file size<br> \- No transparency supported | [**Download**\<br>\<br>1 MB](https://static.remove.bg/remove-bg-web/dbfaec02d1e8bd04f1f132c4a92e4623d49a47a7/assets/api-docs/example-tiger-d82d433bc9f0867381c7dd43d3042a3d86de34fd58b9fb4ed082bbcd5ccf10c3.jpg) |
| WebP | Up to 50 Megapixels<br>e.g. 8000x6250 | \+ Simple integration<br> \+ Supports transparency<br> \- Not universally supported file format | [**Download**\<br>\<br>6 MB](https://static.remove.bg/remove-bg-web/dbfaec02d1e8bd04f1f132c4a92e4623d49a47a7/assets/api-docs/example-tiger-512675bb89935ab63898cfc224e9373656be38f19fa59509cc3a580c3850db4b.webp) |
| ZIP | Up to 50 Megapixels<br>e.g. 8000x6250 | \+ Fastest<br> \+ Small file size<br> \+ Supports transparency<br> \- Integration requires composition | [**Download**\<br>\<br>3 MB](https://static.remove.bg/remove-bg-web/dbfaec02d1e8bd04f1f132c4a92e4623d49a47a7/assets/api-docs/example-tiger-ea002b3b176b23e988a97e33dffa25960a19529bb0adcb5c75a96dbab189e7b3.zip) |

Please note that **PNG images above 10 megapixels are not supported**. If you require transparency for images of that size, use either WebP or ZIP format (see below). For the fastest processing we recommend the ZIP format. If you don't need transparency (e.g. white background), we recommend JPG.


Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


## How to use the ZIP format

The ZIP format has the best runtime performance for transparent images.


In comparison to PNG, the resulting file is up to 80% smaller (faster to download) and up to 40% faster to generate. For performance optimization we recommend using the ZIP format whenever possible.


The ZIP file always contains the following files:


|     |     |
| --- | --- |
| **color.jpg** | A non-transparent RGB image in JPG format containing the colors for each pixel. (Note: This image differs from the input image due to edge color corrections.)<br> –<br> [Show example](https://static.remove.bg/remove-bg-web/dbfaec02d1e8bd04f1f132c4a92e4623d49a47a7/assets/api-docs/example-tiger-color-ed5f90da1ab8a94dbba5986580d7e76cde84b2b1ce6d44de2d86d186658e7332.jpg) |
| **alpha.png** | A non-transparent grayscale image in PNG format containing the alpha matte. White pixels are foreground regions, black is background.<br> –<br> [Show example](https://static.remove.bg/remove-bg-web/dbfaec02d1e8bd04f1f132c4a92e4623d49a47a7/assets/api-docs/example-tiger-alpha-e0ae0f94e34a25f1e9bd7a2a68a0bb34f1568a5bcdadd62e623b5cb021981032.png) |

To compose the final image file:


1. Extract the files from the ZIP

2. Apply the alpha matte (alpha.png) to the color image (color.jpg).

3. Save the result in a format of your choice (e.g. PNG)


**Sample code for linux** (requires [zip](http://infozip.sourceforge.net/) and [imagemagick](https://imagemagick.org/)):

```bash
$ unzip no-bg.zip                      && \
  convert color.jpg alpha.png             \
    -compose CopyOpacity                  \
    -composite no-bg.png
```

A `zip2png` command is integrated in our [command line interface](https://github.com/remove-bg/remove-bg-cli/). More code samples can be found [here](https://github.com/remove-bg/integration/tree/master/).


Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


## OAuth 2.0

If you want to authenticate users with the click of a button instead of having them enter an API Key, [get in touch](https://www.remove.bg/sv/support/contact?subject=OAuth+2.0+Login) to try our OAuth 2.0 login.


Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


## API Reference

Please view this page on on a larger device to see the full API Reference.


Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


## Rate Limit

You can process up to **500 images per minute** through the API, depending on the input image resolution in megapixels.


Examples:


| Input image | Megapixels | Effective Rate Limit |
| --- | --- | --- |
| 625 x 400 | 1<br> MP | 500 images per minute |
| 1200 x 800 | 1<br> MP | 500 images per minute |
| 1600 x 1200 | 2<br> MP | 500 / 2 =<br> 250 images per minute |
| 2500 x 1600 | 4<br> MP | 500 / 4 =<br> 125 images per minute |
| 4000 x 2500 | 10<br> MP | 500 / 10 =<br> 50 images per minute |
| 6250 x 4000 | 25<br> MP | 500 / 25 =<br> 20 images per minute |
| 8000 x 6250 | 50<br> MP | 500 / 50 =<br> 10 images per minute |

Exceedance of rate limits leads to a HTTP status 429 response (no credits charged). Clients can use the following response headers to gracefully handle rate limits:


| Response header | Sample value | Description |
| --- | --- | --- |
| `X-RateLimit-Limit` | `500` | Total rate limit in megapixel images |
| `X-RateLimit-Remaining` | `499` | Remaining rate limit for this minute |
| `X-RateLimit-Reset` | `1791013479` | Unix timestamp when rate limit will reset |
| `Retry-After` | `59` | Seconds until rate limit will reset (only present if rate limit exceeded) |

Higher rate limits are only available to high-volume solution users; get in touch [here](https://www.remove.bg/sv/enterprise/contact).


### Sample Code

Handling Rate Limits in your code using the HTTP `Retry-After` header:

Rate Limit

cURLNode.jsPythonRubyPHPJava.NETSwiftObjective-C

```bash
#!/bin/bash

make_request_with_retry() {
    while true; do
        response=$(get_result)
        status_code=$(echo "$response" | grep HTTP | awk '{print $2}')

        if [ "$status_code" -eq 200 ]; then
            echo "$response" | grep -v HTTP
            return
        elif [ "$status_code" -eq 429 ]; then
            retry_after=$(echo "$response" | grep -i "Retry-After" | awk '{print $2}')
            if [ -n "$retry_after" ]; then
                echo "Rate limit reached. Retrying after $retry_after seconds..."
                sleep "$retry_after"
            else
                echo "Rate limit reached. Retrying after a default delay..."
                sleep 10  # Default fallback delay
            fi
        else
            echo "Request failed with status code $status_code"
            exit 1
        fi
    done
}

get_result() {
    # Placeholder for actual API call logic
    # Example
    curl -i -s -X POST "https://api.remove.bg/v1.0/removebg" \
    -H "Content-Type: application/json" \
    -d '{"image_url":"https://www.remove.bg/example.jpg"}'
    echo "HTTP/1.1 429 Too Many Requests"
    echo "Retry-After: 5"
}

make_request_with_retry
```

```javascript
async function makeRequestWithRetry() {
    while (true) {
        const response = await getResult();
        if (response.status === 200) {
            return await response.json();
        } else if (response.status === 429) {
            const retryAfter = response.headers.get("Retry-After");
            if (retryAfter) {
                console.log(`Rate limit reached. Retrying after ${retryAfter} seconds...`);
                await new Promise(resolve => setTimeout(resolve, retryAfter * 1000));
            } else {
                console.log("Rate limit reached. Retrying after a default delay...");
                await new Promise(resolve => setTimeout(resolve, 10000));  // Default fallback delay
            }
        } else {
            throw new Error(`Request failed with status ${response.status}`);
        }
    }
}

async function getResult() {
    // Placeholder for actual API call logic
}
```

```python
import requests
import time

async def make_request_with_retry():
    while True:
        response = get_result()
        if response.status_code == 200:
            return response.json()
        elif response.status_code == 429:
            retry_after = response.headers.get("Retry-After")
            if retry_after:
                print(f"Rate limit reached. Retrying after {retry_after} seconds...")
                time.sleep(int(retry_after))
            else:
                print("Rate limit reached. Retrying after a default delay...")
                time.sleep(10)  # Default fallback delay
        else:
            response.raise_for_status()

async def get_result():
    # Placeholder for actual API call logic
    pass
```

```ruby
require 'net/http'
require 'json'
require 'async'

async def make_request_with_retry
    loop do
        response = get_result
        case response.code.to_i
        when 200
            return JSON.parse(response.body)
        when 429
            retry_after = response['Retry-After']
            if retry_after
                puts "Rate limit reached. Retrying after #{retry_after} seconds..."
                sleep retry_after.to_i
            else
                puts "Rate limit reached. Retrying after a default delay..."
                sleep 10  # Default fallback delay
            end
        else
            response.value  # Raises an HTTP error if the response is not 2xx
        end
    end
end

async def get_result
    # Placeholder for actual API call logic
    uri = URI('https://api.remove.bg/v1.0/removebg')
    Net::HTTP.get_response(uri)
end
```

```php
function make_request_with_retry() {
    while (true) {
        $response = get_result();
        if ($response->getStatusCode() == 200) {
            return json_decode($response->getBody(), true);
        } elseif ($response->getStatusCode() == 429) {
            $retry_after = $response->getHeader('Retry-After');
            if ($retry_after) {
                echo "Rate limit reached. Retrying after {$retry_after[0]} seconds...\n";
                sleep((int)$retry_after[0]);
            } else {
                echo "Rate limit reached. Retrying after a default delay...\n";
                sleep(10);  // Default fallback delay
            }
        } else {
            throw new Exception("HTTP request failed with status code " . $response->getStatusCode());
        }
    }
}

function get_result() {
    // Placeholder for actual API call logic
}
```

```java
import java.io.IOException;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.concurrent.TimeUnit;

public class RateLimitExample {

    public static void main(String[] args) {
        try {
            makeRequestWithRetry();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }

    public static void makeRequestWithRetry() throws IOException, InterruptedException {
        while (true) {
            HttpURLConnection connection = getResult();
            int statusCode = connection.getResponseCode();
            if (statusCode == 200) {
                // Handle successful response
                break;
            } else if (statusCode == 429) {
                String retryAfter = connection.getHeaderField("Retry-After");
                if (retryAfter != null) {
                    System.out.println("Rate limit reached. Retrying after " + retryAfter + " seconds...");
                    TimeUnit.SECONDS.sleep(Integer.parseInt(retryAfter));
                } else {
                    System.out.println("Rate limit reached. Retrying after a default delay...");
                    TimeUnit.SECONDS.sleep(10);  // Default fallback delay
                }
            } else {
                throw new IOException("Unexpected response code: " + statusCode);
            }
        }
    }

    public static HttpURLConnection getResult() throws IOException {
        // Placeholder for actual API call logic
        URL url = new URL("https://api.remove.bg/v1.0/removebg");
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        connection.setRequestMethod("POST");
        connection.setRequestProperty("Content-Type", "application/json");
        connection.setDoOutput(true);
        String jsonInputString = "{\"image_url\":\"https://www.remove.bg/example.jpg\"}";
        try (OutputStream os = connection.getOutputStream()) {
            byte[] input = jsonInputString.getBytes("utf-8");
            os.write(input, 0, input.length);
        }
        return connection;
    }
}
```

```objectivec
#import

@interface RateLimiter : NSObject

- (void)makeRequestWithRetry;

@end

@implementation RateLimiter

- (void)makeRequestWithRetry {
    while (YES) {
        NSDictionary *response = [self getResult];
        NSInteger statusCode = [response[@"statusCode"] integerValue];

        if (statusCode == 200) {
            NSLog(@"%@", response[@"data"]);
            return;
        } else if (statusCode == 429) {
            NSString *retryAfter = response[@"headers"][@"Retry-After"];
            if (retryAfter) {
                NSLog(@"Rate limit reached. Retrying after %@ seconds...", retryAfter);
                [NSThread sleepForTimeInterval:[retryAfter intValue]];
            } else {
                NSLog(@"Rate limit reached. Retrying after a default delay...");
                [NSThread sleepForTimeInterval:10];
            }
        } else {
            [NSException raise:@"RequestFailed" format:@"Request failed with status code: %ld", (long)statusCode];
        }
    }
}

- (NSDictionary *)getResult {
    // Placeholder for actual API call logic
    return @{};
}

@end
```

```swift
import Foundation
import FoundationNetworking

func makeRequestWithRetry(completion: @escaping (Result<>) -> Void) {
    var requestBody = [\
        "image_url": "https://www.remove.bg/example.jpg"\
    ]
    let url = URL(string: "https://api.remove.bg/v1.0/removebg")!
    var request = URLRequest(url: url)
    request.httpBody = try? JSONSerialization.data(withJSONObject: requestBody, options: [])
    request.setValue("application/json", forHTTPHeaderField: "Content-Type")

    func executeRequest() {
        let task = URLSession.shared.dataTask(with: request) { responseData, response, error in
            if let error = error {
                completion(.failure(error))
                return
            }

            guard let httpResponse = response as? HTTPURLResponse else {
                completion(.failure(NSError(domain: "InvalidResponse", code: 0, userInfo: nil)))
                return
            }

            switch httpResponse.statusCode {
            case 200:
                if let responseData = responseData {
                    completion(.success(responseData))
                } else {
                    completion(.failure(NSError(domain: "NoData", code: 0, userInfo: nil)))
                }
            case 429:
                if let retryAfter = httpResponse.allHeaderFields["Retry-After"] as? String, let retryAfterSeconds = Double(retryAfter) {
                    print("Rate limit reached. Retrying after \(retryAfterSeconds) seconds...")
                    DispatchQueue.global().asyncAfter(deadline: .now() + retryAfterSeconds) {
                        executeRequest()
                    }
                } else {
                    print("Rate limit reached. Retrying after a default delay...")
                    DispatchQueue.global().asyncAfter(deadline: .now() + 10) {
                        executeRequest()
                    }
                }
            default:
                completion(.failure(NSError(domain: "HTTPError", code: httpResponse.statusCode, userInfo: nil)))
            }
        }
        task.resume()
    }

    executeRequest()
}
```

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class RateLimitExample
{
    private static readonly HttpClient client = new HttpClient();

    public static async Task Main(string[] args)
    {
        var result = await MakeRequestWithRetry();
        Console.WriteLine(result);
    }

    private static async Task MakeRequestWithRetry()
    {
        while (true)
        {
            var response = await GetResult();
            if (response.IsSuccessStatusCode)
            {
                return await response.Content.ReadAsStringAsync();
            }
            else if (response.StatusCode == (System.Net.HttpStatusCode)429)
            {
                if (response.Headers.TryGetValues("Retry-After", out var values))
                {
                    var retryAfter = int.Parse(values.First());
                    Console.WriteLine($"Rate limit reached. Retrying after {retryAfter} seconds...");
                    await Task.Delay(retryAfter * 1000);
                }
                else
                {
                    Console.WriteLine("Rate limit reached. Retrying after a default delay...");
                    await Task.Delay(10000); // Default fallback delay
                }
            }
            else
            {
                response.EnsureSuccessStatusCode();
            }
        }
    }

    private static async Task GetResult()
    {
        // Placeholder for actual API call logic
        var content = new StringContent("{\"image_url\":\"https://www.remove.bg/example.jpg\"}", System.Text.Encoding.UTF8, "application/json");
        return await client.PostAsync("https://api.remove.bg/v1.0/removebg", content);
    }
}
```

Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


## Exponential backoff

Exponential backoff is an error handling strategy in which a client periodically retries a failed request. This technique reduces the number of failed requests and prevents server overload by gradually increasing the waiting time between retries.


The delay increases between requests and often includes jitter (randomized delay) to avoid collisions when using concurrent clients.

Clients should use exponential backoff whenever they receive a `5XX` HTTP status code, such as `503 - Service Unavailable`.


As a general rule, this should be avoided in case of `429 - Too Many Requests`, as they are usually caused by client-side issues.


### Sample Code

Exponential Backoff

cURLNode.jsPythonRubyPHPJava.NETSwiftObjective-C

```bash
#!/bin/bash

MAX_RETRIES=5

call_api_with_exponential_backoff() {
  local retry=true
  local retries=0

  while $retry && [ $retries -lt $MAX_RETRIES ]; do
    local wait_time=$(echo "2^$retries + $RANDOM/32768" | bc -l)
    sleep $wait_time

    local result=$(get_result) # Assume this function retrieves the result

    if [ "$result" == "SUCCESS" ]; then
      retry=false
    elif [ "$result" == "ERROR" ] || [ "$result" == "THROTTLED" ]; then
      retry=true
    fi

    retries=$((retries + 1))
  done
}

get_result() {
  # Placeholder for actual API call logic
}
```

```javascript
const MAX_RETRIES = 5;

async function callApiWithExponentialBackoff() {
    let retry = true;
    let retries = 0;

    while (retry && retries < MAX_RETRIES) {
        const waitTime = Math.pow(2, retries) + Math.random(); // random_number in seconds
        await new Promise(resolve => setTimeout(resolve, waitTime * 1000)); // convert to milliseconds

        const result = await getResult(); // Assume this function retrieves the result

        if (result === 'SUCCESS') {
            retry = false;
        } else if (result === 'ERROR' || result === 'THROTTLED') {
            retry = true;
        }

        retries++;
    }
}

async function getResult() {
    // Placeholder for actual API call logic
}
```

```python
import time
import random

MAX_RETRIES = 5

async def call_api_with_exponential_backoff():
    retry = True
    retries = 0

    while retry and retries < MAX_RETRIES:
        wait_time = 2 ** retries + random.random()  # random_number in seconds
        await asyncio.sleep(wait_time)  # convert to milliseconds

        result = await get_result()  # Assume this function retrieves the result

        if result == 'SUCCESS':
            retry = False
        elif result in ['ERROR', 'THROTTLED']:
            retry = True

        retries += 1

async def get_result():
    # Placeholder for actual API call logic
    pass
```

```ruby
MAX_RETRIES = 5

def call_api_with_exponential_backoff
    retry = true
    retries = 0

    while retry && retries < MAX_RETRIES
        wait_time = 2**retries + rand # random_number in seconds
        sleep(wait_time) # convert to seconds

        result = get_result # Assume this function retrieves the result

        if result == 'SUCCESS'
            retry = false
        elsif result == 'ERROR' || result == 'THROTTLED'
            retry = true
        end

        retries += 1
    end
end

def get_result
    # Placeholder for actual API call logic
end
```

```php
define('MAX_RETRIES', 5);

function callApiWithExponentialBackoff() {
    $retry = true;
    $retries = 0;

    while ($retry && $retries < MAX_RETRIES) {
        $waitTime = pow(2, $retries) + mt_rand() / mt_getrandmax(); // random_number in seconds
        usleep($waitTime * 1000000); // convert to microseconds

        $result = getResult(); // Assume this function retrieves the result

        if ($result === 'SUCCESS') {
            $retry = false;
        } else if ($result === 'ERROR' || $result === 'THROTTLED') {
            $retry = true;
        }

        $retries++;
    }
}

function getResult() {
    // Placeholder for actual API call logic
}
```

```java
import java.util.Random;

public class ExponentialBackoff {

    private static final int MAX_RETRIES = 5;

    public static void main(String[] args) {
        try {
            callApiWithExponentialBackoff();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public static void callApiWithExponentialBackoff() throws InterruptedException {
        boolean retry = true;
        int retries = 0;
        Random random = new Random();

        while (retry && retries < MAX_RETRIES) {
            double waitTime = Math.pow(2, retries) + random.nextDouble(); // random_number in seconds
            Thread.sleep((long) (waitTime * 1000)); // convert to milliseconds

            String result = getResult(); // Assume this function retrieves the result

            if ("SUCCESS".equals(result)) {
                retry = false;
            } else if ("ERROR".equals(result) || "THROTTLED".equals(result)) {
                retry = true;
            }

            retries++;
        }
    }

    public static String getResult() {
        // Placeholder for actual API call logic
        return "SUCCESS"; // Example return value
    }
}
```

```objectivec
#define MAX_RETRIES 5

- (void)callApiWithExponentialBackoff {
    __block BOOL retry = YES;
    __block int retries = 0;

    void (^retryBlock)(void) = ^{
        if (retry && retries < MAX_RETRIES) {
            double waitTime = pow(2, retries) + ((double)arc4random() / UINT32_MAX);
            dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(waitTime * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
                [self getResultWithCompletion:^(NSString *result) {\
                    if ([result isEqualToString:@"SUCCESS"]) {\
                        retry = NO;\
                    } else if ([result isEqualToString:@"ERROR"] || [result isEqualToString:@"THROTTLED"]) {\
                        retry = YES;\
                    }\
                    retries++;\
                    retryBlock();\
                }];
            });
        }
    };

    retryBlock();
}

- (void)getResultWithCompletion:(void (^)(NSString *result))completion {
    // Placeholder for actual API call logic
    // Call completion with the result, e.g., completion(@"SUCCESS");
}
```

```swift
import Foundation

let MAX_RETRIES = 5

func callApiWithExponentialBackoff() async {
    var retry = true
    var retries = 0

    while retry && retries < MAX_RETRIES {
        let waitTime = pow(2.0, Double(retries)) + Double.random(in: 0..<1)
        try? await Task.sleep(nanoseconds: UInt64(waitTime * 1_000_000_000)) // convert to nanoseconds

        let result = await getResult() // Assume this function retrieves the result

        if result == "SUCCESS" {
            retry = false
        } else if result == "ERROR" || result == "THROTTLED" {
            retry = true
        }

        retries += 1
    }
}

func getResult() async -> String {
    // Placeholder for actual API call logic
    return "SUCCESS" // Example return value
}
```

```csharp
const int MAX_RETRIES = 5;

public async Task CallApiWithExponentialBackoff()
{
  bool retry = true;
  int retries = 0;

  while (retry && retries < MAX_RETRIES)
  {
    double waitTime = Math.Pow(2, retries) + new Random().NextDouble(); // random_number in seconds
    await Task.Delay(TimeSpan.FromSeconds(waitTime)); // convert to milliseconds

    string result = await GetResult(); // Assume this function retrieves the result

    if (result == "SUCCESS")
    {
      retry = false;
    }
    else if (result == "ERROR" || result == "THROTTLED")
    {
      retry = true;
    }

    retries++;
  }
}

public async Task GetResult()
{
  // Placeholder for actual API call logic
  return "SUCCESS"; // Example return value
}
```

Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


## API Changelog

Most recent API updates:


- **2025-04-07:** Drop Shadow is now more consistent across images, regardless of their resolution.

- **2025-03-31:** Added support for WebP as an accepted input and output image format.

- **2024-12-13:** Added code samples and tips in the Exponential Backoff section.

- **2024-06-03:** Introduced new parameters: `shadow_type` and `shadow_opacity`. Deprecated parameter: `add_shadow`. Extended `type` parameter with new values: "graphic", "transportation" and "animal".

- **2024-03-17:** Added new value for size parameter: `50MP` for up to 50 megapixels (e.g., 8000x6250 pixels) with formats ZIP or JPG, or up to 10 megapixels (e.g., 4000x2500 pixels) with PNG – costs 1 credit per image. The "auto" option keeps supporting a maximum of 25MP for backwards compatibility.

- **2024-01-10:** Final reminder - Deprecation of `TLS 1.0` and `1.1`. Upgrade to `TLS 1.2` or higher for uninterrupted service before 2024-02-05.

- **2023-12-06:** Second notice - Deprecation of `TLS 1.0` and `1.1`. Upgrade to `TLS 1.2` or higher for uninterrupted service before 2024-02-05.

- **2023-11-22:** First notice - Deprecation of `TLS 1.0` and `1.1`. Upgrade to `TLS 1.2` or higher for uninterrupted service before 2024-02-05.

- **2021-12-07:** Added foreground position and size to background removal responses. (JSON fields: `foreground_top`,
`foreground_left`, `foreground_width` and `foreground_height`. Response headers:
`X-Foreground-Top`, `X-Foreground-Left`, `X-Foreground-Width` and `X-Foreground-Height`.)

- **2021-04-13:** Removed deprecated `shadow_method=legacy` option and `shadow_method` parameter as it no longer has any effect.

- **2021-03-01:** Added examples for `400` error codes.

- **2021-01-21:** Added `shadow_method` parameter to control shadow appearance. Deprecated `legacy` value for `shadow_method`.

- **2020-09-30:** Added `type_level` parameter and `POST /improve` endpoint.

- **2020-05-06:** Added `semitransparency` parameter.

- **2019-09-27:** Introduce ZIP format and support for images up to 25 megapixels.

- **2019-09-25:** Increased maximum file size to 12 MB and rate limit to 500 images per minute. Rate limit is now resolution-dependent.

- **2019-09-16:** Added `enterprise` credit balance field to account endpoint.

- **2019-08-01:** Added `add_shadow` option for car images.

- **2019-06-26:** Added `crop_margin`, `scale` and `position` parameters.

- **2019-06-19:** Added support for animals and other foregrounds (response header `X-Type: animal` and `X-Type: other`)

- **2019-06-11:** Credit balances can now have fractional digits, this affects the `X-Credits-Charged` value

- **2019-06-03:** Added parameters `bg_image_url`, `bg_image_file` (add a background image), `crop` (crop off empty regions) and `roi` (specify a region of interest).

- **2019-05-13:** Added car support (`type=car` parameter and `X-Type: car` response header)

- **2019-05-02:** Renamed size `"regular"` to `"small"`. Clients should use the new value, but the old one will continue to work (deprecated)

- **2019-05-01:** Added endpoint `GET /account` for credit balance lookups

- **2019-04-15:** Added parameter `format` to set the result image format

- **2019-04-15:** Added parameter `bg_color` to add a background color to the result image


Was this section helpful?
YesNo

Send Feedback

Thanks for your feedback.


### Tack för din feedback!

Vill du hjälpa oss att bli bättre? (valfritt)

- Bidra med den här bilden och hjälp oss att göra remove.bg bättre

- Lär ut den artificiella intelligensen

- Få bättre resultat för liknande bilder i framtiden


Jag samtycker till [Villkor för förbättringsprogram](https://www.remove.bg/sv/ipc).\*

Kom ihåg mitt beslut för framtida bilder som jag betygsätter negativt


Ja, bidra med bild


Välj om du vill att vi ska använda den här bilden för kvalitetsförbättringar.


Nej, bidra inte


Välj om du INTE vill att vi ska använda den här bilden för kvalitetsförbättringar.


Din bild kommer att användas för framtida förbättringar av remove.bg.

Stäng

Din bild kommer INTE att användas för framtida förbättringar av remove.bg.

Stäng

Genom att använda remove.bg samtycker du till användningen av cookies. Du kan hitta information om hur vi använder cookies i vår [Cookiepolicy](https://www.remove.bg/sv/cookies).

Stäng
