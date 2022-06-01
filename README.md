# n8n-scalable

[Queue mode](https://docs.n8n.io/hosting/scaling/queue-mode/)

- [x] Configure workers
- [x] Configure webhooks
- [x] Configure master

```bash
docker compose up n8n-worker-1 n8n-master n8n-worker-2 n8n-webhook-1
```

Create a simple webhook workflow

```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "Start",
      "type": "n8n-nodes-base.start",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {
        "path": "235cdfe3-ddba-4567-b8c7-fb9aff056d5b",
        "options": {}
      },
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [
        450,
        450
      ],
      "webhookId": "235cdfe3-ddba-4567-b8c7-fb9aff056d5b"
    }
  ],
  "connections": {}
}
```

The webhook URL will be create with port number `5678`: `http://localhost:5678/webhook/235cdfe3-ddba-4567-b8c7-fb9aff056d5b`

Change the port number for `5679` and open the URL: `http://localhost:5679/webhook/235cdfe3-ddba-4567-b8c7-fb9aff056d5b`

You will see logs like that:
```bash
n8n-scalable-n8n-webhook-1-1  | Started with ID: 1
n8n-scalable-n8n-worker-2-1   | Start job: 1 (Workflow ID: 1 | Execution: 9)
n8n-scalable-n8n-webhook-1-1  | Started with ID: 2
n8n-scalable-n8n-worker-2-1   | Start job: 2 (Workflow ID: 1 | Execution: 10)
n8n-scalable-n8n-webhook-1-1  | Started with ID: 3
n8n-scalable-n8n-worker-2-1   | Start job: 3 (Workflow ID: 1 | Execution: 11)
n8n-scalable-n8n-webhook-1-1  | Started with ID: 4
n8n-scalable-n8n-worker-1-1   | Start job: 4 (Workflow ID: 1 | Execution: 12)
n8n-scalable-n8n-webhook-1-1  | Started with ID: 5
n8n-scalable-n8n-worker-2-1   | Start job: 5 (Workflow ID: 1 | Execution: 13)
n8n-scalable-n8n-webhook-1-1  | Started with ID: 6
n8n-scalable-n8n-worker-1-1   | Start job: 6 (Workflow ID: 1 | Execution: 14)
n8n-scalable-n8n-webhook-1-1  | Started with ID: 7
n8n-scalable-n8n-worker-2-1   | Start job: 7 (Workflow ID: 1 | Execution: 15)
n8n-scalable-n8n-webhook-1-1  | Started with ID: 8
n8n-scalable-n8n-worker-1-1   | Start job: 8 (Workflow ID: 1 | Execution: 16)
```