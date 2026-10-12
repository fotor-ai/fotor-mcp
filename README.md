<p align="center">
  <img src="assets/logo.svg" alt="Fotor logo" width="112">
  <br>
  <strong>Fotor MCP</strong>
</p>

<h1 align="center">Power Your AI Agent with Fotor</h1>

<p align="center">
  Generate images, edit photos, and create videos through natural language.
</p>

<p align="center">
  <a href="#quick-start">Quick start</a> &nbsp;·&nbsp;
  <a href="#what-you-can-create">Capabilities</a> &nbsp;·&nbsp;
  <a href="#try-it">Example prompts</a> &nbsp;·&nbsp;
  <a href="docs/troubleshooting.md">Troubleshooting</a>
</p>

---

Connect Fotor to **Codex** or **Claude Code** and turn a creative brief into images and videos from your conversation. Describe the result you want: your agent can choose a model, prepare the request, and bring back the result link. Fotor handles the generation and image processing.

Use one connection to generate and edit images, remove backgrounds, upscale photos, and create videos. Sign in with your Fotor account through OAuth; the service is hosted, with no local server or manual Fotor API key setup required.

## What you can create

| Goal | Use Fotor through your agent to… |
| --- | --- |
| Social media visuals | Create post images and campaign concepts from a written brief. |
| Product imagery | Remove a photo's background, request a new setting, or upscale an existing image. |
| Illustrations and concept art | Explore a visual direction, then refine it using image references and follow-up prompts. |
| Short videos | Describe a scene or animate a still image with a motion prompt. |
| Video with references | Guide generation with first and last frames, or supported image, video, and audio references. |

**Models include:** GPT Image 2 · Gemini 2.5 Flash Image · Seedance 2.0.

Let your agent choose a model suited to the task, or name one in your prompt. Available models, settings, and reference types vary; your agent can check them before submitting.

## Quick start

You'll need a **Fotor account** and an **AI agent with remote MCP and OAuth support**, such as Codex or Claude Code. Generation and image processing can consume Fotor credits. Ask your agent to check your balance before creating.

Connect to the hosted MCP endpoint:

```text
https://mcp.fotor.com/mcp
```

**Transport:** Streamable HTTP · **Authentication:** OAuth with your Fotor account.

Follow the connection steps for [Codex](#codex), [Claude Code](#claude-code), or [other agents](#other-agents).

### Codex

**1. Add Fotor MCP.** Run this in your terminal:

```bash
codex mcp add fotor-mcp --url https://mcp.fotor.com/mcp --oauth-resource https://mcp.fotor.com/mcp
```

**2. Sign in.** Run:

```bash
codex mcp login fotor-mcp
```

Complete the Fotor sign-in and authorization flow in your browser, then return to your terminal.

**3. Check the connection.** Start Codex and use `/mcp` to inspect the server. Then continue with [Verify your connection](#verify-your-connection) below.

See the [official Codex MCP documentation](https://learn.chatgpt.com/docs/extend/mcp?surface=cli) for configuration details.

### Claude Code

**1. Add Fotor MCP.** Run this in your terminal:

```bash
claude mcp add --transport http --scope user fotor-mcp https://mcp.fotor.com/mcp
```

This adds the connection for your user account across projects.

**2. Sign in.** Start Claude Code, enter `/mcp`, select `fotor-mcp`, and follow the authentication prompt. Complete Fotor sign-in and authorization in your browser.

**3. Check the connection.** Return to Claude Code and inspect the server in `/mcp`. Then continue with [Verify your connection](#verify-your-connection) below.

See the [official Claude Code MCP documentation](https://code.claude.com/docs/en/mcp) for configuration details.

### Other agents

For other agents, use a remote MCP connection with **Streamable HTTP** and **OAuth** support. The setting names and configuration format depend on the agent.

1. Open the agent's MCP server or connector settings and add a remote server.
2. Name the connection **Fotor MCP** and enter the server URL shown above. Select **Streamable HTTP** if a transport option is required.
3. Connect and follow the **OAuth** authorization flow. Sign in to your Fotor account in the browser and approve access.
4. Return to the agent, confirm that the connection is active, and enable the Fotor tools you want to use. Continue with [Verify your connection](#verify-your-connection).

If your agent uses a configuration file, use its documented format for a remote server URL and OAuth authentication. No manual Fotor API key is needed.

### Verify your connection

Ask your agent:

> Use Fotor to check my available credits.

A returned balance confirms that the agent can call an authenticated Fotor tool. If balance information is unavailable for your account, follow the [credit troubleshooting steps](docs/troubleshooting.md#credits-and-plans).

## Try it

### Create your first image

Start with a brief that needs no reference upload:

> Use Fotor to create a square social media image for a neighborhood coffee shop. Show a ceramic cup of coffee on a wooden table, warm morning light, and a cozy atmosphere. Leave room at the top for a headline. Choose an available image model and give me the result link when it is ready.

Then use the result as a reference for another version:

> Use that image as a reference. Create a second version with cooler light and more space around the cup.

### Prepare a product image

> Use Fotor to remove the background from this product photo and return a transparent image.

For a larger version of an existing image:

> Use Fotor to upscale this image by 2×.

Provide a file your agent can read or an accessible HTTPS media URL. Your agent needs to upload local files before using them with Fotor.

### Turn an idea or image into video

> Use Fotor to create a short 16:9 video of steam rising from a coffee cup, with a slow camera push-in. Choose a supported video model and duration.

Or continue from an image you already have:

> Use this image as the first frame of a 16:9 Fotor video. Add gentle movement to the steam and a slow camera push-in.

Your agent submits the request, checks its progress, and shares the result link when it is ready. If a task is still processing, you can ask for its status later using the task ID. Save the outputs you want to keep; result links are not guaranteed to remain available permanently.

## FAQ

### Why can't I connect or sign in?

Check the server URL, agent version, and browser authorization flow. Follow [connection and sign-in troubleshooting](docs/troubleshooting.md#connection-and-sign-in) if the problem continues.

### Why are Fotor tools missing after I connect?

Check the server's status and tool permissions in your agent. See [tools not appearing](docs/troubleshooting.md#tools-not-appearing) for the next steps.

### What if I don't have enough credits?

Ask your agent to check your current balance. See [credit troubleshooting](docs/troubleshooting.md#credits-and-plans) for account and balance issues.

### Why did I receive a task ID instead of an image or video?

The request was submitted for processing. Ask your agent to check that task ID for the result. See [task status and results](docs/troubleshooting.md#task-status-and-results), including what to do after a timeout.

## Help and links

- **MCP connection issues, tool problems, and feature requests:** [GitHub Issues](https://github.com/fotor-ai/fotor-mcp/issues). Include the details listed in [reporting an issue](docs/troubleshooting.md#reporting-an-issue).
- **Account, payment, and order questions:** [Fotor Help Center](https://support.fotor.com/hc/en-us).
- **Fotor:** [Website](https://www.fotor.com/) · [Privacy Policy](https://www.fotor.com/privacypolicy) · [Terms of Service](https://www.fotor.com/termsofservice).

## License

Repository content is provided under the [MIT License](LICENSE). Use of the hosted Fotor service is governed by Fotor's Terms of Service.
