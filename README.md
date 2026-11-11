# Warehouse Management

The common warehouse vocabulary -- the warehouses and the bin locations inside them, the inbound receipts (ASNs) that bring stock in and the pick lists that send it out -- distilled from the APIs that already exist. Stock levels belong to commerce, outbound shipments to shipping. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Warehouse Management, WMS, 3PL, Fulfillment, Inventory Management, Warehousing, Order Fulfillment in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| warehouse | 11 | 10 | name 80%, id 70%, address 60% | warehouses 8, facilities 2, warehouse 1 |
| inbound_receipt | 4 | 4 | status 100% | receiving 2, asns 1, inbound-shipments 1 |

Cohort: 75 providers with harvested OpenAPI, 13 crosswalks. Of the providers exposing a warehouse: 55% create, 91% list, 36% fetch, 46% update, 27% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A warehouse agrees on name, id and address across WMS, 3PL and inventory platforms. Everything that happens inside it -- bins, receiving, picking -- is barely published: inbound receipts at 4 providers (agreeing on a status), bins and pick lists at 2 or fewer.
- 3PLs expose the receiving workflow (ShipBob, ShipMonk) without exposing the warehouse; a warehouse is the customer's view, receiving is the operator's.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Facilities, fulfillment centers and distribution centers are warehouses.
- ASNs, inbound shipments and receivings are inbound receipts (`/inbound-receipts`) -- the concept procurement measured and dropped as goods receipts.
- Stock levels are commerce's inventory; outbound shipments are shipping's.
- Bins and pick lists were measured and dropped.
- Duplicates merged: 3PL Central into Extensiv.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
