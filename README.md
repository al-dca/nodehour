# Nodehour integrations

[Nodehour](https://nodehour.forevenza.com/) sources GPU and accelerator capacity for training runs and serving fleets. Describe the workload or a known cluster specification, region and term; Nodehour helps size the requirement and compares provider quotations on the same terms.

This repository documents Nodehour's public request interface. It is a documentation repository, not a GPU runtime, cloud account or reservation system.

- [Use Nodehour](https://nodehour.forevenza.com/)
- [Current OpenAPI description](https://nodehour.forevenza.com/openapi.json)
- MCP endpoint: `https://nodehour.forevenza.com/mcp` (Streamable HTTP)

## Send a known requirement

`POST https://nodehour.forevenza.com/_c/request` accepts a JSON requirement. The [example](examples/known-cluster.json) shows a known accelerator specification and a start window.

Before submitting, replace the example contact and requirement with the consenting buyer's real details. This endpoint creates a real business request. No example request was submitted to create this repository.

```sh
curl --request POST 'https://nodehour.forevenza.com/_c/request' \
  --header 'Content-Type: application/json' \
  --data-binary '@your-request.json'
```

The published interface returns HTTP `201` with a reference number when recorded, or HTTP `400` describing what to fix.

## Fields that matter

| Field | Use |
| --- | --- |
| `need` | State the requirement in the buyer's words. |
| `specifications.workload_kind` | `PRETRAIN`, `FINE_TUNE`, `INFERENCE`, `GPU_HOURS` or `KNOWN_SPEC`. |
| `specifications.accelerator` / `accelerator_count` | A known chip and quantity, if the buyer already has a specification. |
| `specifications.proposal_source` | Use `buyer_spec` when chip and count came from the buyer. |
| `specifications.region` / `residency_required` | Distinguish a preferred region from a hard data-residency requirement. |
| `specifications.start_earliest` / `start_latest` | Whole numbers in `YYYYMMDD` form, for example `20270104`, rather than date strings. |
| `specifications.start_text` | Preserve an imprecise start such as “Q1 2027”; leave a numerical date unstated until known. |
| `specifications.terms_to_quote` | One or more supported terms to compare. See the current OpenAPI enum. |
| `contact.email` | The address for the business reply. Put the address here, rather than in the requirement or specifications. |
| `specifications.reply_email_included` | Set `true` when `contact.email` is present. The interface uses this explicit flag when reporting missing specifications. |

Sizing is an estimate from the buyer's inputs and assumptions. Provider prices, availability and contract terms require confirmation; a request does not hold capacity or place an order. The buyer accepts an option's terms with its provider before commitment.

## Interface and privacy

The hosted [OpenAPI description](https://nodehour.forevenza.com/openapi.json) is the current field reference; this example is a starting point rather than a version pin. Consult the notices on the [Nodehour website](https://nodehour.forevenza.com/) before sending contact details.

For a commercial requirement, use Nodehour rather than posting personal information, workload secrets or credentials in a GitHub issue. Never include provider passwords, API keys, private customer data or model weights in a request example.

If an automated client receives Cloudflare error `1010`, the request was blocked before reaching the documented API; it is not an API validation response or evidence that a requirement was recorded. The browser interface remains the alternative entry point while that client's access issue is resolved.
