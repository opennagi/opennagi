# OpenNagi

> Calm the storm. Bundle AI-to-human notifications and deliver them on the receiver's terms.

**Homepage: [opennagi.com](https://opennagi.com)**

OpenNagi sits between the flood of AI-generated notifications and a human's finite attention. It takes what AI agents want to tell a person, bundles it, curates it, and delivers it in a quiet, non-intrusive form.

The name joins **open** (an open intake for any AI, any notification) and **nagi** (凪, the calm after wind and waves settle). This repo is the hub — the code lives in the repositories below.

Status: concept and MVP design. The first feature is the digest (bundle and deliver on a schedule), starting with RSS as the "first agent."

## Repositories

| Repo | Visibility | Role |
| --- | --- | --- |
| [protocol](https://github.com/opennagi/protocol) | Public | Contract layer: the intake envelope schema/types and the public SDK (sender SDK, RSS adapter). The root — depends on nothing. |
| [server](https://github.com/opennagi/server) | Private | Backend: intake (`/intake`), bundling, scheduled delivery. Depends on `protocol`. Design docs live here. |
| [app](https://github.com/opennagi/app) | Private | The receiver's mobile client (Expo / React Native). |
| [web](https://github.com/opennagi/web) | Private | The website at [opennagi.com](https://opennagi.com) (Cloudflare Workers). |

`protocol` is the root; `server` and `app` depend on it one-way.

## License

Open-core, licensed per repo. `protocol` is open source; the others are considered for release in stages.
