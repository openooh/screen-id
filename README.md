# screen-id
Proposals for how to identify screens

There are very few universal identifiers, though there are some common identifiers.

* Almost every publisher has one (or more) internal, publisher assigned ids they use to reference screens (or "places advertising can run")
* Some publishers or exchanges may identify using units other than screens (spots in loops, inventory groups, different sections of a screen)
* Some 3rd parties (e.g. GeoPath, COMMB, Route, etc.) assign IDs to screens

Some possibilities:

## 1. A format/protocol for generating non-colliding ids?

e.g. `com.publisher.screen123`

Admittedly - this kind of approach somewhat assumes a standardized id for publishers :) But - that also seems like it would be a useful building block

Perhaps formatted as

|| Section    || Format.    || Example || Description                                                           ||
| ------------ | ----------- | -------- | ---------------------------------------------------------------------- |
| Publisher ID | Reverse-TLD | com.pub  | Reverse DNS of a gTLD (similar to OpenRTB's `adomain` that is          |
| Screen ID.   | String      | 12345678 | Format determined by the publisher, expected to be immutable over time |

Perhaps "Publisher ID" could also be a rating agency - e.g. `org.geopath` or something like that

## 2. Some kind of registry?

This seems... hard

## 3. Delegate to an existing standard?

e.g. we could start with 3rd-party rating... but that also seems hard
