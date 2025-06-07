# AI Discovery Meta Tag Standard

## 1. Purpose of the Standard

The purpose of the **ai-discovery** meta tag standard is to establish a convention for indicating the presence or absence of AI Agent-compatible content and services on a website. This standard enables AI agents, bots, and web crawlers to:

* Discover MCP (Machine-Consumable Page) services
* Identify A2A (Agent-to-Agent) compatible services
* Recognize AI-targeted consumable content
* Respect site instructions to **avoid** AI-based processing

The metadata is intended to complement `.well-known/ai_discovery.json` as a structured and central discovery endpoint.

---

## 2. Naming Convention

* **Prefix:** `ai-discovery:`
* **Attribute Type:** `name`
* **Versioning:** Managed via the `.well-known/ai_discovery.json` file

---

## 3. Meta Tag Definitions

### a. `ai-discovery:mcp`

* **Attribute Type:** `name`
* **Expected Value Format:** None (presence-only)
* **Description:** Indicates that the application or site provides MCP-compatible tools or services. Discovery details are listed in `.well-known/ai_discovery.json`.
* **Use Case:** Signals to bots and AI agents that MCP services are available.
* **Required:** Situational — used only when MCP services are present and documented in the well-known file.
* **Example:**

  ```html
  <meta name="ai-discovery:mcp">
  ```

### b. `ai-discovery:a2a`

* **Attribute Type:** `name`
* **Expected Value Format:** None (presence-only)
* **Description:** Indicates that the application or site supports A2A communication with agents. Details are listed in `.well-known/ai_discovery.json`.
* **Use Case:** Signals the availability of A2A-compatible services.
* **Required:** Situational — used when A2A services are available.
* **Example:**

  ```html
  <meta name="ai-discovery:a2a">
  ```

### c. `ai-discovery:content`

* **Attribute Type:** `name`
* **Expected Value Format:** None (presence-only)
* **Description:** Indicates that the document contains AI-consumable content.
* **Use Case:** Enables bots and AI tools to prioritize indexing or analysis.
* **Required:** Optional
* **Example:**

  ```html
  <meta name="ai-discovery:content">
  ```

### d. `ai-discovery:ignore`

* **Attribute Type:** `name`
* **Expected Value Format:** None (presence-only)
* **Description:** Explicitly indicates that AI agents should **not** process the content of the document.
* **Use Case:** Signals opt-out of AI processing (similar to `robots.txt` disallow rules).
* **Required:** Situational — mutually exclusive with the other `ai-discovery` tags.
* **Example:**

  ```html
  <meta name="ai-discovery:ignore">
  ```

---

## 4. Versioning

The ai-discovery standard version is declared and documented inside the `.well-known/ai_discovery.json` file, not in the HTML meta tags themselves.

---

## 5. Target Audience

* Public websites
* Developers building AI-aware web platforms
* AI agents, bots, crawlers
* AI service discovery systems

---

## 6. Compliance Requirements

* Pages should include one or more of the following **if relevant**:

  * `ai-discovery:mcp`
  * `ai-discovery:a2a`
  * `ai-discovery:content`
* If the page **should be ignored by AI**, include:

  * `ai-discovery:ignore`
* Do not combine `ai-discovery:ignore` with any other ai-discovery tag.

---

## 7. Hosting and Discovery

The standard requires a JSON file hosted at:

```
/.well-known/ai_discovery.json
```

### JSON Schema (Version 1.0.0)

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "AI Discovery Schema",
  "description": "Defines the structure for AI discovery data",
  "version": "1.0.0",
  "type": "object",
  "properties": {
    "version": {
      "type": "string",
      "description": "The version of the schema"
    },
    "description": {
      "type": "string",
      "description": "A description of the AI discovery data"
    },
    "mcpServices": {
      "type": "array",
      "items": {
        "$ref": "#/$defs/mcpService"
      }
    },
    "a2aServices": {
      "type": "array",
      "items": {
        "$ref": "#/$defs/a2aService"
      }
    }
  },
  "$defs": {
    "mcpService": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string",
          "description": "The name of the mcp service"
        },
        "url": {
          "type": "string",
          "description": "The url of the mcp service"
        },
        "description": {
          "type": "string",
          "description": "A description of the mcp service"
        },
        "tools": {
          "type": "array",
          "items": {
            "type": "string",
            "description": "A tool provided by the mcp service"
          }
        }
      },
      "required": ["name", "url"],
      "additionalProperties": false
    },
    "a2aService": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string",
          "description": "The name of the a2a service"
        },
        "url": {
          "type": "string",
          "description": "The url of the mcp service"
        },
        "card": {
          "type": "string",
          "description": "The service endpoint url of A2A service's /.well-known/agent.json file."
        },
        "description": {
          "type": "string",
          "description": "A description of the A2A service"
        }
      },
      "required": ["name", "url", "card"],
      "additionalProperties": false
    }
  },
  "required": ["version"],
  "additionalProperties": false
}
```

---

## 8. Publication

The official specification and updates will be hosted at:

```
https://github.com/1155project/ai_discovery_specification
```

---

*End of AI Discovery Meta Tag Specification (v1.0)*
