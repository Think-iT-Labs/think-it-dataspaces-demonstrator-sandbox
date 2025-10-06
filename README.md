# Think-it Dataspaces Demonstrator Sandbox

AWS Sandbox for Think-it Data Spaces Demonstrator

## Lab Phases

### Phase 1: Secure and Sovereign Data Integration

### Phase 2: Discovery & Assessment

### Phase 3: Contract Negotiation & Policy Configuration

### Phase 4: Data Transfer & Integration

### Phase 5: Reporting & Verification

## Postman Configuration Guide

### Configuring Postman to Interact with the Connector

1. **Import the Collection**:
   - Navigate to the `collections/Postman/` directory.
   - Import the `Think-it EDC Connector - Basic.json` file into Postman.

2. **Set Up the Base URL of your Connector**:
   - Define the following variables in your Postman environment:
     - `base_url`: The base URL of your connector's HTTP API.

3. **Authentication**:
   - Ensure that the necessary authentication header `api_key` is configured in the Postman collection.

4. **Testing the Connector Endpoints**:
   - Use the provided requests to interact with the connector.
