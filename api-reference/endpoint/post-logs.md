# API Reference: Log a generated output

Creates a `log` object recording the output of a tested `prompt`. The `log` is owned by the user and linked to a `prompt`.

## URL

```text
https://promptcrafter-production.up.railway.app/logs
```

## Method

`POST`

## Parameters

None

## Request headers

| Header name     | Required | Value                               |
|-----------------|----------|--------------------------------------------|
| `Authorization` | Yes      | `Authorization: Bearer {your_token}` |
| `Content-Type`  | Yes      | `application/json`          |

## Request body

A JSON object representing the new `log`. All fields are required except `notes` and `score`.

```json
{
  "promptId": "prompt101",
  "output": "The business report finds that revenue increased 12% last quarter, driven by strong online sales. Recommendations include expanding digital marketing and improving supply chain efficiency. No significant risks were found, but leadership should monitor supplier stability. Immediate action is suggested to secure long-term supplier contracts.",
  "notes": "Summary is clear and actionable. Matches requirements.",
  "modelUsed": "GPT-4o",
  "score": 9
}
```

## Example request

```shell
curl -X POST https://promptcrafter-production.up.railway.app/logs \
  -H "Authorization: Bearer {your_token}" \
  -H "Content-Type: application/json" \
  -d '{
    "promptId": "prompt101",
    "output": "The business report finds that revenue increased 12% last quarter, driven by strong online sales. Recommendations include expanding digital marketing and improving supply chain efficiency. No significant risks were found, but leadership should monitor supplier stability. Immediate action is suggested to secure long-term supplier contracts.",
    "notes": "Summary is clear and actionable. Matches requirements.",
    "modelUsed": "GPT-4o",
    "score": 9
  }'
```

## Response body

The newly created `log` object.

```json
{
  "_id": "log101",
  "promptId": "prompt101",
  "output": "The business report finds that revenue increased 12% last quarter, driven by strong online sales. Recommendations include expanding digital marketing and improving supply chain efficiency. No significant risks were found, but leadership should monitor supplier stability. Immediate action is suggested to secure long-term supplier contracts.",
  "notes": "Summary is clear and actionable. Matches requirements.",
  "modelUsed": "GPT-4o",
  "score": 9,
  "createdAt": "2024-06-20T13:10:00Z"
}
```

## Return status

| Status code | Status                 | Description                                           |
|-------------|------------------------|-------------------------------------------------------|
| 201         | Created                | Log created successfully.                             |
| 400         | Bad Request            | Required fields are missing or invalid.               |
| 401         | Unauthorized           | Authentication token is missing, expired, or invalid. |
| 404         | Not Found              | Prompt ID does not exist or is not accessible.        |
| 500         | Internal Server Error  | An unexpected server error occurred.                  |

## Related

[Retrieve all logs](reference/endpoints/get-logs.md): `GET /logs`  
[Retrieve logs for a specific prompt](reference/endpoints/get-logs-by-prompt.md): `GET /logs?promptId=...`  
[Delete a log](reference/endpoints/delete-logs-id.md): `DELETE /logs/:id`  
