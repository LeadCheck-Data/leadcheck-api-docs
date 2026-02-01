# LeadCheck API Documentation

[![License: Proprietary](https://img.shields.io/badge/License-Proprietary-blue.svg)](https://leadcheck.co.uk)
[![Status: Active](https://img.shields.io/badge/Status-Active-success.svg)](https://leadcheck.co.uk)
[![Region: UK](https://img.shields.io/badge/Region-UK%20Only-red.svg)](https://leadcheck.co.uk)

**LeadCheck** is a UK-specific data validation utility for residential property data. 

This repository contains the schema definitions, response examples, and integration patterns for the LeadCheck API.

## Overview

The LeadCheck API allows developers to programmatically validate UK addresses against multiple government and proprietary datasets in real-time. It is designed for high-volume data processing, enabling teams to filter records based on:

* **HM Land Registry** (Price Paid Data & Tenure)
* **EPC Register** (Energy Performance Certificates)
* **Retrofit Eligibility** (ECO4, GBIS, Warm Homes Plan & Insulation criteria)

## Usage

To use the live API, you must obtain an API key from the main dashboard.

👉 **[Get API Key at LeadCheck.co.uk](https://leadcheck.co.uk/?utm_source=github&utm_medium=referral&utm_campaign=get_api_key)**

### Authentication
The API uses Bearer Token authentication. Include your API key in the header of all requests.

```bash
curl -X GET [https://api.leadcheck.co.uk/v1/property/SW1A1AA](https://api.leadcheck.co.uk/v1/property/SW1A1AA) \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## JSON Response Example

When querying a valid UK postcode, the API returns a standardized JSON object containing property attributes.

**Request:**
`GET /v1/validate?postcode=SW1A1AA`

**Response:**
```json
{
  "status": "success",
  "meta": {
    "timestamp": "2026-02-01T10:00:00Z",
    "region": "GB-ENG"
  },
  "data": {
    "address": {
      "postcode": "SW1A 1AA",
      "uprn": "100023336956"
    },
    "property_attributes": {
      "tenure": "Freehold",
      "property_type": "Detached",
      "last_sold_date": "2010-05-20",
      "last_sold_price": 450000
    },
    "epc_data": {
      "current_rating": "D",
      "potential_rating": "B",
      "lodgement_date": "2025-01-15",
      "total_floor_area": 98
    },
    "retrofit_eligibility": {
      "eco4_qualified": true,
      "warm_homes_plan_eligible": true,
      "gbis_qualified": false,
      "measures_recommended": [
        "Solar PV",
        "External Wall Insulation",
        "Heat Pump"
      ]
    }
  }
}
```

## Rate Limits

The public API is rate-limited to ensure stability.
* **Sandbox:** 50 requests/hour
* **Production:** Custom (See dashboard)

## Licensing

This schema and documentation are proprietary to **LeadCheck Data Solutions**. 
For full documentation, SLAs, and support, visit the official portal.

[**View Full Documentation**](https://leadcheck.co.uk/?utm_source=github&utm_medium=referral&utm_campaign=api_docs)
