<h1 align="center">AI Discovery Meta Specification</h1>

<p align="center">
  <img src="public/ai_discovery_logo_w.png" alt="AI Discovery Logo" width="600">
</p>
A standardized approach for websites to declare AI Agent-compatible content and services through HTML meta tags and structured discovery endpoints.

## Overview

The **AI Discovery Meta Specification** establishes a convention for websites to indicate the presence or absence of AI Agent-compatible content and services. This enables AI agents, bots, and web crawlers to efficiently discover and interact with:

- **MCP (Machine-Consumable Page) services** - Standardized tools and APIs for AI agents
- **A2A (Agent-to-Agent) compatible services** - Direct agent communication protocols  
- **AI-targeted consumable content** - Content optimized for AI processing
- **Opt-out preferences** - Sites that explicitly avoid AI-based processing

## Key Features

- **🏷️ HTML Meta Tags** - Simple presence-based tags using the `ai-discovery:` prefix
- **📋 Structured Discovery** - Centralized `.well-known/ai_discovery.json` endpoint
- **🔍 Service Discovery** - Automatic identification of MCP and A2A services
- **🚫 Respectful Processing** - Built-in opt-out mechanism for privacy-conscious sites
- **📝 JSON Schema Validation** - Well-defined structure for discovery data

## Quick Start

### 1. Add Meta Tags to Your HTML

```html
<!-- For sites providing MCP services -->
<meta name="ai-discovery:mcp">

<!-- For sites supporting Agent-to-Agent communication -->
<meta name="ai-discovery:a2a">

<!-- For pages with AI-consumable content -->
<meta name="ai-discovery:content">

<!-- For pages that should be ignored by AI (mutually exclusive) -->
<meta name="ai-discovery:ignore">
```

### 2. Create Discovery Endpoint

Host a JSON file at `/.well-known/ai_discovery.json`:

```json
{
  "version": "1.0.0",
  "description": "AI services and content discovery for example.com",
  "mcpServices": [
    {
      "name": "Weather Service",
      "url": "https://example.com/api/mcp/weather",
      "description": "Provides weather data and forecasts",
      "tools": ["get_weather", "get_forecast"]
    }
  ],
  "a2aServices": [
    {
      "name": "Customer Support Agent",
      "url": "https://example.com/api/a2a/support",
      "card": "https://example.com/.well-known/agent.json",
      "description": "AI agent for customer support interactions"
    }
  ]
}
```

## Meta Tag Reference

| Tag | Purpose | Usage |
|-----|---------|-------|
| `ai-discovery:mcp` | Indicates MCP services available | Include when hosting MCP-compatible tools |
| `ai-discovery:a2a` | Indicates A2A communication support | Include when supporting agent-to-agent protocols |
| `ai-discovery:content` | Marks AI-consumable content | Include on pages optimized for AI processing |
| `ai-discovery:ignore` | Opts out of AI processing | Include to prevent AI analysis (exclusive) |

## Implementation Examples

### Web Application with MCP Services

```html
<!DOCTYPE html>
<html>
<head>
    <meta name="ai-discovery:mcp">
    <meta name="ai-discovery:content">
    <title>My AI-Enabled App</title>
</head>
<body>
    <!-- Your content here -->
</body>
</html>
```

### Privacy-Focused Site

```html
<!DOCTYPE html>
<html>
<head>
    <meta name="ai-discovery:ignore">
    <title>Private Content</title>
</head>
<body>
    <!-- AI agents will respect this opt-out -->
</body>
</html>
```

## Specification Documents

- **[Full Specification](spec/ai_discovery_meta_specification.md)** - Complete technical specification
- **[JSON Schema](spec/well_known_ai_discovery_schema.json)** - Schema for `.well-known/ai_discovery.json`

## Target Audience

- **Website Developers** - Implementing AI discovery on public websites
- **AI Platform Builders** - Creating AI-aware web platforms and services
- **Bot/Crawler Developers** - Building AI agents that discover and consume web services
- **Service Discovery Systems** - Implementing automated AI service discovery

## Benefits

### For Website Owners
- **Increased Discoverability** - AI agents can find and utilize your services
- **Respectful Processing** - Clear opt-out mechanisms protect privacy
- **Standardized Approach** - Industry-standard way to declare AI compatibility

### For AI Developers  
- **Efficient Discovery** - Quickly identify compatible services and content
- **Structured Data** - Well-defined JSON schema for programmatic access
- **Respect Boundaries** - Honor site preferences for AI processing

## Version

Current specification version: **1.0.0**

Version information is managed through the `.well-known/ai_discovery.json` file, not in HTML meta tags.

## License

This specification is released under the [MIT License](LICENSE).

## Contributing

We welcome contributions to improve and extend this specification. Please see our repository for contribution guidelines and submit issues or pull requests.

## Repository

**Official Specification**: https://github.com/1155project/ai_discovery_specification

---

*AI Discovery Meta Specification v1.0 - Enabling respectful and efficient AI-web interactions*
