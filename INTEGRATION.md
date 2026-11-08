<!-- forevenza-managed-integration/1 -->
# Nodehour

Nodehour sources GPU and accelerator capacity. Describe the run or the fleet; Nodehour sizes the cluster in arithmetic you can check, takes that one requirement to providers that can run it, and brings back options and quotations side by side to choose from and accept.

Operated by Forevenza.

- [Canonical website](https://nodehour.forevenza.com/)
- [Current OpenAPI description](https://nodehour.forevenza.com/openapi.json)
- MCP endpoint: https://nodehour.forevenza.com/mcp
- Business contact: hello@nodehour.forevenza.com

## Connect an MCP client

Use the remote Streamable HTTP endpoint in an MCP client that supports it. Clients that use a mcpServers configuration can start with:

```json
{
  "mcpServers": {
    "nodehour": {
      "type": "http",
      "url": "https://nodehour.forevenza.com/mcp"
    }
  }
}
```

Inspect the live tools before choosing an operation:

```sh
node examples/discover-mcp.mjs
```

This Node.js 20+ example initializes the connection and reads every page of tools/list. It prints each current tool's description, input schema and action annotations; it never invokes a tool or submits a customer request. If discovery fails, it reports an error rather than implying the operation is available. Review the operation's inputs and terms before calling it.

## Discover the current HTTP interface

The published OpenAPI description is the source of truth for HTTP operations, inputs and any authentication requirements. This repository contains integration documentation and client examples, not the server implementation. It does not promise that every operation is free or that a service request has been accepted. Follow the service's current terms before sending business information or creating a request.

```sh
curl --fail --silent --show-error 'https://nodehour.forevenza.com/openapi.json'
```

Run `node examples/discover.mjs` with Node.js 20 or later to list the current documented HTTP operations. It only reads the public specification and does not submit a customer request.
