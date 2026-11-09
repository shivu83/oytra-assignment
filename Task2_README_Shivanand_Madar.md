# Task 2 – n8n API Integration Workflow
Candidate: Shivanand Suresh Madar

## APIs used
- Hacker News Firebase API: `https://hacker-news.firebaseio.com/v0/topstories.json` returns the current top-story IDs.
- Hacker News item endpoint: `https://hacker-news.firebaseio.com/v0/item/{id}.json` enriches each selected ID with title, URL, score, author and timestamp.

## Workflow logic
1. Schedule Trigger runs every hour.
2. HTTP Request fetches the top-story IDs.
3. Code node keeps the first five IDs.
4. HTTP Request fetches the details for each story.
5. Code node normalizes fields and supplies a fallback URL/title when missing.
6. IF node checks whether each story score is at least 100.
7. Separate Code nodes build a high-score digest or a below-threshold summary.
8. Email node sends the result.

## Credentials and setup
- Import the JSON into n8n.
- Create an SMTP credential in n8n Credentials. Attach it to the Email node; replace the placeholder sender and recipient with valid addresses.
- Do not put passwords or API secrets directly in node parameters.
- Save the workflow and execute it manually once before enabling the hourly schedule.

## Error handling
The HTTP Request nodes are configured to continue regular output on error and have error outputs connected to an Error Fallback Log Code node. Confirm the behavior in your n8n version after import. If your version does not expose error outputs for these nodes, configure the node's On Error setting to `Continue (using error output)` and reconnect the error output to the fallback logger. Inspect the execution log for failed calls.

## Verification status
This JSON is a starter workflow definition. It has not been imported into a live n8n instance, credentials have not been configured, and no successful execution screenshot is included. Validate node versions and connections in your n8n installation before submission.
