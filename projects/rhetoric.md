# Rhetoric
rhetoric is an ai content generation and dissemination assistant.
## Concept
Rhetoric is a suite of tools for content creators. It allows users to leverage AI to generate text, images, and video for social medias like Medium, Twitter, and YouTube. It provides a GUI for interacting with generative AI models to generate and refine content. The suite also comes with tools for automating routine social media tasks like commenting, liking, and following other users. It allows you to schedule your content releases to these platforms and for the running of automations.

To make things a little bit easier for users to understand the interfaces with generative AI APIs are referred to as "assistants".

e.g. use the blog assistant to generate, augment, or refine your next blog.
## Content Generation
### Blogs (Medium)
rhetoric allows you to generate blogs from seed content like a summary or notes, or even a topic.
the chat interface allows you to easily iterate on your blog until you're happy.
the same is possible for the blog image via image generation.
### Posts (Twitter)
rhetoric allows you to generate posts from seed content, in the same way as blogs.
you also have the option to add generated images to your posts.
you can choose to review the tweets or just set the twitter assistant on autopilot.
there is also an optional engagement assistant that can run tasks like commenting, liking, and following.
the engagement assistant can be configured to run flows at specific times (temporal trigger) or after a delay following an interaction with your account (response trigger).
### Video (YouTube)
rhetoric can generate short video content from your seed content.
this requires some configuration in order to fine-tune the output.
## Technology
### Architecture
rhetoric uses a simple client-server architecture with the frontend running in a separate process to the backend and communication between them using HTTP and the javascript fetch library.
### Frontend
rhetoric's frontend is built in javascript svelte with the flowbite component library.
### Backend
rhetoric's backend runs on python fastapi.
### Hosting
rhetoric is hosted on google cloud run.
### Models
rhetoric uses models from openai, stability, and other generative ai service providers.
rhetoric may one day offer self-hosted open-source highly optimized ai assistants but not yet.