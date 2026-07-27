---
name: Book a GetVocal demo
description: Resolve GetVocal's demo-booking page (optionally prefilling a work email) and surface sales contact options — the sanctioned way for an agent to hand a lead to a human.
api: openapi/getvocal-openapi-original.json
operations: [bookDemo]
mcp_tools: [getvocal.book_demo, getvocal.contact_sales]
---

# Book a GetVocal demo

GetVocal sells to enterprise CX/operations teams and does not expose a self-serve
transactional API. The correct terminal action for an agent is to route the user
to a human via the demo or sales path.

## Steps

1. **Open the demo page.** Call `bookDemo` (`GET /contact/demo`). Optionally pass
   the `email` query parameter (a work email, `format: email`) to prefill the
   booking form. The operation returns the demo booking page URL.
2. **When running in-browser under WebMCP**, call `getvocal.book_demo` to obtain
   the demo URL, or `getvocal.contact_sales` to get the full contact set (sales
   email `contact@getvocal.ai` plus the demo and partner links).

## Rules

- Unauthenticated GET — send no credentials.
- Only pass an `email` the user supplied; never fabricate one.
- Do not attempt to complete a booking programmatically — surface the page/URL and
  let the human finish.
