# **RECAPP** 

#### **Automated pre-meeting audio briefings and client cheat sheets, powered by n8n, Eleven labs and Claude.** 

## **Inspiration** 

This project started with a real problem faced by one of our team member’s close relatives. When you have back-to-back client meetings all day, you rarely have even 10 spare minutes to dig through old Gmail threads just to remember who you're talking to and what was discussed last time. We wanted to build an automated assistant that pulls that context together for you and delivers a quick, hands-free briefing right before you hop on a call. 

## **What It Does** 

**RECAPP** gathers your past email history with a client, cross-references it with your own business profile, and sends both a written cheat sheet and an audio briefing straight to your inbox. It works in two ways: 

### **1. On-Demand Briefings (Manual Trigger)** 

- **Search & Structure:** Enter a client's name into the form, and the workflow pulls your past Gmail conversations with them into a structured format. 

- **Tailored Summary:** Using your personal/company profile as context, the AI summarizes the client's role, key background details, how they align with your goals, and questions they might bring up. 

- **Listen Anywhere:** ElevenLabs converts the written summary into a natural-sounding audio file. Both the MP3 and the transcript are emailed to you so you can prepare while driving, commuting on the train, or walking into the office! 

### **2. Automatic Calendar Prep (Scheduled Trigger)** 

- **Hands-Free Monitoring:** Every 5 minutes, **RECAPP** checks your Google Calendar for meetings starting within the next hour. 

- **Multi-Attendee Filtering:** If a meeting has multiple guests, the workflow loops through each attendee, pulls their email history, and weighs who is actually relevant to the meeting before generating your briefing—delivering it 60 minutes before the call starts. 

## **Tech Stack & Services Used** 

- **n8n:** Workflow orchestration, scheduling, multi-attendee looping, and data storage 

- **Google Calendar & Gmail APIs:** Event tracking, email retrieval, and briefing delivery 

- **Anthropic (Claude):** Contextual summarization and attendee relevance scoring 

- **ElevenLabs:** Text-to-speech audio generation 

## **How to Set It Up** 

Because **recapp** is an n8n workflow, anyone can import and run it in a few minutes without writing code from scratch: 

1. **Get n8n:** Sign up for n8n Cloud or run a local instance. 

2. **Import the Workflow:** Download client_summary.json from this repository. In n8n, open a blank workflow, click the **...** menu in the top-right corner, and select **Import from File** . 

3. **Connect Your Credentials:** Open the highlighted nodes and link your own accounts: 

   - **Google OAuth2** (for Gmail and Google Calendar) 

   - **Anthropic API Key** (for the AI Agent) 

   - **ElevenLabs API Key** (for audio generation) 

      - i. You must also select a AI voice from elevenlabs to make this area function 

4. **Add Your Profile:** Open the **About Me** node and fill in your role, company background, and goals so the AI tailors its advice to you. 

5. **Publish:** Click **Publish** in the top-right corner. Your calendar trigger will now run automatically in the background, and you can copy the **Production URL** from the form node to trigger briefings on demand. 

## **Challenges & What We Learned** 

The trickiest part of the build was handling Google Calendar events with multiple attendees. Instead of letting the AI get overwhelmed by mixed email threads, we used n8n's Split Out and Loop Over Items nodes to fetch and save each person's email history individually, merge them cleanly, and let the agent prioritize the most relevant details. Building this taught us a lot about structuring data pipelines in n8n and prompting AI agents to filter signal from noise. 

## **What's Next** 

- **Slack & SMS Delivery:** Sending 2-minute audio briefs directly to Slack or WhatsApp before meetings. 

- **Post-Meeting Follow-Ups:** Automatically drafting follow-up emails and action items once a calendar event ends. 

## **Team** 

- Built at **UBC LOOP Hackathon (Nov 2026)** by  Cody Luchangco, Eric Chen, Reo Suzuki and Joel Renaud. 

