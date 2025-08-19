​User Story 1: Initiate Post Generation
​As a working professional,
I want to initiate the LinkedIn post creation process by sending a text dump of news to the Telegram bot,
so that the agent can start working on a draft on my behalf.
​Acceptance Criteria:
​GIVEN the Telegram bot is active and listening for messages,
​WHEN I send a message containing unstructured AI-related news content,
​THEN the n8n workflow must trigger successfully, and the message content must be captured.
​AND the agent must immediately send a brief, conversational message back to me confirming receipt of the content and indicating that it is now drafting the post.
​User Story 2: Generate & Present a Post Draft
​As an n8n agent,
I want to process a user's raw text dump using the Gemini model to generate a polished LinkedIn post draft and a relevant image,
so that I can present a complete, ready-to-publish post for the user's review.
​Acceptance Criteria:
​GIVEN a user's news dump has been captured by the workflow,
​WHEN the agent calls the Gemini model with a prompt to refine the content,
​THEN the model's response must include a well-structured and professional post body, complete with appropriate hashtags.
​AND the agent must use a separate prompt to generate or select a relevant image to accompany the post.
​AND the agent must then compile the post text and image into a single, cohesive draft and present it to the user via Telegram.
​User Story 3: Manage Post Approval and Re-drafting
​As a user,
I want to review the post draft in Telegram and have a clear way to either approve it for immediate publication or reject it with feedback for revision,
so that I can maintain creative control over the final content before it goes live.
​Acceptance Criteria:
​GIVEN I have received a post draft from the agent,
​WHEN I reply with the command "approve,"
​THEN the workflow must correctly identify this command and proceed to the publication step.
​GIVEN I have received a post draft from the agent,
​WHEN I reply with the command "reject" followed by text feedback,
​THEN the workflow must correctly identify the rejection, capture my feedback, and return to the drafting phase to generate a new version based on my suggestions.
​AND if I reply with an invalid command, the agent must send a message prompting me to use the correct "approve" or "reject" commands without exiting the review loop.
​User Story 4: Publish Final Content to LinkedIn
​As an n8n agent,
I want to publish the final, approved post to the user's LinkedIn profile,
so that the entire workflow is fully automated from content idea to public post.
​Acceptance Criteria:
​GIVEN a post draft has been explicitly approved by the user,
​WHEN the agent executes the LinkedIn posting action,
​THEN the post must be successfully published to the user's profile.
​AND the published post must include both the final text and the accompanying image.
​AND the agent must send a final confirmation message to the user via Telegram, including a link to the live post on LinkedIn.
