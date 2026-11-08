<p align="center">
  <img src="https://img.shields.io/badge/MCP%20Dock-catalog%20releases-0a7c8a?style=for-the-badge" alt="MCP Dock Catalog Releases">
</p>

# MCP Dock Catalog Releases

![Signed](https://img.shields.io/badge/signature-Ed25519-success)
![Checksums](https://img.shields.io/badge/checksums-SHA--256-success)
![Generated](https://img.shields.io/badge/content-generated%20only-informational)
![License](https://img.shields.io/badge/license-proprietary-critical)

Signed releases of the server catalog of **MCP Dock**, the Windows app that adds, protects and watches MCP servers in AI apps such as Claude Desktop and Cursor.

This repository holds only the generated catalog files. The MCP Dock app downloads them from here, checks the signature and the checksums, and shows the servers to its users. The sources of the catalog are maintained privately.

> [!NOTE]
> Nothing here needs to be downloaded by hand. MCP Dock does it itself: **Settings → Server catalog → Refresh catalog**.

## How the app uses it

The app reads the files in `dist/` from:

```txt
https://raw.githubusercontent.com/OmniAI-Stack/MCP-Dock-Catalog-Releases/main/dist
```

1. It downloads `manifest.json` and `manifest.sig`.
2. It checks the Ed25519 signature of `manifest.json` with the public key built into the app. A catalog with a missing or wrong signature is refused.
3. It downloads the other files and checks the SHA-256 checksum of each one against the manifest.
4. It keeps the verified copy on disk and uses it until a newer signed catalog is available.

Because of the signature, a changed file in this repository, or on the way to the user, is detected and refused. Only the maintainers who hold the private key can publish a catalog the app accepts. The key is never stored in any repository.

## Layout

```txt
dist/
├── manifest.json        version, schema, minimum app version, checksums
├── manifest.sig         Ed25519 signature of manifest.json
├── index.json           list of servers (English)
├── index.<lang>.json    list of servers in cs, de, es, fr, pt
├── servers/<id>.json    install settings and texts of one server
├── categories.json      categories
├── tags.json            tags
├── publishers.json      publishers
└── notices.json         notices shown in the app
```

The files are generated and signed. They are never edited by hand, and a hand-made change would break the signature.

## Versions

A catalog version is a date and a counter, `YYYY.MM.DD.N` (for example `2026.11.07.3`), and it is written in `dist/manifest.json`. Each published version is one commit named `Catalog <version>`, so the history of this repository is the history of the catalog.

## Suggest a server

Do you know an MCP server that should be in the catalog? Open an issue with the **Suggest a server** form. Every server is checked by hand before it is listed, so it can take a while. Never paste an API key, a token or a password into an issue.

## License

Proprietary. Copyright (c) 2026 OmniAI-Stack. All rights reserved. The files are public so that the MCP Dock app can download them, but they may not be copied, mirrored or reused. The listed MCP servers belong to their publishers and have their own licenses. See [LICENSE](LICENSE).
