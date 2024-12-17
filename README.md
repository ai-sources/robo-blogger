# Robo Blogger

Robo Blogger is an assistant that transforms voice recordings into polished blog posts, making content creation effortless and efficient.

## Quickstart

Set API keys for the LLM of choice (default is Anthropic Claude 3.5 Sonnet):
```
export ANTHROPIC_API_KEY=<your_anthropic_api_key>
```

Clone the repository and launch the assistant [with the LangGraph server](https://langchain-ai.github.io/langgraph/cloud/reference/cli/#dev):
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
git clone https://github.com/langchain-ai/robo_blogger.git
cd robo_blogger
uvx --refresh --from "langgraph-cli[inmem]" --with-editable . --python 3.11 langgraph dev
```

You should see the following output and Studio will open in your browser:

- 🚀 API: http://127.0.0.1:2024
- 🎨 Studio UI: https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
- 📚 API Docs: http://127.0.0.1:2024/docs

Use a dictation app (e.g., [Flowwise](https://www.flowvoice.ai/)) to dictate some high level notes about the blog post you want to write:

* Save your dictation to a file in the `notes` folder (e.g., `blog_notes.txt`). 
* For example, with Flowwise in Cursor, you can simply hold down the `fn` key (on Mac) and dictate your notes.

In Studio inputs: 
* Provide the name of the dictation file (e.g., `blog_notes.txt`) in the `configuration` tab.
* Optionally, provide any links to documentation that you want to use to write the blog post.

![Screenshot 2024-12-13 at 4 15 06 PM](https://github.com/user-attachments/assets/db32bce7-9784-4315-8a41-c2d89abff6f2)

In the `configuration` tab, you can optionally customize the blog post structure (the default is in configuration.py).

## Motivation

LangChain blog posts typically follow a consistent structure:

1. High level overview of the topic
2. Code documentation and examples
3. Structured content walkthrough

While this structure is clear, getting from initial thoughts to a polished first draft can be challenging. Robo Blogger streamlines this process by requiring only:
- A voice recording of your initial thoughts
- Optional documentation links
- Optional custom blog structure

The workflow is simple:
1. **Voice Capture**: Record your thoughts using any dictation app (e.g., Flowwise)
2. **Planning**: Claude 3.5 Sonnet converts your dictation, links, and structure into a coherent plan
3. **Writing**: Automated generation of each blog section following the plan

This approach builds on concepts from our previous [Report mAIstro](https://github.com/langchain-ai/report-mAIstro) project.

## Customization

We have a few different types of blog posts:

* Product update: https://blog.langchain.dev/langgraph-cloud/
* Perspective: https://blog.langchain.dev/what-is-an-agent/

Templates for different types of blog posts can be passed in as a configuration option. 

### Product Update Example

URLs provided: 
* "https://langchain-ai.github.io/langgraph/concepts/", 
* "https://langchain-ai.github.io/langgraph/concepts/langgraph_platform/",
* "https://langchain-ai.github.io/langgraph/concepts/deployment_options/"

Blog structure provided: 
* examples/product_update/template.txt

Audio dictation provided: 
* notes/langgraph_cloud.txt

Resulting blog post: 
* examples/product_update/langgrah_update.md

### Perspective Example

URLs provided: 
* "https://langchain-ai.github.io/langgraph/concepts/high_level/", 
* "https://langchain-ai.github.io/langgraph/concepts/agentic_concepts/",
* "https://www.deeplearning.ai/the-batch/issue-253/"

Blog structure provided: 
* examples/perspective/template.txt

Audio dictation provided: 
* notes/agents.txt

Resulting blog post: 
* examples/perspective/agents.md
