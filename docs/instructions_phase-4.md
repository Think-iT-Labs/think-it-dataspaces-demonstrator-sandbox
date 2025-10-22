# Phase 4: Data Transfer & Integration

> Learning Objective: Execute secure, sovereign data transfers

## Mission Brief

Contracts are signed, policies are in place. Now execute the actual data transfer(s). Your CFO wants to see real numbers, not just promises.

## Quest Tasks

### Initiate the data transfer process

With Postman, use the `Create Transfer Process V3` request:

- In the Pre-request Script tab, configure:
  - `counterPartyAddress`: Provider's DSP endpoint (same as used in negotiation)
  - `contractId`: The agreement ID obtained from the finalized negotiation (use `Get Agreement For Negotiation V3` if needed)
  - `transferType`: Set to `AmazonS3-PUSH`
- In the request body, add the following data destination to receive data on your S3 Bucket:

```json
"dataDestination": {
    "type": "AmazonS3",
    "objectName": "your-destination-data-filename",
    "region": "<REPLACE WITH THE BUCKET REGION>",
    "bucketName": "<REPLACE WITH THE SOURCE BUCKET NAME>",
    "accessKeyId": "<REPLACE WITH YOUR ACCESS KEY ID>",
    "secretAccessKey": "<REPLACE WITH SECRET ACCESS KEY>"
}
```

- Send the request and save the returned `transferProcessId`

### Monitor the transfer process until completion

With Postman, use the `State Transfer Process V3` request:

- In the Pre-request Script tab, set the `transferProcessId` from the previous step
- Send the request repeatedly (every few seconds) to monitor the transfer state. Wait until the transfer state becomes `COMPLETED`

![Transfer Completed](../resources/transfer-completed.png)

### Verify the transferred data in your S3 bucket

Once the transfer is completed:

- Visit the Think-it AWS Simple S3 Browser application of your organization's bucket
- Verify that the data file appears in the expected location

![S3 Assets Transferred](../resources/s3-assets-transfered.png)

### Inspect the received data and share insights

Download and review the transferred data:

- Review the data structure and content
- Discuss with your team:
  - What data did you receive and how does it align with the catalog description?
  - What challenges did you encounter during the data space workflow?
  - How could this data be integrated with your organization's systems?
