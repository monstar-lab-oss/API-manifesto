<!--
Table of contents created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc)

use the following command: `gh-md-toc README.md | grep -v g-emoji` to filter out lines with emoji
-->

<!--
New section template:

## Section

### TODO
<details>
<summary>Click to see examples</summary>

#### ✅

#### ⛔️

</details>
-->

# API Manifesto
Documents how to write APIs

## Introduction

TODO

Table of Contents
=================

   * [API Manifesto](#api-manifesto)
      * [Introduction](#introduction)
   * [Table of Contents](#table-of-contents)
   * [Requests](#requests)
      * [URLs](#urls)
         * [TODO](#todo)
      * [Request Headers](#request-headers)
         * [Protected endpoints](#protected-endpoints)
         * [Supporting localization](#supporting-localization)
         * [Making debugging easier](#making-debugging-easier)
   * [Responses](#responses)
      * [Response Body](#response-body)
         * [Object at the root level](#object-at-the-root-level)
         * [Return an empty collection when there are no results](#return-an-empty-collection-when-there-are-no-results)
      * [Use null or unset keys that are not set](#use-null-or-unset-keys-that-are-not-set)
      * [Status Codes](#status-codes)
         * [TODO](#todo-1)
   * [Auth](#auth)
      * [TODO](#todo-2)
   * [Error Handling](#error-handling)
      * [TODO](#todo-3)
   * [Localization](#localization)
      * [TODO](#todo-4)
   * [Timeouts](#timeouts)
      * [TODO](#todo-5)
   * [Pagination](#pagination)
      * [TODO](#todo-6)
   * [Inspiration](#inspiration)
   
# Requests

## URLs

### TODO

<details>
<summary>Click to see examples</summary>

#### ✅

#### ⛔️

</details>

## Request Headers

### Protected endpoints

Use the `Authorization` header to consume protected endpoints. See the [Auth](#auth) section for more information on how to handle authorization and authentication.

<details>
<summary>Click to see examples</summary>

#### ✅

Use `Authorization` to authorize:

```bash
Authorization = "Basic QWxhZGRpbjpPcGVuU2VzYW1l"
```

#### ⛔️

Avoid using custom headers for authorization:

```bash
UserToken = "QWxhZGRpbjpPcGVuU2VzYW1l"
```

</details>

### Supporting localization

In order to support localization now and in the future, the `Accept-Language` should be used to indicate the client's language towards the API. 

<details>
<summary>Click to see examples</summary>

#### ✅

Use [ISO 639-1](http://www.loc.gov/standards/iso639-2/php/code_list.php) codes to indicate the preferred language of the response.

```bash
Accept-Language = da
```

Use a prioritized list of languages to influence the fallback language:

```bash
Accept-Language = da, en
```

#### ⛔️

Avoid using other standards than ISO 639-1 for specifying the preferred language:

```bash
Accept-Language = danish
```

</details>

### Making debugging easier

Use headers to give the API information about the consumer to ease debugging. There's no industry standard, so feel free to make your own convention, just remember to use it consistently.

<details>
<summary>Click to see examples</summary>

#### ✅

```bash
Client-Meta-Information = iOS;staging;v1.2;iOS12;iPhone13
```

</details>

See [N-Meta](https://github.com/nodes-vapor/n-meta) for inspiration on how to do this.

# Responses

## Response Body

### Object at the root level

A body should always return an object at the root level. This enables including additional data about the response such as metadata separate from the object(s). We recommend using `data` for successful requests with meaningful response data and `error` for unsuccessful requests with error data being returned.

<details>
<summary>Click to see examples</summary>

#### ✅

Returning a collection should be encapsulated in a key:

```json
{
    "data": [
        {
            "username": "..."
        },
        {
            "username": "..."
        }
    ]
}
```

Returning an object (e.g. a user) should also use the `data` key:

```json
{
    "data": {
        "username": "..."
    }
}
```

Returning an error should use the `error` key:

```json
{
    "error": {
        "description": "..."
    }
}
```

Please see the [error section](#errors) for more information.

#### ⛔️

Avoid returning collections at the top level in the response:

```json
[
    {
        "email": "..."
    },
    {
        "email": "..."
    }
]
```

Avoid returning data that are not encapsulated in a root key (`data` or `error`):

```json
{
    "error": true,
    "description": "..."
}
```

</details>

### Return an empty collection when there are no results

To make it easier for the API consumer, return HTTP status code `200` with an empty collection instead of e.g. `204` with no body.

<details>
<summary>Click to see examples</summary>

#### ✅

Combine HTTP status code `200` with empty collections:

```json
{
    "data": []
}
```

#### ⛔️

Avoid using HTTP status code `204` for empty collections.

</details>

## Use `null` or unset keys that are not set

To make the API explicit and to make it easier for the consumer, always return keys without values as `null` or unset them.

<details>
<summary>Click to see examples</summary>

#### ✅

Return a value as `null`:

```json
{
    "data": {
        "email": null,
        "name": "..."
    }
}
```

Unset a key without a value:

```json
{
    "data": {
        "name": "..."
    }
}
```

#### ⛔️

Avoid including a key without a meaningful value:

```json
{
    "data": {
        "name": ""
    }
}
```
</details>

## Status Codes

### TODO

<details>
<summary>Click to see examples</summary>

#### ✅

#### ⛔️

</details>

# Auth

### TODO

<details>
<summary>Click to see examples</summary>

#### ✅

#### ⛔️

</details>

# Error Handling

### TODO

<details>
<summary>Click to see examples</summary>

#### ✅

#### ⛔️

</details>

# Localization

### TODO

<details>
<summary>Click to see examples</summary>

#### ✅

#### ⛔️

</details>

# Timeouts

### TODO

<details>
<summary>Click to see examples</summary>

#### ✅

#### ⛔️

</details>

# Pagination

### TODO

<details>
<summary>Click to see examples</summary>

#### ✅

#### ⛔️

</details>

# Inspiration

These guidelines have been made with inspiration from the following API guidelines:

- [Microsoft API Guidelines](https://github.com/microsoft/api-guidelines/blob/vNext/Guidelines.md)
- [Zalando API Guidelines](https://opensource.zalando.com/restful-api-guidelines/)
- [PayPal API Guidelines](https://github.com/paypal/api-standards/blob/master/api-style-guide.md)
- [Atlassian API Guidelines](https://developer.atlassian.com/server/framework/atlassian-sdk/atlassian-rest-api-design-guidelines-version-1/)