# AI-Powered Industry News Monitor & Weekly Digest

An automated n8n workflow that monitors AI and automation news, uses OpenAI to identify strategically important developments, and sends a concise weekly intelligence digest to Slack.

## Workflow

The workflow runs every Monday at 9:00 AM Eastern Time and:

1. Fetches the TechCrunch AI and VentureBeat AI RSS feeds using separate HTTP Request nodes.
2. Parses and normalizes the RSS/XML content.
3. Removes duplicate and outdated articles.
4. Balances articles across both sources and limits the AI input to 15 items.
5. Uses OpenAI to select 3–5 source-grounded takeaways relevant to FocusKPI.
6. Formats the structured response into Slack Markdown.
7. Sends the finished digest to a Slack channel.

## Design Choices

TechCrunch AI provides timely reporting on product launches, funding, and major industry developments, while VentureBeat provides deeper enterprise coverage of AI infrastructure, agents, security, evaluation, and governance. The preprocessing stage removes HTML, filters articles to the previous seven days, deduplicates URLs and titles, balances both sources, and caps description length to control token usage. The OpenAI node returns strict structured JSON and is instructed to use only supplied articles, include real source URLs, and explain why each development matters to an AI consulting company. The final Slack digest contains a two-sentence executive summary and 3–5 concise takeaways with source links.

## Tools Used

- n8n AI Workflow Builder — created the initial workflow scaffold from my architecture prompt.
- OpenAI GPT-5.5 through n8n Connect — analyzed the live articles and generated the structured digest.
- ChatGPT — provided limited implementation guidance and troubleshooting.

I reviewed, customized, and tested the complete workflow, including preprocessing, source balancing, structured output, and Slack delivery.

## Import and Setup

1. Download [`AI & Automation Weekly Intelligence Digest.json`](./AI%20%26%20Automation%20Weekly%20Intelligence%20Digest.json).
2. Import it into n8n.
3. Connect an OpenAI credential or use n8n Connect.
4. Connect a Slack OAuth2 credential.
5. Select a Slack channel.
6. Execute the workflow once for testing, then publish it.

Credentials and API keys are not included in the exported workflow.
