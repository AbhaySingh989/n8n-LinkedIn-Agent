# LinkedIn Posting Agent (n8n Workflow)

This repository contains an n8n workflow for an autonomous agent that streamlines the process of creating and publishing LinkedIn posts about AI news. The agent interacts with the user via Telegram, uses Gemini for content and image generation, and posts the final approved content to LinkedIn.

## Features

- **Telegram-driven:** Initiate the workflow and manage the entire process from your Telegram chat.
- **AI-Powered Content Generation:** Leverages Gemini to draft professional and engaging LinkedIn posts from a simple text dump of news.
- **AI-Powered Image Generation:** Creates relevant and visually appealing images to accompany each post.
- **Human-in-the-Loop Approval:** Review every post before it goes live. You have full creative control to approve or reject drafts.
- **Automated Publishing:** Once approved, the agent automatically publishes the post and image to your LinkedIn profile.
- **End-to-End Automation:** A fully automated workflow from content idea to a live LinkedIn post.

## How to Use

Follow these steps to get the LinkedIn Posting Agent up and running in your n8n environment.

### 1. Import the Workflow

1.  **Download the workflow file:** Get the `linkedin_agent_workflow.n8n.json` file from this repository.
2.  **Open your n8n canvas.**
3.  **Import the workflow:** Click on `File > Import from File` and select the `linkedin_agent_workflow.n8n.json` file you downloaded. The complete workflow will appear on your canvas.

### 2. Configure Credentials

Before you can activate the workflow, you need to set up credentials for the services it uses. In the n8n workflow, you will see placeholder credentials (e.g., `{{ telegram_api_key }}`). You need to replace these with your actual n8n credentials.

1.  **Go to the Credentials section** in your n8n instance (usually in the left-hand sidebar).
2.  **Add New Credentials** for each of the following services if you haven't already:
    *   **Telegram:**
        *   You will need a **Telegram Bot API token**. You can get this from the "BotFather" on Telegram.
        *   Select "Telegram" as the credential type and enter your API token.
    *   **Gemini (or Google Vertex AI):**
        *   The workflow uses a Gemini model. You will need an API key from Google AI Studio or a service account key for Vertex AI.
        *   The example workflow uses a generic `geminiApi` credential. You may need to use the "Google" or "Vertex AI" credential type depending on your n8n version and setup.
    *   **LinkedIn:**
        *   You will need to create a LinkedIn app and get OAuth 2.0 credentials.
        *   Select "LinkedIn (OAuth2)" as the credential type and follow the on-screen instructions to connect your LinkedIn account.
    *   **Image Generation:**
        *   The workflow uses a placeholder `imageGeneration` node. You can replace this with any image generation service you prefer (e.g., another call to Gemini/Imagen via the Vertex AI node, or a different service like DALL-E via an HTTP Request node).
        *   You will need to create a credential for your chosen image generation service.

3.  **Link Credentials in the Workflow:**
    *   For each node that has a "Credentials" section (e.g., Telegram Trigger, Draft Post with Gemini, Publish to LinkedIn), select the credential you created from the dropdown menu.

### 3. Special Setup for the "Wait for Approval" Node

The approval process in this workflow relies on a `Wait` node that pauses the execution until you reply on Telegram. This requires a one-time setup to connect Telegram's webhooks to your n8n instance.

**This step is crucial for the approval/rejection loop to work.**

1.  **Get the Webhook URL:**
    *   The `Wait for Approval` node in the workflow is configured to resume on a webhook call. When the workflow runs, it will generate a unique webhook URL for each execution.
    *   To make this work seamlessly, you need a static webhook URL that Telegram can always send replies to.

2.  **Create a Webhook Trigger Workflow:**
    *   The standard n8n practice for this is to create a *separate, simple workflow* that consists of only a **Webhook** node.
    *   This Webhook node will give you a **static URL**. Copy this URL.
    *   Set your Telegram bot's webhook to this URL using a command like this (replace `<YOUR_BOT_TOKEN>` and `<YOUR_N8N_WEBHOOK_URL>`):
        `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/setWebhook?url=<YOUR_N8N_WEBHOOK_URL>`
    *   Now, all replies to your bot will be sent to this webhook.

3.  **Resume the Main Workflow:**
    *   The `Wait` node in the main workflow needs to be told which execution to resume. This is typically done by passing a `workflowId` or a unique identifier.
    *   A more advanced version of this workflow would involve storing the `workflowId` of the main flow and using the webhook workflow to resume it.
    *   For simplicity, this workflow assumes a basic `Wait` node setup. Depending on your n8n version, you may need to adjust the `Wait` node's configuration to correctly correlate the reply from the user.

### 4. Activate and Run the Workflow

1.  **Save the workflow.**
2.  **Activate the workflow** using the toggle switch at the top right of the n8n canvas.
3.  **Start a conversation with your Telegram bot.**
4.  **Send a message** containing a news article, a summary, or any text dump you want to turn into a LinkedIn post.
5.  **Follow the bot's instructions** to approve or reject the draft.
6.  Once you approve, the post will be published to your LinkedIn profile, and you'll receive a confirmation message with the link.

Enjoy your automated LinkedIn content creation!
