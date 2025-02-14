---
tap: "bing-ads"
version: "2"

name: "age_gender_audience_report"
doc-link: https://docs.microsoft.com/en-us/advertising/reporting-service/agegenderaudiencereportfilter?view=bingads-13
singer-schema: ## link to the JSON schema file in the integration's Singer repo
description: |
  The `{{ table.name }}` table contains info about the age and gender demographics of people interacting with your campaigns and ad groups.

  [This is a **Report** table](#replication). See the **Replication** section for information on how data is replicated and loaded for this table.

replication-method: "Key-based Incremental"
loading-behavior: "Append-Only"

attribution-window: true

attributes:
  - name: "AccountId"
    type: "integer"
    primary-key: true
    description: "The Bing Ads-assigned ID of the account."
    foreign-key-id: "account-id"

  - name: "{{ system-column.report-date-time }}"
    type: "date-time"
    primary-key: true
    description: "The start time of the Stitch replication job that replicated this record."

  - name: "TimePeriod"
    type: "date"
    primary-key: true
    replication-key: true
    description: "The day the record pertains to."

  - name: "AdGroupId"
    type: "integer"
    description: "The ID of the ad group."
    foreign-key-id: "ad-group-id"

  - name: "CampaignId"
    type: "integer"
    description: "The ID of the campaign."
    foreign-key-id: "campaign-id"

  - name: "AccountName"
    type: "string"
    description: "The account name."

  - name: "AdGroupName"
    type: "string"
    description: "The ad group name."

  - name: "AgeGroup"
    type: "string"
    description: "The age group of the audience who might have viewed the ad."

  - name: "Gender"
    type: "string"
    description: "The gender of the audience who might have viewed the ad."

  - name: "Custom Fields"
    description: |
      Columns selected by you. For descriptions of available columns, refer to [Microsoft's documentation]({{ table.doc-link }}).
---