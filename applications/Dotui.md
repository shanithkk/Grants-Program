# Dotui

- **Team Name:** Shanith K K
- **Payment Details:**
  - **DOT**: 121ycppiucKXVWKjE1NGWjDBk5fADCGC3NrPoV1FSrAbxhb1
  - **Payment**: 1FT2JUZ7ifyG6Wxt1Nuu9PYVoaV3iT4qnA (BTC)
- **[Level](https://grants.web3.foundation/docs/Introduction/levels):** 1

## Project Overview :page_facing_up:

### Overview

Dotui is a terminal-native explorer and lightweight wallet for Polkadot SDK chains. It combines a live block explorer with a local-signing transfer workflow in a keyboard-first TUI (terminal user interface), making it easier to inspect chain activity and perform simple transfers without depending on a browser extension or a hosted service.

The initial target networks are Polkadot, Kusama, and Westend, with support for custom WebSocket RPC endpoints for other Substrate-compatible chains. Dotui will connect directly to nodes using `subxt`, render the interface with `ratatui`, and keep private keys on the local machine using `sp-core`-based signing flows.

The project is aimed at developers, node operators, power users, and anyone who prefers terminal-first workflows, including remote and SSH-based environments where browser-centric tooling is inconvenient.

### Project Details

#### Solution

Dotui consists of two core modules.

**Module 1: Live Block Explorer**

- Live block stream: new finalized blocks appear in real time.
- Per-block view: extrinsics list, events log, timestamp, parent hash, and state root.
- Extrinsic detail view: decoded call data, signer, tip, and nonce.
- Keyboard navigation: arrow keys to move, `Enter` to drill down, `Esc` to go back.
- Chain selector: Polkadot, Kusama, Westend, or a custom WebSocket RPC endpoint.

**Module 2: Wallet & Transfers**

- Load accounts from a JSON keystore file or mnemonic phrase (BIP39).
- View account balance, nonce, and on-chain identity when available.
- Construct and sign transfer extrinsics locally.
- Broadcast transactions and track status in real time.
- Transaction history view for the loaded account.

#### Conceptual TUI Layout

```text
┌─ Dotui ─────────────────────────────────────────────────────┐
│ Network: Polkadot    Block: #21,543,201    Finalized: ✓     │
├──────────────────┬──────────────────────────────────────────┤
│ BLOCKS           │ EXTRINSICS (#21543201)                   │
│ ▶ #21,543,201    │ transfer(5Grwv... → 5FHne..., 10 DOT)   │
│   #21,543,200    │ stake(5Cx5o..., 500 DOT)                 │
│   #21,543,199    │ vote(referendum_42, aye)                 │
├──────────────────┴──────────────────────────────────────────┤

```

#### Technical Stack

| Component                | Library / Tool           | Purpose                                                                      |
| ------------------------ | ------------------------ | ---------------------------------------------------------------------------- |
| Core Integration Library | `substrate_tui`          | Reusable application core for Dotui, external integrations, and node helpers |
| TUI Framework            | `ratatui` 0.26+          | Rendering panels, widgets, and keyboard-driven views                         |
| Terminal Backend         | `crossterm` 0.27+        | Cross-platform terminal control and input handling                           |
| Substrate Client         | `subxt` 0.35+            | Type-safe Substrate / Polkadot RPC access                                    |
| Async Runtime            | `tokio` 1.x              | Async subscriptions, RPC requests, and background tasks                      |
| Keystore / Signing       | `sp-core`                | Local key management and transaction signing                                 |
| Build & CI               | `cargo` + GitHub Actions | Testing, builds, and cross-platform release binaries                         |

#### Planned Interface / Startup Options

As a terminal application, Dotui will primarily be used by launching the TUI directly. The initial scope includes:

- `dotui` — start the application with the default network.
- `dotui --network <polkadot|kusama|westend>` — start directly on a known network.
- `dotui --rpc-url <ws-url>` — start with a custom WebSocket endpoint.
- `dotui` binary options for local workflows, including development and testnet node execution.

Wallet import and transfer flows are planned to be performed inside the TUI, not through separate CLI subcommands in this grant scope.

The `dotui` binary will be powered by a reusable `substrate_tui` library. In addition to serving the terminal application itself, `substrate_tui` will support external integration by exposing the core explorer, wallet, and network-management capabilities in a reusable form. The library will also include support for running local devnet and testnet nodes for demos, development, and integration testing workflows.

#### Architecture Notes

- No hosted backend is required; Dotui talks directly to a connected node.
- Keys never leave the user machine; signing is local-only.
- The application state is split into network state, explorer state, wallet state, and UI navigation state.
- Core functionality will be implemented in the `substrate_tui` library so the same logic can be reused by external integrations.
- The library will include support for local devnet and testnet node execution during development and testing flows.
- The transaction history view will be implemented without introducing a mandatory external indexing service in the MVP scope.

#### Out of Scope for This Grant

- Browser extension, mobile wallet, or custodial wallet functionality.
- Advanced staking, governance, or multisig flows.
- A hosted explorer backend or managed indexing platform.
- Hardware wallet integration in the initial grant scope.

### Ecosystem Fit

- **Where and how does your project fit into the ecosystem?** Dotui fits as a terminal-native interface for Polkadot SDK chains. It complements browser-first explorers and wallets by serving users who operate in terminals, remote servers, and developer environments.
- **Who is your target audience?** Developers, DevOps and infrastructure teams, validators, power users, and community contributors who want fast read access to chain activity plus simple local-signing transfer functionality.
- **What need(s) does your project meet?** Dotui reduces friction for two common workflows: monitoring finalized blocks and submitting basic transfers from a terminal-native interface. This is especially useful in SSH sessions, low-resource environments, and workflows where users prefer keyboard-driven tooling.
- **How did you identify these needs?** Existing Polkadot tooling is strong in browser and web-based experiences, but there is still room for a compact terminal-first interface focused on live chain inspection and local signing. Dotui is intended to fill that usability gap rather than replace existing wallets or explorers.
- **Are there any other projects similar to yours in the Substrate / Polkadot / Kusama ecosystem?** There are mature browser and web-native products for exploration and wallet usage, including explorer and wallet interfaces used across the ecosystem. Dotui differs by focusing on a single terminal-native workflow that combines real-time exploration and local transfer execution.
- **Are there any projects similar to yours in related ecosystems?** Terminal-first tools in adjacent ecosystems and infrastructure domains show that users value fast, keyboard-driven interfaces. Dotui applies that style of UX specifically to Polkadot-compatible chains.

## Team :busts_in_silhouette:

### Team members

- Shanith K K - Solo Founder & Researcher

### Contact

- **Contact Name:** Shanith K K
- **Contact Email:** kkshanith@gmail.com
- **Website:** [Shanith K K](https://github.com/shanithkk/)

### Legal Structure

- **Registered Address:** Individual researcher - no registered entity
- **Registered Legal Entity:** N/A - Individual

### Team's experience

To be completed by the applicant before submission. This section should summarize the team's experience with Rust, async systems, terminal applications, and Substrate / Polkadot integrations, plus any relevant shipped products or open-source work.

If anyone on the team has previously applied for a Web3 Foundation grant, that information should also be added here.

### Team Code Repos

- [Substrate TUI](https://github.com/shanithkk/substrate-tui)

Please also provide the GitHub accounts of all team members.

- [Shanith K K](https://github.com/shanithkk/)

### Team LinkedIn Profiles (if available)

- [Shanith K K](https://www.linkedin.com/in/shanith-kk/)

## Development Status :open_book:

Development of the project has already started, and approximately **50%** of the planned work is already completed. The current codebase includes the core terminal UI shell, the project structure for the reusable `substrate_tui` library and `dotui` binary, and the initial implementation of the main operator workflows.

Current preparation for the grant scope includes:

- a scoped product definition for a live explorer and wallet-transfer TUI,
- a conceptual interface layout,
- a Rust-based implementation plan using `ratatui`, `crossterm`, `subxt`, `tokio`, and `sp-core`, and
- a milestone plan with explicit testing and documentation outputs.

A recording/demo of the current implementation is provided below as supporting material.

## Development Roadmap :nut_and_bolt:

### Overview

- **Total Estimated Duration:** 12 weeks
- **Full-Time Equivalent (FTE):** 1
- **Total Costs:** 10,000 USD
- **DOT %:** 50%

### Milestone 1 — Core TUI Shell & Block Explorer

- **Estimated duration:** 5 weeks
- **FTE:** 1
- **Costs:** 5,000 USD

|  Number | Deliverable                           | Specification                                                                                                                                                          |
| ------: | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **0a.** | License                               | All code produced for this milestone will be published under an open-source license (`Apache 2.0 / MIT`).                                                              |
| **0b.** | Documentation                         | README with installation, supported networks, startup options, keyboard shortcuts, and usage instructions for the live block explorer.                                 |
| **0c.** | Testing and Testing Guide             | Unit tests for RPC parsing, block/extrinsic/event data models, and UI state transitions, plus a guide for running the tests locally.                                   |
| **0d.** | Docker                                | A Dockerfile that builds the binary and runs the automated test suite / smoke checks for the milestone deliverables.                                                   |
|      1. | TUI shell and navigation              | Runnable Rust binary with `ratatui` layout, including header, panels, status bar, and help overlay. Keyboard navigation supports arrow keys, `Enter`, `Esc`, and `q`.  |
|      2. | Network selector and RPC connectivity | WebSocket connection to Polkadot, Kusama, Westend, or a custom Substrate-compatible endpoint via `subxt`, including connection status feedback in the UI.              |
|      3. | Live finalized block feed             | Real-time, auto-updating block feed that subscribes to finalized blocks and renders new entries as they arrive.                                                        |
|      4. | Block and extrinsic drill-down        | Selected block view showing extrinsics, events, timestamp, parent hash, and state root, plus per-extrinsic detail view with decoded call data, signer, tip, and nonce. |
|      5. | `substrate_tui` core library          | Reusable core library crate that powers the `dotui` binary and exposes explorer and network primitives for external integrations.                                      |

### Milestone 2 — Wallet & Transfer Module

- **Estimated duration:** 5 weeks
- **FTE:** 1
- **Costs:** 3,000 USD

|  Number | Deliverable                         | Specification                                                                                                                                                    |
| ------: | ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **0a.** | License                             | All code produced for this milestone will be published under an open-source license (`Apache 2.0 / MIT`).                                                        |
| **0b.** | Documentation                       | User documentation for account loading, transfer flow, validation rules, and transaction tracking, plus security notes describing local key handling.            |
| **0c.** | Testing and Testing Guide           | Unit and integration tests covering signing, validation, and transaction submission flow, with a guide describing how to reproduce the tests.                    |
| **0d.** | Docker                              | Updated Docker-based test environment for building the application and validating the non-interactive parts of the wallet workflow.                              |
|      1. | Account import and local signing    | Load accounts from JSON keystore files or mnemonic phrases (BIP39) and sign transactions locally using `sp-core`, ensuring private keys never leave the machine. |
|      2. | Account overview                    | Wallet panel showing the selected account's address, balance, nonce, and on-chain identity when available on the connected network.                              |
|      3. | Transfer composer                   | Transfer form for recipient and amount input, including address and amount validation before signing.                                                            |
|      4. | Broadcast and confirmation tracking | Broadcast signed transfer extrinsics and display submission, inclusion, and finalization status in real time.                                                    |
|      5. | Transaction history view            | A history panel for the loaded account that surfaces recent transfer activity within the MVP constraints of the connected chain/RPC environment.                 |
|      6. | Westend integration coverage        | Integration tests and validation guide for signing and submitting transactions on Westend testnet.                                                               |

### Milestone 3 — Polish, Cross-Platform Releases & Docs

- **Estimated duration:** 2 weeks
- **FTE:** 1
- **Costs:** 2,000 USD

|  Number | Deliverable                                | Specification                                                                                                                                           |
| ------: | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **0a.** | License                                    | All code produced for this milestone will remain available under the selected open-source license (`Apache 2.0 / MIT`).                                 |
| **0b.** | Documentation                              | Complete user documentation, configuration reference, inline help documentation, and a developer contribution guide.                                    |
| **0c.** | Testing and Testing Guide                  | Final regression test guide covering explorer, wallet, release verification, and configuration flows.                                                   |
| **0d.** | Docker                                     | Final build/test container configuration for reproducible validation of the project deliverables.                                                       |
|     0e. | Article / Tutorial                         | Publish a walkthrough article and a tutorial video or animated GIF demonstrating the main explorer and wallet workflows.                                |
|      1. | Cross-platform release automation          | GitHub Actions workflows producing release binaries for Linux x86_64, macOS arm64/x86_64, and Windows.                                                  |
|      2. | Config file support                        | Support for `~/.dotui/config.toml` to persist preferred endpoints and user settings.                                                                    |
|      3. | Resilience and UX polish                   | Graceful disconnect handling, reconnection logic, and user-friendly error states across the explorer and wallet flows.                                  |
|      4. | Inline help system                         | Full in-app help overlay accessible from the keyboard shortcut help flow.                                                                               |
|      5. | Final developer and operator documentation | Contribution guide, local build instructions, release notes, and verification instructions for reviewers and contributors.                              |
|      6. | Devnet / testnet runner support            | `substrate_tui` will include helper functionality for running local devnet and testnet nodes for development, demos, and integration testing workflows. |

## Future Plans

After the initial grant scope, Dotui can expand into a broader terminal-native toolkit for Polkadot ecosystem users. Potential follow-up work includes richer account actions, staking and governance views, support for additional pallets and chains, stronger account history capabilities, and optional integrations with other local signing methods.

In the short term, the focus will be on shipping a polished MVP, making onboarding simple, and gathering feedback from developers and operators who prefer terminal-based workflows. Long-term maintenance can be supported through follow-up ecosystem grants, sponsored development, consulting, or direct community contributions to the open-source project.

## Referral Program (optional) :moneybag:

- **Referrer:** TBD
- **Payment Address:** TBD

## Additional Information :heavy_plus_sign:

**How did you hear about the Grants Program?** Worked in Aurras.

Additional information:

- Project repository / prototype: [https://github.com/shanithkk/substrate-tui](https://github.com/shanithkk/substrate-tui)
- Work on the project has already started, and approximately **50%** of the planned implementation is already completed.
- A recording/demo of the current state of the project is provided below.
- There are currently no other teams or sponsors supporting the project.

### Current Progress Screenshots

Watch Demo - click the image below

[![Watch the video](https://res.cloudinary.com/dfhemk1nz/image/upload/v1773254619/dotui_qws67l.png)](https://player.cloudinary.com/embed/?cloud_name=dfhemk1nz&public_id=dotui_q6dcpg)

[![Dotui explorer view](https://res.cloudinary.com/dfhemk1nz/image/upload/v1773254619/dotui-explorer_j9nily.png)](https://player.cloudinary.com/embed/?cloud_name=dfhemk1nz&public_id=dotui_q6dcpg)
