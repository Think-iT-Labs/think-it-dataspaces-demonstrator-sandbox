# Think-it Dataspaces Demonstrator Sandbox

AWS Sandbox for Think-it Data Spaces Demonstrator

## Postman Configuration Guide

### Configuring Postman to Interact with the Connector

1. **Import the Collection**:
   - Navigate to the `collections/Postman/` directory.
   - Import the `Think-it EDC Connector - Basic.json` file into Postman.

2. **Set Up Environment Variables**:
   - Define the following variables in your Postman environment:
     - `base_url`: The base URL of your connector's HTTP API.

3. **Authentication**:
   - Ensure that the necessary authentication header `api_key` is configured in the Postman collection.

4. **Testing Data Exchange**:
   - Use the provided requests to interact with the connector.

## Lab Phases

### Phase 1: Secure and Sovereign Data Integration

- **Task 1.1**: Create an asset in the data space.
- **Task 1.2**: Define a policy for data usage.
- **Task 1.3**: Create a contract definition to enforce the policy.

### Phase 2: Discovery & Assessment

- **Task 2.1**: Query the catalog to discover available datasets.
- **Task 2.2**: Assess the quality and relevance of the discovered datasets based on available metadata.

### Phase 3: Contract Negotiation & Policy Configuration

- **Task 3.1**: Create a Policy.
- **Task 3.2**: Initiate a contract negotiation with another participant.
- **Task 3.3**: Monitor the negotiation process and finalize the agreement.

### Phase 4: Data Transfer & Integration

- **Task 4.1**: Initiate a data transfer process.
- **Task 4.2**: Verify the successful transfer of data.
- **Task 4.3**: Integrate the received data into your internal system.

### Phase 5: Reporting & Verification

- **Task 5.1**: Generate a report based on the exchanged data.

## Gamification Checklist

Participants can use the following checklist to track their progress.

Judges will use this to assign scores and incentivize the lab session.

### Lab Checklist

- [ ] **(5 points)** Successfully configure Postman to interact with the connector.
- [ ] **(10 points)** Complete Task 1.1: Create an asset in the data space.
- [ ] **(10 points)** Complete Task 1.2: Define a simple policy for data usage.
- [ ] **(10 points)** Complete Task 1.3: Create a contract definition to enforce the policy.
- [ ] **(10 points)** Complete Task 2.1: Query the catalog to discover available datasets.
- [ ] **(5 points)** Complete Task 2.2: Assess the quality and relevance of the discovered datasets based on available metadata.
- [ ] **(15 points)** Complete Task 3.1: Initiate a contract negotiation with another participant.
- [ ] **(5 points)** Complete Task 3.2: Monitor the negotiation process and finalize the agreement.
- [ ] **(10 points)** Complete Task 4.1: Initiate a data transfer process.
- [ ] **(5 points)** Complete Task 4.2: Verify the successful transfer of data.
- [ ] **(10 points)** Complete Task 4.3: Integrate the received data into your internal system.
- [ ] **(10 points)** Complete Task 5.1: Generate a report based on the exchanged data.
- [ ] **(5 points)** Submit final reports and verification results for review.

## Participants of the Data Space

| Lab Persona                                   | Participant ID          |
|-----------------------------------------------|-------------------------|
| City of Madrid - Urban Infrastructure Manager | MADRID_MUNICIPALITY     |
| SEAT - Automotive Innovation Leader           | CAR_MANUFACTURER_1      |
| Renault - Strategic Mobility Partner          | CAR_MANUFACTURER_2      |
| EMT Madrid - Public Transport Authority       | EMT_MADRID              |
| Madrid Road Maintenance Company               | ROADS_COMPANY_SL        |

## Additional Resources

- [Postman Documentation](https://learning.postman.com/docs/getting-started/introduction/)
