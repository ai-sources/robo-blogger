# Robo Blogger

Robo Blogger is an assistant for Voice-to-Content designed for blog posts. It allows the user simply record a summary of their ideas and will convert these into a polished blog post, using optionally provided links (e.g., documentation) and / or blog post outline to ground the writing process.

![robo-blogger](https://github.com/user-attachments/assets/0599ebc3-bcd7-4a1f-abe5-07ee4e828ec8)

## Quickstart

Set API keys for the LLM of choice (default is Anthropic Claude 3.5 Sonnet):
```
export ANTHROPIC_API_KEY=<your_anthropic_api_key>
```

Clone the repository and launch the assistant [using the LangGraph server](https://langchain-ai.github.io/langgraph/cloud/reference/cli/#dev):
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
git clone https://github.com/langchain-ai/robo-blogger.git
cd robo-blogger
uvx --refresh --from "langgraph-cli[inmem]" --with-editable . --python 3.11 langgraph dev
```

This will open LangGraph Studio in your browser. 

### Required Input

The only required input is the name of the audio dictation file (e.g., `audio_dictation.txt` in `notes` folder). You can use any audio-to-voice dictation app (e.g., [Flowvoice](https://www.flowvoice.ai/)) to create this file. 
```
notes/audio_dictation.txt
```

![Screenshot 2024-12-16 at 4 53 37 PM](https://github.com/user-attachments/assets/de7acd1f-9ee3-49f5-8aef-26bcda8ae479)

### Optional Inputs

Two additional inputs are optional: 
1. A list of URLs to documentation that you want to use to help write the blog post.
2. A template for the blog post structure.

![Screenshot 2024-12-16 at 3 20 10 PM](https://github.com/user-attachments/assets/8903f08c-eba0-4abc-b5a6-8bd3eff8fe9a)

In the `configuration` tab, you can provide template for the blog post structure (see ## Customization below for examples).

![Screenshot 2024-12-16 at 4 45 12 PM](https://github.com/user-attachments/assets/1712c440-68c0-4655-bd5f-8078fbfa125e)

## Motivation

Blog posts typically follow a consistent structure:

1. High level overview of the topic
2. Code documentation and examples
3. Structured content walkthrough

While this structure is clear, getting from initial thoughts to a polished first draft can be challenging. Robo Blogger streamlines this process by requiring only:
- A voice recording of your initial thoughts
- Optional documentation links
- Optional blog structure

The workflow is simple:
1. **Voice Capture**: Record your thoughts using any dictation app (e.g., Flowwise)
2. **Planning**: Claude 3.5 Sonnet converts your dictation and structure into a coherent plan
3. **Writing**: Automated generation of each blog section following the plan, using your dictation and any documentation links

This approach builds on concepts from our previous [Report mAIstro](https://github.com/langchain-ai/report-mAIstro) project.

## Customization

We've found that blog posts typically follow a consistent structure. For example, we have:

* Product update: https://blog.langchain.dev/langgraph-cloud/
* Perspective: https://blog.langchain.dev/what-is-an-agent/

Templates for different types of blog posts can be passed in as a configuration option. 

### Product Update Example

URLs provided: 
* "https://langchain-ai.github.io/langgraph/concepts/", 
* "https://langchain-ai.github.io/langgraph/concepts/langgraph_platform/",
* "https://langchain-ai.github.io/langgraph/concepts/deployment_options/"

Blog structure provided: 
* [`examples/product_update/template.txt`](examples/product_update/template.txt)

Audio dictation provided: 
* [`notes/langgraph_cloud.txt`](notes/langgraph_cloud.txt)

Resulting blog post: 
* [`examples/product_update/langgraph_update.md`](examples/product_update/langgraph_update.md)

### Perspective Example

URLs provided: 
* "https://langchain-ai.github.io/langgraph/concepts/high_level/", 
* "https://langchain-ai.github.io/langgraph/concepts/agentic_concepts/",
* "https://www.deeplearning.ai/the-batch/issue-253/"

Blog structure provided: 
* [`examples/perspective/template.txt`](examples/perspective/template.txt)

Audio dictation provided: 
* [`notes/agents.txt`](notes/agents.txt)

Resulting blog post: 
* [`examples/perspective/agents.md`](examples/perspective/agents.md)
