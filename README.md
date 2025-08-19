# LinkedIn Posting Agent (n8n Workflow)

This repository contains a robust, corrected n8n workflow for an autonomous agent that streamlines the process of creating and publishing LinkedIn posts about AI news. The agent interacts with the user via Telegram, uses Google Gemini for content and image generation, and posts the final approved content to LinkedIn.

This workflow has been built and verified against the latest n8n standards to ensure all nodes are supported and all connections are correct.

## Features

- **Telegram-driven:** Initiate the workflow and manage the entire process from your Telegram chat.
- **AI-Powered Content Generation:** Leverages Google Gemini to draft professional and engaging LinkedIn posts from a simple text dump of news.
- **AI-Powered Image Generation:** Uses Google Gemini to create relevant and visually appealing images to accompany each post.
- **Simple Human-in-the-Loop Approval:** Review every post before it goes live. You have full creative control to approve or reject drafts with simple buttons inside Telegram.
- **Automated Re-drafting:** If a draft is rejected, the agent will ask for feedback and automatically generate a new version.
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
        *   In n8n, search for the "Telegram" credential type and enter your API token. Give it a name (e.g., "My Telegram Bot").
    *   **Google Gemini:**
        *   The workflow uses the official Google Gemini node. You will need an API key from **Google AI Studio**.
        *   In n8n, search for the "Google Gemini API" credential type and enter your API key. Give it a name (e.g., "My Gemini Key").
    *   **LinkedIn:**
        *   You will need to create a LinkedIn app and get OAuth 2.0 credentials.
        *   In n8n, search for the "LinkedIn OAuth2" credential type and follow the on-screen instructions to connect your LinkedIn account. Give it a name (e.g., "My LinkedIn Profile").

3.  **Link Credentials in the Workflow:**
    *   For each node that has a "Credentials" section (Telegram, Google Gemini, LinkedIn), select the credential you created from the dropdown menu.

### 3. Activate and Run the Workflow

1.  **Save the workflow** by clicking the "Save" button.
2.  **Activate the workflow** using the toggle switch at the top right of the n8n canvas.
3.  **Start a conversation with your Telegram bot.**
4.  **Send a message** containing a news article, a summary, or any text dump you want to turn into a LinkedIn post.
5.  The agent will send you a draft of the post along with a generated image.
6.  **Click the "✅ Approve" or "❌ Reject" buttons** directly in the Telegram message.
7.  If you reject, the bot will ask for feedback. Simply reply with your comments, and it will generate a new draft.
8.  Once you approve, the post will be published to your LinkedIn profile, and you'll receive a final confirmation message with the link.

Enjoy your new, streamlined content creation process!
