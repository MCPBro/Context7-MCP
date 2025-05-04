# Learning Context7 MCP: My Notes

I'm new to programming and trying to figure out how to use MCP (Model Context Protocol) with Context7. My goal is to use AI models to help me write better code by giving them up-to-date documentation.

## My Setup

I'm using VS Code Insiders and following the instructions to install [Context7 MCP](https://mcpbro.com/mcp/context7-mcp-server).

## Installation Process

I went to the Context7 README and found the section for "Install in VS Code Insiders".

It suggested clicking a badge or adding configuration to my VS Code MCP config file. I decided to go with adding the config manually to understand it better.

I opened my VS Code settings and searched for "MCP". I found the setting for "Model Context Protocol: Servers" and clicked "Edit in settings.json".

Then I copied the configuration block:

```json
{
  "servers": {
    "Context7": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

I pasted this into my `settings.json` file inside the `chat.experimental.mcp.servers` object. It looked something like this after I added it:

```json
{
    // other settings
    "chat.experimental.mcp.servers": {
        "Context7": {
          "type": "stdio",
          "command": "npx",
          "args": ["-y", "@upstash/context7-mcp@latest"]
        }
    }
    // other settings
}
```

I saved the `settings.json` file.

## Trying it Out

The README said to add `use context7` to my prompt.

I opened a Chat panel in VS Code and typed a simple prompt:

`Create a basic Node.js script to read a file. use context7`

I sent the prompt.

The AI model started generating code. I could see it was providing comments that looked like they were referencing external documentation, which I assumed was coming from Context7. The generated code seemed reasonable for reading a file in Node.js.

## Encountering an Issue

After trying a few times, I noticed that sometimes the MCP server seemed to take a while to respond, or the AI would generate code without mentioning Context7 at all. I wasn't sure if the server was running correctly or if I was using it right.

I remembered the README mentioned a troubleshooting section. I looked through it. It had suggestions like checking Node version, trying `bunx` or `deno`, and removing `@latest`.

My Node.js version is v18 or higher, so that wasn't the issue. I wasn't using Bun or Deno, just `npx` as in the example.

One suggestion was to try removing `@latest`. I went back to my `settings.json` and changed the `args` line:

```json
"args": ["-y", "@upstash/context7-mcp"] // Removed @latest
```

I saved the file and tried the same prompt again.

It seemed to work, and the responses felt more consistent. I'm not entirely sure why removing `@latest` helped, but it seemed to make the MCP server more reliable for me. Maybe there was a temporary issue with the very latest version.

## Notes on Tools

The README lists some available tools:

- `resolve-library-id`: Seems useful for figuring out the correct ID for a library if the AI isn't sure.
- `get-library-docs`: This is the main tool to get documentation. It takes a library ID and optional topic and token count.

I haven't specifically tried using these tools directly in a prompt yet, but I understand that the AI uses them when I include `use context7`.

## Summary

So far, I have successfully installed Context7 MCP in VS Code by adding the configuration to my `settings.json`. I learned that I need to add `use context7` to my prompts for the AI to use the MCP server. I had a small issue with the `@latest` tag which I fixed by removing it based on the troubleshooting section. I can see that Context7 seems to be providing documentation to the AI, which helps it generate more relevant code. I still need to explore the available tools more and understand how to best phrase prompts to get the most out of Context7.
