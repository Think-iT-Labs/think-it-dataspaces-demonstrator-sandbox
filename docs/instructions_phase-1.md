# Phase 1: Secure and sovereign integration of internal data systems to the data space

> Learning Objective: Understand how to register and publish data offers in a data space

## Mission Brief

Before you can participate in the data space ecosystem, you need to contribute value to the network. Your organization has valuable pothole data that other partners need for their route planning and road maintenance. Register your data assets to make them discoverable and establish your organization as a trusted data provider in the network.

## Quest Tasks

### Review your organization's available datasets (provided as mock data)

Using the Think-it Simple AWS S3 Browser, download and view the data available to your company.

### Register data assets with metadata for discoverability

With Postman, use the `Create Asset V3` request:

- Update `@id` with your unique asset identifier
- Update `properties` section with descriptive metadata (title, description, organization)
- Configure the `dataAddress` section with your S3 bucket information:

```json
"dataAddress": {
    "type": "AmazonS3",
    "objectName": "your-data-file.json",
    "region": "<REPLACE WITH THE BUCKET REGION>",
    "bucketName": "<REPLACE WITH THE SOURCE BUCKET NAME>",
    "accessKeyId": "<REPLACE WITH YOUR ACCESS KEY ID>",
    "secretAccessKey": "<REPLACE WITH SECRET ACCESS KEY>"
}
```

### Configure a basic access policy for your data offer

With Postman, use the `Create Policy Definition V3` request:

- In the Pre-request Script tab, set the `policyId` variable (e.g., `policy-1`)
- The default request body already includes the permission structure with "use" action and empty constraints. It allows the usage without restrictions.
- Send the request and save the policy ID for the next step

### Create a contract definition (data offer) using the policy ID that you created

With Postman, use the `Create Contract Definition V3` request:

- In the Pre-request Script tab, configure:
  - `definitionId`: Your contract definition ID (e.g., `contract-definition-1`)
  - `accessPolicyId`: The policy ID from step 4
  - `contractPolicyId`: The policy ID from step 4

This creates a contract that allows access to my datasets with no restrictions.

### Validate successful registration by checking your own catalog publication

Use the `Request Catalog V3` request:

- In the Pre-request Script tab, set `counterPartyAddress` to your own DSP endpoint: `https://your-company.dataspace-sandbox.think-it.io/api/dsp`
- Send the request and verify your asset appears in the catalog response
