# Google Analytics 4 (GA4)

This page guides you through the process of setting up the Google Analytics source connector.

This connector supports GA4 properties through the [Analytics Data API v1](https://developers.google.com/analytics/devguides/reporting/data/v1).

## Prerequisites

* JSON credentials for the service account that has access to Google Analytics. For more details check [instructions](https://support.google.com/analytics/answer/1009702#zippy=%2Cin-this-article)
* OAuth 2.0 credentials for the service account that has access to Google Analytics
* Property ID
* Date Range Start Date
* Data request time increment in days (Optional)

## Custom reports

* Support for multiple custom reports
* Custom reports in format `[{"name": "<report-name>", "dimensions": ["<dimension-name>", ...], "metrics": ["<metric-name>", ...]}]`
* Custom report format when using segments and / or filters `[{"name": "<report-name>", "dimensions": ["<dimension-name>", ...], "metrics": ["<metric-name>", ...], "segments":  ["<segment-id-or-dynamic-segment-v3-format]", filter: "<filter-definition-v3-format>"}]`
* When using segments, make sure you add the `ga:segment` dimension.
* Custom reports: [Dimensions and metrics explorer](https://ga-dev-tools.web.app/dimensions-metrics-explorer/)

## Step 1: Set up Source

### Create a Service Account

First, you need to select existing or create a new project in the Google Developers Console:

1. Sign in to the Google Account you are using for Google Analytics as an admin.
2. Go to the [Service accounts page](https://console.developers.google.com/iam-admin/serviceaccounts).
3. Click `Create service account`.
4. Create a JSON key file for the service user. The contents of this file will be provided as the `credentials_json` in the UI when authorizing GA after you grant permissions \(see below\).

### Add service account to the Google Analytics account

Use the service account email address to [add a user](https://support.google.com/analytics/answer/1009702) to the Google analytics view you want to access via the API. You will need to grant [Viewer permissions](https://support.google.com/analytics/answer/2884495).

### Enable the APIs

1. Go to the [Google Analytics Reporting API dashboard](https://console.developers.google.com/apis/api/analyticsreporting.googleapis.com/overview) in the project for your service user. Enable the API for your account. You can set quotas and check usage.
2. Go to the [Google Analytics API dashboard](https://console.developers.google.com/apis/api/analytics.googleapis.com/overview) in the project for your service user. Enable the API for your account.

### Property ID

Specify the Property ID as set [here](https://analytics.google.com/analytics/web/a54907729p153687530/admin/property/settings)

## Step 2: Set up the source connector in Airbyte

Set the required fields in the Google Analytics Data API connector page such as the JSON credentials, property ID,
custom reports, date ranges start date, data request time increment in days.

## Supported sync modes

The Google Analytics source connector supports the following [sync modes](https://docs.airbyte.com/cloud/core-concepts#connection-sync-modes):
 - Full Refresh
 - Incremental

## Rate Limits & Performance Considerations \(Airbyte Open-Source\)

[Google Analytics Data API](https://developers.google.com/analytics/devguides/reporting/data/v1/quotas)

* Number of requests per day per project: 50,000

# Reports

The reports are custom by setting the dimensions and metrics required. To support Incremental sync, the `uuid` field is
added by default to any report. There are 8 default reports. To add more reports, you need to specify the `custom reports` field.

## Changelog

| Version | Date       | Pull Request                                             | Subject                                            |
|:--------|:-----------|:---------------------------------------------------------|:---------------------------------------------------|
| 0.1.0   | 2023-01-08 | [20889](https://github.com/airbytehq/airbyte/pull/20889) | Improved config validation, SAT                    |
| 0.0.3   | 2022-08-15 | [15229](https://github.com/airbytehq/airbyte/pull/15229) | Source Google Analytics Data Api: code refactoring |
| 0.0.2   | 2022-07-27 | [15087](https://github.com/airbytehq/airbyte/pull/15087) | fix documentationUrl                               |
| 0.0.1   | 2022-05-09 | [12701](https://github.com/airbytehq/airbyte/pull/12701) | Introduce Google Analytics Data API source         |
