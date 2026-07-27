---
name: Triage and resolve a Huntress incident report
description: List SOC incident reports, inspect one, review its remediations, bulk-approve them, and record a resolution.
api: openapi/huntress-rest-openapi.json
operations: [getV1IncidentReports, getV1IncidentReportsId, getV1IncidentReportsIncidentReportIdRemediations, postV1IncidentReportsIncidentReportIdRemediationsBulkApproval, postV1IncidentReportsIdResolution]
---

# Triage and resolve a Huntress incident report

Authenticate with HTTP Basic (username = API key, password = API secret) against
`https://api.huntress.io/v1`. All list endpoints are cursor-paginated with
`limit` + `page_token`; follow `pagination.next_page_token` until empty.

1. **List open incident reports** — `getV1IncidentReports` (`GET /v1/incident_reports`).
   Filter/paginate to the reports you need to triage.
2. **Inspect a report** — `getV1IncidentReportsId` (`GET /v1/incident_reports/{id}`)
   to read the detection detail. A report can only be actioned when its status is `sent`.
3. **Review remediations** — `getV1IncidentReportsIncidentReportIdRemediations`
   (`GET /v1/incident_reports/{incident_report_id}/remediations`).
4. **Bulk approve** the remediations you trust —
   `postV1IncidentReportsIncidentReportIdRemediationsBulkApproval`
   (`POST /v1/incident_reports/{incident_report_id}/remediations/bulk_approval`).
5. **Resolve** — `postV1IncidentReportsIdResolution`
   (`POST /v1/incident_reports/{id}/resolution`).

Error rules: `403` = credential/permission issue; `404` = report not found;
`409`/`422` = the report is not in `sent` status (do not retry until status changes).
See errors/huntress-problem-types.yml.
