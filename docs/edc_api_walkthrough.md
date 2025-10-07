# Walkthrough of the EDC Connector Management API

## Core Endpoints

| Resource | Endpoint |
|----------|----------|
| Asset | `<MANAGEMENT_API_URL>/v3/assets` |
| Policy Definition | `<MANAGEMENT_API_URL>/v3/policydefinitions` |
| Contract Definition | `<MANAGEMENT_API_URL>/v3/contractdefinitions` |
| Catalog | `<MANAGEMENT_API_URL>/v3/catalog` |
| Contract Negotiation | `<MANAGEMENT_API_URL>/v3/contractnegotiations` |
| Contract Agreement | `<MANAGEMENT_API_URL>/v3/contractagreements` |
| Transfer Process | `<MANAGEMENT_API_URL>/v3/transferprocesses` |
| EDR | `<MANAGEMENT_API_URL>/v3/edrs` |

## Create an Asset

An asset represents a resource that can be shared within the Dataspace, such as a file or a service endpoint.

```http
POST /v3/assets
Content-Type: application/json

{
  "@context": {
    "@vocabulary": "https://w3id.org/edc/v0.0.1/ns/",
    "dcat": "http://www.w3.org/ns/dcat#",
    "dct": "http://purl.org/dc/terms/"
  },
  "@id": "my-asset-id",
  "properties": {
    "dct:title": "My Asset",
    "dct:description": "Lorem Ipsum ...",
    "dct:language": "code/EN"
  },
  "dataAddress": {
    "@type": "DataAddress",
    "type": "HttpData",
    "baseUrl": "https://example.com"
  }
}
```

## Create a Policy Definition

A policy definition specifies the rules and conditions for accessing an asset.

```http
POST /v3/policydefinitions
Content-Type: application/json

{
  "@context": {
    "edc": "https://w3id.org/edc/v0.0.1/ns/"
  },
  "@id": "aPolicy",
  "policy": {
    "@context":"http://www.w3.org/ns/odrl.jsonld",
    "@type":"Set",
    "permission":[{
      "action":"use",
    }],
    "obligation":[],
    "prohibition":[]
  }
}
```

## Create a Contract Definition

A contract definition links assets with usage policies.

```http
POST /v3/contractdefinitions
Content-Type: application/json

{
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
  },
  "@id": "definition-id",
  "accessPolicyId": "aPolicy",
  "contractPolicyId": "aPolicy",
  "assetsSelector": [
    {
      "operandLeft":"@id",
      "operator":"in",
      "operandRight":"asset-id"
    }
  ]
}
```

## Request Catalog from another participant

The catalog endpoint allows consumers to discover available assets.

```http
POST /v3/catalog/request
Content-Type: application/json

{
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
  },
  "@type": "CatalogRequest",
  "counterPartyAddress": "https://provider.dataspaces.think-it.io/api/dsp",
  "counterPartyId": "MY_CONNECTOR_ID",
  "protocol": "dataspace-protocol-http",
  "additionalScopes": [
  ]
}
```

## Initiate Contract Negotiation

Contract negotiation is the process of establishing an agreement between a provider and a consumer for asset usage.

```http
POST /v3/contractnegotiations
Content-Type: application/json

{
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
  },
  "@type": "https://w3id.org/edc/v0.0.1/ns/ContractRequest",
  "counterPartyAddress": "https://provider.dataspaces.think-it.io/api/dsp",
  "protocol": "dataspace-protocol-http",
  "policy": {
    "@context": "http://www.w3.org/ns/odrl.jsonld",
    "@type": "odrl:Offer",
    "@id": "offer-id",
    "assigner": "MY_CONNECTOR_ID",
    "odrl:permission": {
        "odrl:action": {
            "@id": "use"
        }
    },
    "odrl:prohibition": [],
    "odrl:obligation": [],
    "target": "asset-id"
  }
}
```

## Initiate Transfer Process

The transfer process manages the actual data transfer between provider and consumer.

### PUSH Flow

```http
POST /v3/transferprocesses
Content-Type: application/json

{
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
  },
  "@type": "TransferRequest",
  "protocol": "dataspace-protocol-http",
  "counterPartyAddress": "{{https://provider.dataspaces.think-it.io/api/dsp}}",
  "contractId": "{{contract-id}}",
  "transferType": "HttpData-PUSH",
  "dataDestination": {
    "@type": "DataAddress",
    "type": "HttpData",
    "baseUrl": "https://example.com"
  }
}
```

### PULL Flow

```http
POST /v3/transferprocesses
Content-Type: application/json

{
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
  },
  "@type": "TransferRequest",
  "protocol": "dataspace-protocol-http",
  "counterPartyAddress": "{{https://provider.dataspaces.think-it.io/api/dsp}}",
  "contractId": "{{contract-id}}",
  "transferType": "HttpData-PULL"
}
```
