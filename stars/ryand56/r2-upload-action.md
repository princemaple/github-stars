---
project: r2-upload-action
stars: 81
description: GitHub Action to upload files or directories to a Cloudflare R2 bucket (or another S3 compatible API), built on top of @aws-sdk/client-s3 in TypeScript.
url: https://github.com/ryand56/r2-upload-action
---

R2 Upload Action
================

GitHub Action to upload files to a Cloudflare R2 bucket, built on top of @aws-sdk/client-s3 in TypeScript.  
Combination of these two repos: S3 Upload Action and Cloudflare R2 Upload.

Important

Node.js 20 is now required to run this action.

Usage
-----

### Basic Usage

\- uses: ryand56/r2-upload-action@latest
  with:
    r2-account-id: ${{ secrets.R2\_ACCOUNT\_ID }}
    r2-access-key-id: ${{ secrets.R2\_ACCESS\_KEY\_ID }}
    r2-secret-access-key: ${{ secrets.R2\_SECRET\_ACCESS\_KEY }}
    r2-bucket: ${{ secrets.R2\_BUCKET }}
    source-dir: src
    destination-dir: ./

In this example, `source-dir` is stored in the root of the bucket. Change `destination-dir` input to specify the location of where the directory will be uploaded.

### Custom Usage

\- uses: ryand56/r2-upload-action@latest # Can be any release
  with:
    r2-account-id: ${{ secrets.R2\_ACCOUNT\_ID }}
    r2-access-key-id: ${{ secrets.R2\_ACCESS\_KEY\_ID }}
    r2-secret-access-key: ${{ secrets.R2\_SECRET\_ACCESS\_KEY }}
    r2-bucket: ${{ secrets.R2\_BUCKET }}
    source-dir: src
    destination-dir: artifacts # Can be anything as long as it is an actual path
    output-file-url: true # defaults to true
    multipart-size: 100 # If the file size is greater than the value provided here, then use multipart upload
    max-retries: 5 # The maximum number of retries it takes to upload a multipart chunk until it moves on to the next part
    multipart-concurrent: true # Whether to concurrently upload a multipart chunk
    keep-file-fresh: false # defaults to false

See the latest action.yml for every input and output or take a look below.

Inputs
------

Name

Description

Default

`r2-account-id`

**(Required)** Your Cloudflare account ID.

_N/A_

`r2-access-key-id`

**(Required)** Your Cloudflare R2 bucket access key ID.

_N/A_

`r2-secret-access-key`

**(Required)** Your Cloudflare R2 bucket secret access key.

_N/A_

`r2-bucket`

**(Required)** Your Cloudflare R2 bucket name.

_N/A_

`source-dir`

**(Required)** The directory to upload to the Cloudflare R2 bucket.

_N/A_

`destination-dir`

(Optional) The destination to upload the directory to in the Cloudflare R2 bucket.

Empty string

`output-file-url`

(Optional) Output the results of the action uploaded files to the `file-urls` output

true

`multipart-size`

(Optional) The minimum file size to use multipart file upload

100 (in MB)

`max-retries`

(Optional) The maximum number of retries before failing

5

`multipart-concurrent`

(Optional) Use multipart concurrent file uploading

true

`keep-file-fresh`

(Optional) Keep the destination up-to-date, **which will permanently delete the previous contents**

false

Outputs
-------

Name

Description

`result`

Result of this action. Either `success` or `failure` is set.

`file-urls`

The URLs of the uploaded files in the directory.

Contributing
------------

See the contributing guide for more detail on how to implement something into the project.
