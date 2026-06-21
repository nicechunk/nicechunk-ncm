# NiceChunk NCM

![NiceChunk NCM overview](docs/screenshots/overview.png)

NCM on-chain 3D asset format and local VOX converter.

## Project Overview

This repository contains the NCM asset format page and conversion tooling. NCM is a compact text representation for cuboid-based 3D assets that can be inspected, transported, and potentially stored in program-owned accounts.

The current tooling includes browser-side MagicaVoxel .vox parsing, conversion into NCM text, sample assets, and the shared voxel utility module.

The repository is split out because asset format design deserves independent iteration from gameplay pages and contract logic.

## System Principles

- Compactness matters: the format is designed around cuboids and merged boxes so 3D assets can remain small.
- Local conversion first: the browser converter parses files locally and does not require an upload service.
- Readable representation: NCM should be easier to inspect than opaque binary blobs.
- Format logic should be reusable: conversion and decoding live in shared modules that other tools can import.

## How It Works

- Open the NCM page and load a sample or local .vox file.
- Convert the source model into NCM text and inspect the resulting cuboids.
- Use the command-line converter for repeatable file conversion during asset preparation.
- Keep generated .ncm examples small enough to remain practical for repository review.

## Why This Project Matters

NiceChunk needs an asset format that fits the project's on-chain and browser-first constraints. NCM is an experiment in making voxel-like assets compact, inspectable, and portable.

A dedicated NCM repository gives asset tooling a clear home and lets other projects experiment with the format without depending on the game client.

## Repository Layout

- `ncm/`
- `src/vox/`
- `scripts/vox-to-ncm.mjs`
- `public/media/vox/`

## Development Workflow

1. Clone the repository and inspect the focused source tree before changing shared contracts or generated artifacts.
2. Keep changes scoped to the domain of this repository. Cross-domain changes should be coordinated through the matching split repositories.
3. Run the smallest meaningful validation for the touched surface: build checks for programs, browser checks for pages, or fixture checks for deterministic libraries.
4. Update screenshots and documentation when behavior, visible UI, public constants, or developer-facing workflows change.

## Future Development Direction

- Define a formal NCM specification document and compatibility versioning.
- Add validation tests for encoder and decoder round trips.
- Support additional optimization passes for cuboid merging.
- Connect NCM assets to forging, marketplace, and future on-chain metadata flows.

## Maintenance Notes

This repository is a focused split from the main NiceChunk working tree. Keep the public surface explicit: avoid committing private keys, wallet files, deployment-only scripts, machine-specific configuration, or generated build artifacts. Runtime user-facing copy should stay behind the i18n layer where the project has an i18n surface.
