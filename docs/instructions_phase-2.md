# Phase 2: Discovery & Assessment

> Learning Objective: Understand data space catalog discovery and asset identification

## Mission Brief

Your team has identified 4 key supplier categories (2 car manufacturers, the municipality of Madrid, EMT Madrid and the road maintenance company) that have relevant data. Time to discover what data is actually available in the data space network.

## Quest Tasks

### Identify partner organizations to query for available datasets

Review the list of participants in the data space network and note their DSP endpoint URLs (e.g., `https://partner-company.dataspace-sandbox.think-it.io/api/dsp`).

### Discover available data catalogs from partner organizations

With Postman, use the `Request Catalog V3` request:

- In the Pre-request Script tab, set `counterPartyAddress` to the target connector's DSP endpoint
- Send the request to fetch the partner's catalog
- Repeat for each partner organization you want to discover their catalog of offers

### Review catalog responses and identify relevant datasets

For each catalog response:

- Examine the available datasets and their metadata (title, description, properties)
- Note the `@id` field of datasets you're interested in (you'll need this for negotiation)
- Review the `odrl:hasPolicy` section to understand usage requirements and constraints

### Document your findings across all partner catalogs

Create a summary of:

- Which partners have relevant datasets for your use case
- The asset IDs and offer IDs you plan to negotiate
- Any policy constraints that might affect your usage
