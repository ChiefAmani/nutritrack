# TECHNICAL_SPEC.md

## Project Overview
Integrate the `campaign_calendar.json` into marketing automation platforms for streamlined campaign deployment. This specification includes robust revision control and data integrity mechanisms to prevent file mismatches and ensure accurate campaign execution.

## Tech Stack
- Python==3.10.12 (for integration scripting/middleware)
- JSON (data format for campaign calendar)
- Marketing Automation Platform API (e.g., Mailchimp, HubSpot, Salesforce Marketing Cloud - specific platform to be determined by implementation team, but API interaction patterns defined here)

## File Tree
.
|-- src/
|   |-- main.py
|   `-- config.py
|-- tests/
|   `-- test_integration.py
|-- campaign_calendar.json
|-- requirements.txt
`-- .env

## API Endpoints (Conceptual for Marketing Automation Platform)
- Method: POST
- Path: /api/campaigns/create
- Request body: { "campaign_id": "string", "name": "string", "scheduled_date": "YYYY-MM-DD", "content": "string", "target_audience": "list of strings", "status": "string" }
- Response: { "status": "success", "message": "Campaign created", "platform_campaign_id": "string" }
- Auth: API Key or OAuth token required

- Method: PUT
- Path: /api/campaigns/update/{platform_campaign_id}
- Request body: { "name": "string", "scheduled_date": "YYYY-MM-DD", "content": "string", "target_audience": "list of strings", "status": "string" }
- Response: { "status": "success", "message": "Campaign updated" }
- Auth: API Key or OAuth token required

- Method: GET
- Path: /api/campaigns/{platform_campaign_id}
- Response: { "campaign_id": "string", "name": "string", "scheduled_date": "YYYY-MM-DD", "content": "string", "target_audience": "list of strings", "status": "string" }
- Auth: API Key or OAuth token required

## Environment Variables
- `MARKETING_AUTOMATION_API_KEY`
- `MARKETING_AUTOMATION_BASE_URL`
- `CAMPAIGN_CALENDAR_PATH` (path to `campaign_calendar.json`)

## Dependencies
fastapi==0.110.0
pydantic==2.6.1
requests==2.31.0
python-dotenv==1.0.1

## Revision Control and Data Integrity
### 1. Versioning of `campaign_calendar.json`
- All changes to `campaign_calendar.json` MUST be committed to version control (Git).
- Each commit MUST include a clear, descriptive message detailing the changes.
- A unique version identifier (e.g., Git commit hash or semantic version in metadata) MUST be associated with each deployed campaign set.

### 2. File Mismatch Detection
- Before any integration or update operation, the system MUST compare the `campaign_calendar.json` file's hash (e.g., MD5 or SHA256) with the hash of the last successfully processed version.
- If hashes do not match, the system MUST flag a potential mismatch and require explicit confirmation or a defined conflict resolution strategy.
- A log of processed `campaign_calendar.json` versions and their hashes MUST be maintained.

### 3. Routing Logic for Updates
- **New Campaigns:** Entries in `campaign_calendar.json` with no corresponding `platform_campaign_id` in the marketing automation platform will trigger a `POST /api/campaigns/create` operation.
- **Updated Campaigns:** Entries in `campaign_calendar.json` with a matching `platform_campaign_id` but differing content (detected by comparing relevant fields) will trigger a `PUT /api/campaigns/update/{platform_campaign_id}` operation.
- **Deleted Campaigns:** If a campaign present in the last processed `campaign_calendar.json` is absent in the current version, it will be flagged for review. Manual confirmation or a specific flag in the JSON (e.g., `"status": "archived"`) will be required for deletion or archiving in the marketing automation platform.
- **Error Handling:** All API interactions MUST include robust error handling, logging, and retry mechanisms. Failed operations MUST be reported and require manual intervention.

### 4. Scheduled Date Handling
- The `scheduled_date` in `campaign_calendar.json` will be used to schedule campaigns within the marketing automation platform.
- Any changes to `scheduled_date` for an existing campaign will trigger an update operation.
- The system MUST validate that `scheduled_date` is in the future for new or updated campaigns.
