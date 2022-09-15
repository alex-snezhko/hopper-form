---
title: HopperForm
---

An HTML form body parsing extension for Hopper.

Version 0.1.0

## Types

Type declarations included in the hopper-form module

### HopperForm.**FilePartData**

```grain
record FilePartData {
  filename: String,
  contentType: String,
  content: String,
}
```

Represents data for a file for `multipart/form-data` requests.

### HopperForm.**Part**

```grain
enum Part {
  FilePart(FilePartData),
  TextPart(String),
}
```

Represents data for `multipart/form-data` requests.

### HopperForm.**FormError**

```grain
enum FormError {
  ContentTypeNotAllowed,
  InvalidFormData(String),
}
```

Represents possible errors encountered while parsing form bodies.

## Values

Functions for parsing HTML form body data.

### HopperForm.**urlEncodedFormBody**

```grain
urlEncodedFormBody :
  Hopper.Message<a> ->
   Result<Map.Map<String, Hopper.OneOrMany<String>>, FormError>
```

Parses an HTTP request body with URL-encoded form data into a `Map` mapping
form item names to their values. The keys/values are expected to be
URL-encoded and the request is expected to have a
`Content-Type: application/x-www-form-urlencoded` header

Parameters:

|param|type|description|
|-----|----|-----------|
|`req`|`Hopper.Message<a>`|The incoming `Request`|

Returns:

|type|description|
|----|-----------|
|`Result<Map.Map<String, Hopper.OneOrMany<String>>, FormError>`|A `Result` with a `Map` mapping form item names to their values or an error reason|

### HopperForm.**multipartFormBody**

```grain
multipartFormBody :
  Hopper.Message<a> ->
   Result<Map.Map<String, Hopper.OneOrMany<Part>>, FormError>
```

Parses an HTTP request body with multipart form data into a `Map` mapping
form item names to their values. The request should have
a `Content-Type: multipart/form-data` header

Parameters:

|param|type|description|
|-----|----|-----------|
|`req`|`Hopper.Message<a>`|The incoming `Request`|

Returns:

|type|description|
|----|-----------|
|`Result<Map.Map<String, Hopper.OneOrMany<Part>>, FormError>`|A `Result` with a `Map` mapping form item names to their values or an error reason|

