---
url: https://www.slazzer.com/api
retrieved: 2026-10-02
command: firecrawl scrape https://www.slazzer.com/api --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Background Removal API – slazzer.com
---
We use cookies, by continuing to use this site you accept our use of cookies.
To learn more visit our
[privacy policy.](https://www.slazzer.com/privacy-policy "")

Close

![Close](https://www.slazzer.com/static/images/close.svg)![Slazzer logo](https://www.slazzer.com/static/images/logo-icon.svg)

###### Slazzer App

All-in-one AI photo editor

[Get App](https://play.google.com/store/search?q=slazzer&c=apps)

-->

AI upscale your photos, instantly. [Try Now](https://www.slazzer.com/features/ai-upscale/upload "")

AI enhance your photos, instantly. [Try Now](https://www.slazzer.com/features/ai-enhance/upload "")

AI relight your photos, instantly. [Try Now](https://www.slazzer.com/features/ai-relighting/upload "")

AI generate shadows, instantly. [Try Now](https://www.slazzer.com/features/ai-shadow/upload "")

AI replace your sky, instantly. [Try Now](https://www.slazzer.com/features/sky-replacement/upload "")

AI deoldify your photos, instantly. [Try Now](https://www.slazzer.com/features/ai-de-oldify/upload "")

Download Mobile App Now. [Android](https://play.google.com/store/search?q=slazzer&c=apps&pli=1 "") \| [ios](https://apps.apple.com/in/app/slazzer-background-remover/id6499511787 "")

# Background Removal API

- remove background
- crop
- background color

##### Remove image background with just a single API call

Our AI will remove the background from any image that has a clear foreground and background. (tested with human, cars, animals, & products )

## API Reference

Head


- ###### Server URL:


https://api.slazzer.com/v2.0

- ###### Request Body:


multipart/form-data

- ###### Method:

POST
- ###### API:


/remove\_image\_background


#### Authorization

- ###### API-KEY :

string
- ###### Your API key :

xxxx xxxx xxxx xxxx
- [Get API Key](https://www.slazzer.com/login)

Parameters Request body

- ###### source\_image\_file




**Type :** string($binary)



**Required :** Yes (Only one of the source\_image\_ parameters can be used in a single request.)





##### Description :



The source\_image\_file parameter uploads an image for background processing. By default, the API removes the background and returns a transparent PNG. Based on additional parameters, it can replace the background with a solid color or crop the image. It must be sent as a multipart/form-data request, processing one image at a time. Transparent PNGs retain transparency unless a background color is set.





**Supported Format :** PNG, JPG, JPEG.



**Examples :** source\_image\_file = @/path/to/image.png



**Important :** Only one of the source\_image\_ parameters can be used in a single request. If multiple source\_image\_ parameters are included, the request will fail.


- ###### source\_image\_url




**Type :** string



**Required :** Yes (Only one of the source\_image\_ parameters can be used in a single request.)





##### Description :



The source\_image\_url parameter provides a URL to an image for background processing. The API removes the background by default, returning a transparent PNG, or replaces it with a solid color or crops it, based on additional parameters. The URL must point to a publicly accessible image in JPG, JPEG, or PNG format.





**Supported Format :** PNG, JPG, JPEG.



**Examples :** source\_image\_url = https://example.com/image.png



**Important :** Only one of the source\_image\_ parameters can be used in a single request. If multiple source\_image\_ parameters are included, the request will fail.


- ###### source\_image\_base64




**Type :** string



**Required :** Yes (Only one of the source\_image\_ parameters can be used in a single request.)





##### Description :



The source\_image\_base64 parameter accepts a base64-encoded image string for background processing. The API removes the background by default, returning a transparent PNG, or replaces it with a solid color or crops it, based on additional parameters. The image should be encoded in base64 format and can be in JPG, JPEG, or PNG format.





**Supported Format :** PNG, JPG, JPEG.



**Examples :** source\_image\_base64 = data:image/png;base64,iVBORwEUgAA...



**Important :** Only one of the source\_image\_ parameters can be used in a single request. If multiple source\_image\_ parameters are included, the request will fail.


- ###### bg\_image\_file




**Type :** string($binary)



**Required :** No





##### Description :



This bg\_image\_file will be used as the background for the processed image. The background image will automatically be resized to fit the output image’s aspect ratio.





**Supported Format :** PNG, JPG, JPEG.



**Examples :** bg\_image\_file = @/path/to/image.png



**Important :** Only one of the bg\_image\_ parameter can be used in a single request. If multiple bg\_image\_ parameters are included, the request will fail.


- ###### bg\_image\_url




**Type :** string



**Required :** No





##### Description :



This bg\_image\_url will be used as the background for the output binary image. The background image will automatically be resized to fit the output image’s aspect ratio.





**Supported Format :** PNG, JPG, JPEG.



**Examples :** bg\_image\_url = https://example.com/image.png



**Important :** Only one of the bg\_image\_ parameter can be used in a single request. If multiple bg\_image\_ parameters are included, the request will fail.


- ###### bg\_image\_base64




**Type :** string



**Required :** No





##### Description :



This bg\_image\_base64 will be used as the background for the output binary image. The background image will automatically be resized to fit the output image’s aspect ratio





**Supported Format :** PNG, JPG, JPEG.



**Examples :** bg\_image\_base64 = data:image/png;base64,sYHdKmEUgAA...



**Important :** Only one of the bg\_image\_ parameter can be used in a single request. If multiple bg\_image\_ parameters are included, the request will fail.


- ###### bg\_color\_code




**Type :** string



**Required :** No





##### Description :



The bg\_color\_code parameter is used to specify a solid background color for the processed image. The color must be provided as a HEX color code.





**Supported Format :** HEX color code (e.g., #72E4B3 or #B3D472)



**Examples :** bg\_color\_code = #72E4B3



**Important :** The color code must include the # symbol before the color code.


- ###### format




**Type :** string



**Required :** No





##### Description :



The format parameter specifies the output image format. By default, the format is set to png. You can change it to other formats depending on your requirements.





##### Possible Values:



  - png (Default): PNG format, supports alpha transparency.
  - jpg : JPG format (no transparency).
  - zip : ZIP format, containing both the color image and the alpha matte image.

**Examples :** format = jpg

**Important :**

  - If no format is specified, the default value png will be used.
  - Use png for images requiring transparency, or jpg for standard images without transparency.

- ###### crop




**Type :** boolean



**Required :** No





##### Description :



The crop parameter determines whether extra transparent pixels surrounding the image will be cropped. When set to true, the image will be cropped to remove any transparent pixels around the content.





##### Possible Values:



  - false (Default): PNG format, supports alpha transparency.
  - true : Crops all extra transparent pixels.

**Examples :** crop = true

**Important :**

  - The default value is false, meaning the image will not be cropped unless explicitly specified.
  - Set to true if you want to automatically remove unnecessary transparent borders around the image.

- ###### crop\_margin




**Type :** int



**Required :** No





##### Description :



The crop\_margin parameter allows you to specify the amount of margin around the subject when cropping is applied (i.e., when crop=True). This parameter works only when the crop parameter is set to true.





##### Supported Formats :



  - 20px \- create margin all around the subject.
  - 12% \- create margin all around the subject with respect to the subject
     size.
  - 10px, 20px \- create 10px margin left and right side, 20px margin top and bottom
     side.
  - 10%, 20% \- create 10% margin left and right side, 20% margin top and bottom
     side with respect to the subject size.
  - 10px, 20px, 18px, 24px \- create 10px margin left, 20px margin top, 18px margin
     right and 24px margin in bottom.
  - 10%, 20%, 18%, 24% \- create 10% margin left, 20% margin top, 18% margin
     right and 24% margin in bottom with respect to the subject size.

##### Examples :

  - crop\_margin = "20px" \- Adds a 20px margin around the subject.
  - crop\_margin = "10%, 20%" \- Adds a 10% margin on the left and right sides, and a 20% margin on the top and bottom.
  - crop\_margin = "10px, 20px, 18px, 24px" \- Specifies different margin values for each side.

**Important :** The maximum allowed margin is either 500px or 50% of the subject's size, whichever is smaller.


- ###### scale




**Type :** string



**Required :** No





##### Description :



The scale parameter adjusts the size of the subject in the output image. The scaling factor can range between 10% and 100%, depending on the image dimensions.





##### Possible Values:



  - 10% to 100%  : Adjusts the size of the subject within the image.

##### Default Behavior :

  - If no position parameter is specified, the subject is centered by default.
  - If a position parameter is provided, the subject is scaled accordingly while respecting the specified position.

**Examples :** scale = 50%

**Important :**

  - A lower value (e.g., 10%) reduces the subject size, while a higher value (up to 100%) maintains or enlarges it within the image bounds.
  - Scaling behavior depends on the image's aspect ratio and composition.

- ###### position




**Type :** string



**Required :** No





##### Description :



The position parameter determines the placement of the subject within the image canvas. This parameter only works when the scale parameter is provided.





##### Possible Values:



  - A single value between 0% and 100% (applies to both horizontal and vertical positioning).
  - Two values between 0% and 100%, separated by a comma (e.g., 10%,18%), where:
    - The first value represents the horizontal position.
    - The second value represents the vertical position.

##### Default Behavior :

  - If no value is specified, the subject is placed in the center of the canvas.

**Examples :** position = 25%,50%

**Important :**

  - This parameter requires the scale parameter to be set.
  - Lower values position the subject closer to the top-left, while higher values move it toward the bottom-right.

- ###### preview




**Type :** boolean



**Required :** No





##### Description :



The preview parameter determines whether the image is resized to a lower resolution for preview purposes.





##### Possible Values:



  - false (default) : The image remains at its original resolution.
  - true : The image is resized to 0.25 megapixels (e.g., 400x600 pixels).

##### Default Behavior :

  - If not specified, the default value is false, meaning the image will retain its original resolution.

**Examples :** preview = true

**Important :**

  - When preview = true, the image is resized to 0.25 megapixels.
  - 0.20 credit will be charged per preview image.
  - 1 credit will be charged if the value is set to false.

- ###### channel




**Type :** string



**Required :** No





##### Description :



The channel parameter specifies which image channel to return. It can be used to extract specific color channels (red, green, blue) or the alpha mask.





##### Possible Values:



  - rgba (default) : Returns the image in full RGBA format.
  - alpha : Returns only the alpha mask of the image.

##### Default Behavior :

  - If not specified, the default value is rgba, returning the image with all color channels and transparency.

**Examples :** channel = alpha

**Important :**

  - Use rgba to retain all color information, including transparency.
  - Set to alpha if you only need the alpha mask of the image.

- ###### roi




**Type :** string



**Required :** No





##### Description :



The roi parameter allows you to extract a specific region of interest from an image. Only the contents within the selected rectangular area will be considered as the foreground, while everything else will be removed as background.





##### Supported Formats:



  - 200px, 320px, 400px, 230px – Specifies the top-left and bottom-right coordinates in pixels.
  - 10%, 15%, 25%, 30% – Specifies the top-left and bottom-right coordinates as percentages relative to the image size.

##### Default Behavior :

  - If not specified, the entire image is considered as the foreground.

**Examples :** roi = 100px, 200px, 400px, 500px

**Important :**

  - The first two values represent the top-left coordinates.
  - The last two values represent the bottom-right coordinates.
  - Can be defined in pixels or as a percentage of the image dimensions.

- ###### car\_shadow




**Type :** boolean



**Required :** No





##### Description :



The car\_shadow parameter determines whether an artificial shadow should be included in the output image. This feature is currently limited to car photos.





##### Possible Values:



  - false (default) – No artificial shadow will be applied.
  - true – Adds an artificial shadow to the car.

##### Default Behavior :

  - If not specified, the default value is false, meaning no shadow will be added.

**Examples :** car\_shadow = true

**Important :**

  - Shadows are only applied to car images.
  - For other subjects, no shadow will be applied, even if set to true.
  - This behavior may change in future updates.

Response


- 200

- 400

- 401

- 402

- 429


Success

**Background successfully removed!**

Your image has been processed, and the background is now removed. You can now download or use it as you wish.


Binary image data


Error

**Background removed failed!**

The request could not be processed due to invalid parameters or an unsupported image format. Ensure the input image meets the required format and size specifications, then try again. (No credits were deducted for this request.)

##### Example :

{

     "error": "Source image file not found"

}


Error

**Background removed failed!**

API-KEY missing or invalid API-KEY (No credit deducted)

##### Example :

{

     "error": "invalid api key"

}


Error

**Background removed failed!**

No credits remaining (No credit deducted)

##### Example :

{

     "error": "No credits remaining"

}


Error

**Background removed failed!**

Api rate limit crossed (No credit deducted)

##### Example :

{

     "error": "Api rate limit crossed"

}


## Output Formats

###### Easily request any one of the 2 formats via our format parameter.

| Format | Resolution |
| --- | --- |
| png | - Upto 10 MP , Ex - 3872 x 2592 |
| jpg | - Upto 25 MP , Ex - 6250 x 4000 |

\*Please note that PNG images above 10 megapixels are not supported by default. If you do not require transparency we recommend using the JPG format.

## API Rate Limit

###### You can instantly process upto 500 images per minute via the API, but depending on the input image megapixel resolution.

| Input image | Megapixels | Rate Limit approx |
| --- | --- | --- |
| 625 x 400 | 1 MP | 500 images per minute |
| 1200 x 800 | 1 MP | 500 images per minute |
| 1600 x 1200 | 2 MP | 250 images per minute |
| 2500 x 1600 | 4 MP | 125 images per minute |
| 4000 x 2500 | 10 MP | 50 images per minute |
| 6250 x 4000 | 25 MP | 20 images per minute |

Error code 429 will return if api rate limit exceed & no credit will be charged.

Higher api rate limits are available for enterprise customers. [Contact Us](https://www.slazzer.com/contact-us)

less

[cancel](https://www.slazzer.com/api#) choose

Are you still here [ok](https://www.slazzer.com/upload)
