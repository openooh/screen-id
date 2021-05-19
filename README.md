# screen-id
Proposals for how to identify screens

There are very few universal identifiers, though there are some common identifiers.

* Almost every publisher has one (or more) internal, publisher assigned ids they use to reference screens (or "places advertising can run")
* Some publishers or exchanges may identify using units other than screens (spots in loops, inventory groups, different sections of a screen)
* Some 3rd parties (e.g. GeoPath, COMMB, Route, etc.) assign IDs to screens

Some possibilities:

## 1. A format/protocol for generating non-colliding ids

This seems the most promising - though it requires a standardized id to namespace publishers

e.g. `com.publisher.screen123`

Perhaps formatted as

| Section      | Format      | Example  | Description                                                            |
| ------------ | ----------- | -------- | ---------------------------------------------------------------------- |
| Publisher ID | Reverse-TLD | com.pub  | Reverse DNS of a gTLD (similar to OpenRTB's `adomain`                                                |
| Screen ID    | String      | 12345678 | Format determined by the publisher, expected to be immutable over time - perhaps 128 character limit |

Some tradeoffs to consider:

* Perhaps "Publisher ID" could also be a rating agency - e.g. `org.geopath` instead of a specific publisher's domain, if the publisher decided that was preferable
* If we want to handle de-duplication, compliant suppliers could be required to pass along the original id (or explicitely not pass it if transparent) - perhaps consistent with the IAB Supply Chain concepts around reseller - e.g. in a way that's consistent with sellers.json, and ads.txt and that world of standards
* DNS is "nice and human readable" but does tend to change with companies marketing, branding, and M&A status... though it seems really nice not to have a central registry
* Limits would be nice - what's the max reasonable? UUID length? Something longer?

## 2. Some kind of registry

This seems... hard to maintain and undesireable - though I suppose it could just be a CSV in this repo or something else that pubs are expected to keep up to date
