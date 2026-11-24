# AI Video Generation Workflow

An n8n workflow that automates the path from a simple video idea to an AI-generated video, using Google Gemini to write the prompt and Luma AI (Dream Machine) to generate the video.

## The workflow

1. **Manual Trigger** - starts the run (swap for a webhook, Telegram, or schedule trigger later).
2. **Video Idea** - holds the rough idea for the video.
3. **Enhance Prompt (Gemini)** - sends the idea to the Gemini API, which turns it into a detailed, cinematic video prompt.
4. **Extract Prompt** - a Code node that pulls the enhanced prompt out of the Gemini response.
5. **Start Generation (Luma AI)** - sends the prompt to the Luma Dream Machine API to start video generation.
6. **Wait** - pauses while the video renders.
7. **Check Video Status** - polls the generation's status.
8. **Is Video Ready?** - if not ready, loops back to Wait; if completed, continues.
9. **Video Ready** - passes on the finished video's URL and metadata.

This project is mostly about working with APIs and asynchronous workflows: different AI services chained into one automated pipeline.

## Tech stack

- n8n
- Google Gemini API (prompt generation and enhancement)
- Luma AI Dream Machine API (video generation)
- REST APIs and JavaScript Code nodes

## Setup

1. Import `workflow.json` into n8n (Workflows, Import from File).
2. Add two credentials in n8n and select them on the HTTP nodes:
   - Gemini: Query Auth credential, parameter `key`, with your Google AI Studio API key.
   - Luma AI: Header Auth credential, header `Authorization`, value `Bearer YOUR_LUMA_API_KEY`.
3. Check the current Gemini and Luma model names/endpoints in their docs and update the node URLs if needed; model names change over time.
4. Run the workflow with your own idea in the "Video Idea" node.

## Notes

- No real API keys are included anywhere in this repo; they stay in your own n8n credential store.
- Video generation is a paid API feature; check Luma and Gemini pricing before running.
