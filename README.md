# screen-id
Proposals for how to identify screens

There are very few universal identifiers, though there are some common identifiers.

* Almost every publisher has one (or more) internal, publisher assigned ids they use to reference screens (or "places advertising can run")
* Some publishers or exchanges may identify using units other than screens (spots in loops, inventory groups, different sections of a screen)
* Some 3rd parties (e.g. GeoPath, COMMB, Route, etc.) assign IDs to screens

Some possibilities:

## 1. A format/protocol for generating non-colliding ids

This seems the most promising - though it requires a standardized id or to namespace on something to allow independence

### 1a. Publisher-Namespaced IDs

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

### 1b. Universal IDs

Alternatively, we could try to come up with a universal scheme - though as opposed to many scenarios where the only thing you care about is non-collisions (e.g. UUIDs, other GUID schemes) in our case [Conflation](https://en.wikipedia.org/wiki/Conflation) is an important case (e.g. "de-duplication" of screen identifiers, especially for the purpose of joining information.

One interesting tangential spec is: [PlaceKey](https://www.placekey.io/). In particular, their format (built on Uber's H3) has a notion of geo-spatial locations baked in, which is a possible case for conflation.

![Placekey Structure](https://assets.website-files.com/5f277eb85e5f02d500828d71/5f5034a9ec19138658daa4b0_placekey_explained.png)!

Benefits:

* Geospatial could greatly help with the problem of conflation
* Geospatial is a powerful key to join data to

Problems:

* Moving assets (already a hard problem) are also a hard-problem in this case. While it's possible we could handle that definitionally (e.g. instead of providing a "screen identifier" maybe buyers / DSPs are generally more interested in "where did people see an ad" in which case geographic keys seem very interesting

## 2. A format/protocol for exchanging IDs

How do we pass this? Another OpenRTB extension, with perhaps some names if serialized? e.g.

```jsonc

"ext"{
  "dooh": {
    "screen-id": "com.pub:12345678".
    "aliases": { //optional
      "billing": "id456",
      "internal": "abc123"
    }
  }
}

```

Alternatively - re-use an existing field by convention (`tagid` might be attractive) - perhaps also some kind of URL mapping scheme/recommendation

Do we want to go further and do discovery? e.g. pub.com/screen/12345678 should have human or machine readable information would be... really cool....

## 2. Some kind of registry

This seems... hard to maintain and undesireable - though I suppose it could just be a CSV in this repo or something else that pubs are expected to keep up to date
