# Pipedrive GraphQL Schema

## Overview

This document describes a conceptual GraphQL schema for the Pipedrive CRM API. Pipedrive provides a REST API at `https://api.pipedrive.com/v1` (and v2 endpoints). This schema models the same domain as a GraphQL service, enabling clients to fetch precisely the fields they need across deals, persons, organizations, activities, leads, products, pipelines, goals, subscriptions, and platform objects.

The schema is derived from the [Pipedrive REST API reference](https://developers.pipedrive.com/docs/api/v1) and covers the full breadth of entities exposed by Pipedrive's sales CRM platform.

## Authentication

Pipedrive supports two authentication modes:

- **API Token** — pass `api_token` as a query parameter or in the `Authorization` header for custom integrations.
- **OAuth 2.0** — used by Marketplace apps. Obtain an access token via the authorization code flow at `https://oauth.pipedrive.com/oauth/authorize`.

A GraphQL implementation would require the same credentials in request headers:

```
Authorization: Bearer <access_token>
```

or

```
Authorization: Bearer <api_token>
```

## Schema Design

The schema organizes Pipedrive's domain into the following groups:

### Core Sales Pipeline

- **Pipeline** — top-level sales process container
- **Stage** — ordered steps within a pipeline with win probability
- **Deal** — the central revenue-generating record
- **DealStage** — the current or historical stage assignment of a deal
- **DealHistory** — audit trail of field changes on a deal
- **DealProduct** — a product line item attached to a deal
- **StageChange** — records a deal's transition from one stage to another

### People and Organizations

- **Person** — a contact record (individual human)
- **PersonField** — a custom field definition scoped to persons
- **Organization** — a company grouping persons and deals
- **OrganizationField** — a custom field definition scoped to organizations
- **Follower** — a user following a deal, person, or organization

### Leads

- **Lead** — a pre-qualified opportunity in the Leads Inbox before conversion to a deal
- **LeadLabel** — a color-coded category label applied to leads
- **LeadSource** — the origin channel of a lead

### Activities and Communication

- **Activity** — a scheduled or completed task (call, meeting, email, deadline)
- **ActivityType** — a configurable category defining valid activity kinds
- **Note** — free-form text attached to deals, persons, organizations, or leads
- **File** — an uploaded attachment linked to a CRM record
- **MailThread** — an email conversation synced via Smart Email BCC or 2-way sync
- **MailMessage** — an individual email within a mail thread
- **Channel** — a communication channel connector
- **PersonChannel** — links a communication channel to a person
- **OrganizationChannel** — links a communication channel to an organization
- **DealChannel** — links a communication channel to a deal

### Products and Pricing

- **Product** — a catalog item with name, code, unit, and prices
- **ProductVariation** — a variant of a product (size, color, configuration)
- **ProductPrice** — a currency-specific price for a product
- **Discount** — a percentage or fixed discount applied to a deal product
- **Tax** — a tax rate applied to a deal product or quote

### Revenue and Subscriptions

- **Subscription** — a recurring revenue contract attached to a deal
- **SubscriptionRecurrence** — schedule definition (monthly, annual, custom intervals)
- **Revenue** — a recognized revenue entry
- **RevenueHistory** — historical revenue records over time

### Goals and Reporting

- **Goal** — a quantitative target (deal count, won value) for a user, team, or pipeline
- **GoalResult** — the measured achievement against a goal in a period
- **GoalTracker** — tracks progress toward a goal over time

### Users and Access Control

- **User** — a Pipedrive seat holder (sales rep, manager, admin)
- **UserAccess** — the permissions granted to a user
- **UserSetting** — per-user configuration preferences
- **Team** — a named group of users
- **TeamMember** — a user's membership in a team
- **Role** — a named permission set
- **RoleAssignment** — assigns a role to a user
- **Permission** — an individual access rule within a role
- **SharingSetting** — visibility configuration for a record

### Filters and Search

- **Filter** — a saved query definition (saved view)
- **FilterCondition** — an individual predicate within a filter
- **SearchResult** — a polymorphic result returned from global search

### Custom Fields

- **Field** — a custom field definition (key, label, field type, options)
- **FieldValue** — the value of a custom field on a specific record
- **CustomField** — a domain-specific alias for Field
- **CustomFieldValue** — a domain-specific alias for FieldValue
- **Label** — a color tag applied to deals, persons, or organizations

### Webhooks and Events

- **Webhook** — a subscription to a Pipedrive event type with a target URL
- **Socket** — a real-time push channel

### Platform and Auth

- **Currency** — a supported currency with code, symbol, and exchange rate
- **APIKey** — an API token credential for a user
- **OAuth2** — OAuth 2.0 client credentials and token metadata
- **Visibility** — enum-style record of visibility levels
- **UsageSummary** — API token usage statistics

### Quotes and Orders

- **Quote** — a formal price proposal attached to a deal
- **QuoteItem** — a line item in a quote
- **Invoice** — a billing document
- **Order** — a fulfilled order
- **ItemPrice** — the price of a quote or order line item

## Query Examples

### Fetch a deal with its stage, person, and products

```graphql
query GetDeal($id: ID!) {
  deal(id: $id) {
    id
    title
    value
    currency
    status
    probability
    stage {
      id
      name
      pipeline {
        id
        name
      }
    }
    person {
      id
      name
      email {
        value
        primary
      }
    }
    organization {
      id
      name
    }
    products {
      id
      name
      quantity
      itemPrice
      discount {
        type
        value
      }
    }
    owner {
      id
      name
    }
  }
}
```

### List open deals in a pipeline with pagination

```graphql
query ListDeals($pipelineId: ID!, $after: String) {
  deals(pipelineId: $pipelineId, status: OPEN, first: 20, after: $after) {
    edges {
      node {
        id
        title
        value
        expectedCloseDate
        stage {
          name
          orderNr
        }
        person {
          name
        }
      }
    }
    pageInfo {
      hasNextPage
      endCursor
    }
  }
}
```

### Create a deal

```graphql
mutation CreateDeal($input: CreateDealInput!) {
  createDeal(input: $input) {
    deal {
      id
      title
      value
      stage {
        id
        name
      }
    }
  }
}
```

## Type Count

The schema defines **68 named types** covering the full Pipedrive domain including scalars, enums, input types, object types, and union types.

## Source Reference

- REST API Reference: https://developers.pipedrive.com/docs/api/v1
- Developer Documentation: https://developers.pipedrive.com/
- GitHub Organization: https://github.com/pipedrive
- LLMs.txt: https://developers.pipedrive.com/llms.txt
