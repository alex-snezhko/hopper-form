# Hopper Form
An HTML form body parsing extension for [Hopper](https://github.com/alex-snezhko/hopper), an HTTP microframework for the Grain programming language. Supports both `x-www-form-urlencoded` and `multipart/form-data` encodings.

## Installation
This library is contained within a single Grain file, which should be installed into the same directory as your `hopper.gr`
```
curl https://raw.githubusercontent.com/alex-snezhko/hopper-form/main/hopper-form.gr -o hopper-form.gr
```

## Example Usage
```
import Hopper from "./hopper"
import Form from "./hopper-form"

Hopper.serve([
  Hopper.post("/urlencoded", req => {
    let form = Form.urlEncodedFormBody(req)
    // ...
  }),
  Hopper.post("/multipart", req => {
    let form = Form.multipartFormBody(req)
    // ...
  })
])
```

`urlEncodedFormBody` and `multipartFormBody` both return `Result`s containing either the successfully-parsed form data or an `Err` variant if something went wrong while parsing. To accommodate multiple values being given under the same name, the output is given in a `Map` of `Hopper.OneOrMany` values. The incoming request is expected to have an `application/x-www-form-urlencoded` `Content-Type` if using `urlEncodedFormBody` and a `multipart/form-data` `Content-Type` if using `multipartFormBody`, otherwise an `Err` variant will be returned.

## API Docs
`grain doc`-generated API docs are available [here](/api-docs.md)
