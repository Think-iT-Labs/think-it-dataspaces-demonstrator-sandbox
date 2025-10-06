# Lab - Data Space Demonstrator

## Phase 1: Secure and sovereign integration of internal data systems to the data space

> Learning Objective: Understand how to register and publish data offers in a data space

### Your Mission Brief

"Before you can participate in the data space ecosystem, you need to contribute value to the network. Your organization has valuable pothole data that other partners need for their route planning and road maintenance. Register your data assets to make them discoverable and establish your organization as a trusted data provider in the network."

### Quest Tasks

1. Log into your assigned EDC connector using provided credentials.

Using the Postman Collection, configure the variables:
- Set `base_url` to your assigned connector URL (e.g., `your-company.dataspace-sandbox.think-it.io`)
- Set `api_key` with your provided API key

2. Review your organization's available datasets (provided as mock data)

Using the Think-it Simple AWS S3 Browser, download and view the data available to your company.

3. Register data assets with metadata for discoverability.

Use the **Create Asset V3** request. Modify the request body:
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

4. Configure a basic access policy for your data offers.

Use the **Create Policy Definition V3** request:
- In the Pre-request Script tab, set the `policyId` variable (e.g., `policy-1`)
- The default request body already includes the correct permission structure with "use" action and empty constraints. It allows everyone to use the offer.
- Send the request and save the policy ID for the next step

5. Create a contract definition (data offer) using your asset ID and the policy ID that you created.

Use the **Create Contract Definition V3** request:
- In the Pre-request Script tab, configure:
  - `definitionId`: Your contract definition ID (e.g., `contract-definition-1`)
  - `accessPolicyId`: The policy ID from step 4
  - `contractPolicyId`: The policy ID from step 4

6. Validate successful registration by checking your own catalog publication

Use the **Request Catalog V3** request:
- In the Pre-request Script tab, set `counterPartyAddress` to your own DSP endpoint: `https://your-company.dataspace-sandbox.think-it.io/api/dsp`
- Send the request and verify your asset appears in the catalog response

## Phase 2: Discovery & Assessment

> Learning Objective: Understand data space catalog discovery and asset identification

### Your Mission Brief

"Your team has identified 4 key supplier categories (2 car manufacturers, the municipality of Madrid, EMT Madrid and the road maintenance company) that have relevant data. Time to discover what data is actually available in the data space network."

### Quest Tasks

1. Log into your assigned EDC connector using provided credentials

2. Discover available data catalogs from partner organizations and identify relevant datasets across the network.

Use the **Request Catalog V3** request:
- In the Pre-request Script tab, set `counterPartyAddress` to the target connector's DSP endpoint (e.g., `https://partner-company.dataspace-sandbox.think-it.io/api/dsp`)
- Send the request to fetch the catalog
- Review the response to identify available datasets, their metadata, and associated policies
- Note the `@id` field of datasets you're interested in (you'll need this for negotiation)
- Examine the policy constraints to understand usage requirements

## Phase 3: Contract Negotiation & Agreement

> Learning Objective: Master data usage agreements and sovereignty controls

### Your Mission Brief

"Legal compliance requires that all supplier data used in your report must have clear usage agreements, audit trails, and purpose limitations. Your legal team has provided specific policy requirements that must be embedded in all data sharing contracts."

### Quest Tasks

1. Initiate contract negotiations with at least 1 data provider and configure usage policies according to the provider's catalog.

Use the **Initiate Contract Negotiation V3** request:
- In the Pre-request Script tab, configure the following variables:
  - `counterPartyAddress`: Provider's DSP endpoint (e.g., `https://provider.dataspace-sandbox.think-it.io/api/dsp`)
  - `counterPartyId`: Provider's participant ID (found in catalog response)
  - `offerId`: The offer ID from the catalog (format: `assetId:policyId:definitionId`)
  - `assetId`: The asset ID you want to access
- In the request body, update the `policy` section by copying the **exact policy** from the provider's catalog response that you received in the previous step.

![Catalog Response](./resources/catalog-request.png)

![Negotiation with Policy](./resources/contract-negotiation.png)

- Ensure the policy's `@id`, `assigner`, and `target` fields match the catalog offer
- Send the request and save the returned `negotiationId` from the response

2. Check the status of the contract negotiations until you reach agreements

Use the **Get Negotiation State V3** request:
- In the Pre-request Script tab, set `negotiationId` to the ID from step 1
- Send the request repeatedly (every few seconds) to monitor the negotiation progress
- Wait until the state becomes `FINALIZED` (states: REQUESTING → REQUESTED → OFFERED → ACCEPTED → AGREED → VERIFIED → FINALIZED)

![Finalized Negotiation](./resources/negotiation-finalized.png)

- Once finalized, retrieve the agreement ID (needed for data transfer)

## Phase 4: Data Transfer & Integration (25 minutes)

> Learning Objective: Execute secure, sovereign data transfers

### Your Mission Brief

"Contracts are signed, policies are in place. Now execute the actual data transfer(s). Your CFO wants to see real numbers, not just promises."

### Quest Tasks

1. Execute data transfer(s) from approved contract(s)

Use the **Create Transfer Process V3** request:
- In the Pre-request Script tab, configure:
  - `counterPartyAddress`: Provider's DSP endpoint (same as used in negotiation)
  - `contractId`: The agreement ID obtained from the finalized negotiation (use **Get Agreement For Negotiation V3** if needed)
  - `transferType`: Set to `AmazonS3-PUSH` 
- In the request body, add the following data destination to receive data on your S3 Bucket:
```
"dataDestination": {
    "type": "AmazonS3",
    "objectName": "your-destination-data-filename",
    "region": "<REPLACE WITH THE BUCKET REGION>",
    "bucketName": "<REPLACE WITH THE SOURCE BUCKET NAME>",
    "accessKeyId": "<REPLACE WITH YOUR ACCESS KEY ID>",
    "secretAccessKey": "<REPLACE WITH SECRET ACCESS KEY>"
}
```
- Send the Transfer Process request.
- Send the request repeatedly (every few seconds) to monitor the transfer state using **State Transfer Process V3** request.
- Wait until the transfer state becomes `COMPLETED` (states: INITIAL → PROVISIONING → PROVISIONED → REQUESTING → REQUESTED → STARTING → STARTED → COMPLETING → COMPLETED)
![](./resources/transfer-completed.png)

- Once completed, visit the Think-it AWS Simple S3 Browser application
![](./resources/s3-assets-transfered.png)

2. Inspect the received data and share insights about your learnings.

- Review the data structure and content
- Discuss with your team:
  - What data did you receive and how does it align with the catalog description?
  - What challenges did you encounter during the data space workflow?
  - How could this data be integrated with your organization's systems?
