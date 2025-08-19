# LinkedIn Posting Agent (n8n Workflow)

This repository contains a robust and compatible n8n workflow for an autonomous agent that streamlines the process of creating and publishing LinkedIn posts about AI news. The agent interacts with the user via Telegram, uses Google Gemini for content and image generation, and posts the final approved content to LinkedIn.

This workflow has been built using **core n8n nodes only** (like the HTTP Request node) to ensure maximum compatibility with any standard n8n setup, avoiding the need to install custom node packages.

## Features

- **Telegram-driven:** Initiate the workflow and manage the entire process from your Telegram chat.
- **AI-Powered Content Generation:** Leverages Google Gemini's REST API to draft professional and engaging LinkedIn posts from a simple text dump of news.
- **AI-Powered Image Generation:** Uses Google Gemini's REST API to create relevant and visually appealing images to accompany each post.
- **Simple Human-in-the-Loop Approval:** Review every post before it goes live. You have full creative control to approve or reject drafts with simple buttons inside Telegram.
- **Automated Re-drafting:** If a draft is rejected, the agent will ask for feedback and automatically generate a new version.
- **Automated Publishing:** Once approved, the agent automatically publishes the post and image to your LinkedIn profile.
- **Maximum Compatibility:** Built with the core `HTTP Request` node, ensuring it works on any n8n instance without extra installations.

## How to Use

Follow these steps to get the LinkedIn Posting Agent up and running in your n8n environment.

### 1. Import the Workflow

1.  **Download the workflow file:** Get the `linkedin_agent_workflow.n8n.json` file from this repository.
2.  **Open your n8n canvas.**
3.  **Import the workflow:** Click on `File > Import from File` and select the `linkedin_agent_workflow.n8n.json` file you downloaded. The complete workflow will appear on your canvas.

### 2. Configure Credentials

Before you can activate the workflow, you need to set up credentials for the services it uses. This workflow requires three credentials.

1.  **Go to the Credentials section** in your n8n instance (usually in the left-hand sidebar).
2.  **Add New Credentials** for each of the following:

    *   **Telegram Bot API:**
        *   **Type:** Search for and select `Telegram API`.
        *   **API Token:** You will need a Telegram Bot API token from the "BotFather" on Telegram.
        *   Give it a memorable name (e.g., "My Telegram Bot").

    *   **Gemini API Key (Header Auth):**
        *   **Type:** Search for and select `Header Auth`.
        *   **Name:** `x-goog-api-key` (This must be exact).
        *   **Value:** Your Google Gemini API key, which you can get from **Google AI Studio**.
        *   Give it a memorable name (e.g., "Gemini API Key").

    *   **LinkedIn API:**
        *   **Type:** Search for and select `LinkedIn OAuth2 API`.
        *   Follow the on-screen instructions to connect your LinkedIn account.
        *   Give it a memorable name (e.g., "My LinkedIn Profile").

3.  **Link Credentials in the Workflow:**
    *   Open the workflow and select each of the following nodes:
        *   `Telegram Trigger`, `Confirm Receipt`, `Ask for Approval`, `Ask for Feedback`, `Send Final Confirmation`: Select your **Telegram** credential.
        *   `HTTP Request to Gemini for Text`, `HTTP Request to Gemini for Image`, `HTTP Request to Re-draft Post`: Select your **Gemini API Key (Header Auth)** credential.
        *   `Publish to LinkedIn`: Select your **LinkedIn** credential.

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
