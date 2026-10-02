---
url: https://developers.beehiiv.com/api-reference/posts/create
retrieved: 2026-10-02
command: firecrawl scrape https://developers.beehiiv.com/api-reference/posts/create --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Create post | beehiiv | Developer Documentation
---
For AI agents: a documentation index is available at the root level at /llms.txt. Append /llms.txt to any URL for a page-level index, or .md for the markdown version of any page.

[Skip to navigation](https://developers.beehiiv.com/api-reference/posts/create#fern-sidebar)

Available on the Pro and Enterprise plans

This endpoint is available to publications on the Pro and Enterprise plans.

Create a post for a specific publication. For a detailed walkthrough including setup, testing workflows, and working with custom HTML and templates, see the [Using the Send API and Create Post Endpoint](https://www.beehiiv.com/support/article/36759164012439-using-the-send-api-and-create-post-endpoint) guide.

## Asynchronous creation

Post creation is processed in the background. This endpoint returns `201` immediately with the post’s `id`, but the post is not finished being created at that moment. The returned `id` is stable — it is the same id the post will have once creation completes.

If you fetch the post (`GET /publications/{publicationId}/posts/{postId}`) right away, it may not exist yet. In that case the fetch returns `202` (still being created) — wait briefly and retry, honoring the `Retry-After` header. If background creation fails, the fetch returns `404` with the error code `POST_CREATION_FAILED`, so you should stop retrying, verify your request, and try creating the post again.

## Content methods

There are three ways to provide content for a post. You must provide either `blocks` or `body_content`, but not both.

### 1\. Blocks

Use the `blocks` field to build your post with structured content blocks such as paragraphs, images, headings, buttons, tables, and more. Each block has a `type` and its own set of properties. This method gives you fine-grained control over individual content elements and supports features like visual settings, visibility settings, and dynamic content targeting.

### 2\. Raw HTML (`body_content`)

Use the `body_content` field to provide a single string of raw HTML. The HTML is wrapped in an `htmlSnippet` block internally. This is useful when you have pre-built HTML content or are migrating from another platform.

### 3\. HTML blocks within blocks

Use `type: html` blocks inside the `blocks` array to embed raw HTML snippets alongside other structured blocks. This lets you mix structured content (paragraphs, images, etc.) with custom HTML where needed.

## CSS and styling guardrails

beehiiv processes all HTML content through a sanitization pipeline. When using `body_content` or `html` blocks, be aware of the following:

- **`<style>` tags are removed.** All `<style>` block elements are stripped during sanitization. Do not rely on embedded stylesheets.
- **`<link>` tags are removed.** External stylesheet references are not allowed.
- **Inline styles are preserved.** Styles applied directly to elements via the `style` attribute (e.g., `<div style="color: red;">`) are kept intact.
- **CSS classes have no effect.** While class attributes are not stripped, no corresponding stylesheets are loaded to apply them.
- **beehiiv’s email template wraps your content.** Your HTML is rendered inside beehiiv’s email table structure, which applies its own layout and spacing. This may affect the appearance of your content.
- **Use inline styles for all visual styling.** Since `<style>` and `<link>` tags are removed, inline styles on individual elements are the only reliable way to control appearance.

### Authentication

AuthorizationBearer

### Path parameters

publicationIdstringRequired`format: "^(pub_[0-9a-fA-F\-]+)$"`

The prefixed ID of the publication object

### Request

This endpoint expects an object.

titlestringRequired

The title of the post.

blockslist of objectsOptional

Show 18 variants

body\_contentstringOptional

subtitlestringOptional

The subtitle of the post.

post\_template\_idstringOptional`format: "^(post_template_[0-9a-fA-F\-]+)$"`

The ID of the template to use for the post. If not provided, the default template will be used.

statusenumOptionalDefaults to `draft`

Allowed values:draftconfirmed

scheduled\_atdatetimeOptional

custom\_link\_tracking\_enabledbooleanOptional

If true, custom link tracking will be enabled for this post. If not provided, the default value will be used.

email\_capture\_type\_overrideenumOptional

The email capture type to use for this post. If not provided, the default value will be used.

Allowed values:nonegatedpopup

override\_scheduled\_atdatetimeOptional

social\_shareenumOptional

The social share type to use for this post. If not provided, the default value will be used.

Allowed values:comments\_and\_likes\_onlywith\_comments\_and\_likestopnone

thumbnail\_image\_urlstringOptional

The URL of the thumbnail image to use for the post. If not provided, the default value will be used.

recipientsobjectOptional

The recipients to use for this post. If not provided, the default value will be used.

Show 2 properties

email\_settingsobjectOptional

The email settings to use for this post. If not provided, the default value will be used.

Show 11 properties

web\_settingsobjectOptional

The web settings to use for this post. If not provided, the default value will be used.

Show 7 properties

seo\_settingsobjectOptional

The metadata to use for this post. If not provided, the default value will be used.

Show 6 properties

content\_tagslist of stringsOptional

The content tags to use for this post. If not provided, the default value will be used.

guest\_author\_idslist of stringsOptional

The prefixed IDs of the guest authors to associate with this post. Guest authors must belong to the publication. Obtain IDs from the List Authors endpoint. When provided, replaces all existing guest authors on the post.

team\_author\_idslist of stringsOptional

The prefixed IDs of the team members to associate with this post as authors. Team authors must have access to the publication. Note the List Authors endpoint only returns team members who already have a byline on a published post in this publication, so it will not surface IDs for a team member's first assignment. When provided, replaces all existing team authors on the post.

headersmap from strings to optional stringsOptional

utm\_sourcestringOptional

utm\_mediumstringOptional

utm\_campaignstringOptional

utm\_params\_enabledbooleanOptional

Whether UTM parameters are appended to links in this post. Omit to inherit from the newsletter list, then the publication.

custom\_fieldsmap from strings to stringsOptional

The custom fields to use for this post. If not provided, the default value will be used.

newsletter\_list\_idstringOptional

The prefixed ID of the newsletter list to associate with this post. When provided, the post will only be sent to subscribers of this list.

### Response

Created

dataobject

Show 2 properties

### Errors

400

Bad Request Error

401

Unauthorized Error

403

Forbidden Error

404

Not Found Error

429

Too Many Requests Error

500

Internal Server Error
