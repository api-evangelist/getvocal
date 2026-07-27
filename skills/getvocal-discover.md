---
name: Discover GetVocal for AI agents
description: Load GetVocal's agent guidance and tool manifest, then summarize what it does and enumerate its products and industries — the correct first step before any GetVocal interaction.
api: openapi/getvocal-openapi-original.json
operations: [getLlmsTxt, getMcpManifest]
mcp_tools: [getvocal.get_overview, getvocal.search, getvocal.list_products, getvocal.list_industries]
---

# Discover GetVocal for AI agents

GetVocal is a public, agent-native surface. There is no API key — the site OpenAPI
declares `auth: none` and every operation is a safe GET. Discover, don't authenticate.

## Steps

1. **Read the guidance file.** Call `getLlmsTxt` (`GET /llms.txt`) to retrieve the
   site map and the "Notes for AI agents" block. This is the canonical context
   file and is referenced by both `ai-plugin.json` and the MCP manifest.
2. **Read the MCP manifest.** Call `getMcpManifest` (`GET /.well-known/mcp.json`) to
   learn the WebMCP tools the site registers in-page via `navigator.modelContext`
   (transport `webmcp`, schema_version `2025-06-18`).
3. **When running in-browser under WebMCP**, prefer the registered tools over
   scraping: `getvocal.get_overview` for a one-paragraph summary,
   `getvocal.list_products` and `getvocal.list_industries` to enumerate the
   surface, and `getvocal.search` to resolve a keyword to matching page links.

## Rules

- All calls are unauthenticated GETs — send no credentials.
- Treat `/llms.txt` as the source of truth for the site map and differentiator.
- To reach a human, do not guess endpoints — use the demo/partner links surfaced
  by the guidance file (see the book-a-demo skill).
