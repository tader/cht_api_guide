---
title: How to Use the CloudHealth API
category: documentation
position: 2
parameters:
  - name:
    content:
content_markdown: |-
  The goal of the CloudHealth API is to let you write your own applications that leverage and extend CloudHealth functionality.

  The CloudHealth API provides programmatic access to functionalities in the CloudHealth platform using REST-based arguments and JSON-formatted responses.

  You send REST API requests to various endpoints to retrieve and update data from the CloudHealth Platform. Different API functionality can be found at different endpoints. Here are some example endpoints.
  * `https://chapi.cloudhealthtech.com/olap_reports/cost/history`
  * `https://chapi.cloudhealthtech.com/v1/perspective_schemas`

  Using the API, you can query the following areas of the CloudHealth Platform.
  * Reporting
  * Asset
  * Account
  * Metrics
  * Tagging
  * Perspectives
  * Partner
  * Partner Customer Provisioning
  * Partner AWS Account Assignment
  * Customer Statement

  #### Anatomy of a Request
  Here's a REST-based query that uses the CloudHealth Query Language.

  ```
  curl 'https://chapi.cloudhealthtech.com/olap_reports/cost/history?api_key=XXXXX98900000YYYY&interval=monthly' -H 'Accept: application/json'
  ```

  Let's break down this request.
  * `cURL` is a command-line REST client (https://curl.haxx.se).
  * `https://chapi.cloudhealthtech.com/olap_reports/cost/history` is the REST endpoint. In this example, the endpoint returns data for the **Standard Cost History Report**.
  * `api_key=XXXXX98900000YYYY` attaches your unique API key with the request. See [How CloudHealth Validates API Requests](#how-cloudhealth-validates-api-requests).
  * `interval=monthly` is a query parameter that you append to the REST endpoint. Query parameters allow you to constrain the data returned from a request. You can attach multiple query parameter as long as each parameter is separated from the next by the `&` symbol.

  * A URI string is made up of the REST endpoint and all the query parameters attached to it. In this example, this is the URI string.
    ```
    https://chapi.cloudhealthtech.com/olap_reports/cost/history?api_key=XXXXX98900000YYYY&interval=monthly
    ```
    The maximum permissible length of a URI string is **4000** characters.
    {:.warning}

  * `-H accept: application/json` is the communication header. You can also specify this header as `-H Content-Type:application/json`. All REST API calls must include proper communication headers. The other header you can pass with the CloudHealth API is `Accept-Encoding:gzip`, which compresses the communication with GZIP compression.

  #### Types of Requests
  * GET requests retrieve data from the CloudHealth Platform.
    ```
    curl 'https://chapi.cloudhealthtech.com/olap_reports/cost/history?api_key=XXXXX98900000YYYY&interval=monthly' -H 'Accept: application/json'
    ```
  * POST requests send data to the CloudHealth Platform. They include a JSON-formatted message body, which contains the data that should be sent. Here, the message body is specified as a parameter following the `-d` flag.
    ```
    curl 'https://chapi.cloudhealthtech.com/v1/perspective_schemas?api_key=XXXXX98900000YYYY'
      -H 'content-type: application/json'
      -d '{
        "schema":{
          "name":"Environment-API",
          "rules":[{"type":"categorize","asset":"AwsAsset","tag_field":["cht_env"],"ref_id":"206159110488","name":"Env"}],
          "merges":[],
          "constants":[…]}
        }'
    ```
left_code_blocks:
  - code_block:
    title:
    language:
right_code_blocks:
  - code_block:
      This area displays code examples that you can copy and paste into a terminal. Before running these examples, make sure you replace placeholder values enclosed within angle brackets <> with actual values.

      For example, all API queries must include your unique API Key. The value of this key is indicated as <your_API_key> in these code examples. Replace this placeholder value with your actual API Key.
    title: Code Example Pane
    language: none
---
