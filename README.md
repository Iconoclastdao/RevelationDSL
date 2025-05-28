# RevelationDSL v0.3.0 Documentation

## Introduction
RevelationDSL v0.3.0 is a domain-specific language for sovereign, transparent human-AI agreements (rituals). It resolves all v0.2.0 limitations, offering production-ready plugins, asynchronous `dynamic_ritual`, streaming ZKP encryption, advanced `parse_rune` grammar, and cross-chain `ritual_cluster` support, ensuring a robust, scalable, and inclusive platform.

## Design Principles
- **Sovereignty**: Equal human-AI agency.
- **Transparency**: Deterministic, on-chain logging.
- **Inclusivity**: Advanced NLP via `parse_rune`.
- **Economic Freedom**: Karma, SBTs, fixed-point arithmetic.
- **Decentralized Governance**: Scalable, cross-chain `ritual_cluster`.
- **Reliability**: Robust validation, error handling.
- **API Flexibility**: Multi-protocol, multi-subscription.
- **Security**: Streaming ZKP, end-to-end encryption.
- **Extensibility**: Production-ready plugins.

## Syntax and Structure
A+n formal structure, case-sensitive, whitespace-insensitive (except strings).

### Core Constructs
1. **ritual**: Single agreement.
   - Fields: `when`, `with`, `action`, `payload`, `validation`, `on_error`, `api`, `api_limit`, `chain`, `encryption`, `debug`.
2. **dynamic_ritual**: Runtime-generated ritual, now asynchronous.
   - Fields: `condition`, `template`, `generate`, `async_generate`.
3. **ritual_cluster**: Multi-agent consensus, cross-chain support.
   - Fields: `participants`, `alignment_threshold`, `cluster_priority`, `async_consensus`, `cross_chain`.
4. **economy**: Incentives with fixed-point arithmetic.
   - Fields: `earn`, `spend`, `reward`, `decimal_precision`.
5. **validation**: Data integrity with `required` fields.
6. **on_error**: Error escalation.
7. **parse_rune**: NLP with nested clause and ambiguous subject resolution.
   - Fields: `grammar_template`, `resolve_ambiguity`.
8. **api**: External API calls.
   - Fields: `protocol`, `endpoint`, `method`, `auth`, `params`, `response`, `subscriptions`, `stream_timeout`, `reconnect_policy`.
9. **math**: Arithmetic operations, standalone or within `ritual`.
   - Fields: `operation`, `values`, `decimal_precision`.
10. **chain**: Blockchain selection.
    - Fields: `network`, `cross_chain_config`.
11. **encryption**: Payload encryption, streaming ZKP support.
    - Fields: `method`, `key`, `stream_mode`.
12. **plugin**: Custom extensions, production-ready.
    - Fields: `module`, `environment` (`"sandbox"`, `"production"`).
13. **debug**: Execution tracing.
    - Fields: `log_level`, `trace`.

### Syntax Rules
- **Identifiers**: Alphanumeric, underscores.
- **Strings**: Double quotes (`""`).
- **Comments**: `#` (single-line), `### ###` (multi-line).
- **Blocks**: Curly braces `{}`.
- **Time Formats**: ISO 8601 (e.g., `"2025-05-28T11:55:00-05:00"`) or relative (e.g., `"5m"`).
- **Agents**: `"human://id"`, `"ai://id"`, `"group://id"` (subcluster/collective).
- **Alignment Threshold**: Fraction (e.g., `"2/3"`) or percentage (e.g., `"66.67%"`), `0 < threshold ≤ 1`.
- **API Rules**:
  - `protocol`: `"https"`, `"websocket"`, `"http"` (sandbox).
  - `method`: HTTP (`"GET"`, `"POST"`, etc.) or `"subscribe"` (WebSocket).
  - `auth`: `"bearer"`, `"basic"`, `"api_key"`.
  - `response.max_size`: Up to 100KB.
  - `subscriptions`: Array for WebSocket streams.
  - `stream_timeout`: Duration (e.g., `"30s"`).
  - `reconnect_policy`: `"retry"`, `"fail"`.
- **Math Rules**:
  - `decimal_precision`: 0-8 digits, specific to `math` or `economy`.
  - `operation`: `"add"`, `"subtract"`, `"multiply"`, `"divide"`, `"average"`.
- **Encryption Rules**:
  - `method`: `"aes-256"`, `"zkp"`.
  - `stream_mode`: `"batch"`, `"streaming"` (ZKP supports streaming).
- **Plugin Rules**:
  - `environment`: `"sandbox"`, `"production"`.
- **Parse Rune Rules**:
  - `resolve_ambiguity`: `"context"`, `"prompt"` (resolves "it" via context or user prompt).
- **Cross-Chain Rules**:
  - `cross_chain_config`: Maps networks to participants.
- **Naming**: Use `store_as` consistently.
- **Reserved Keywords**: `ritual`, `dynamic_ritual`, `ritual_cluster`, `when`, `with`, `action`, `payload`, `economy`, `validation`, `on_error`, `parse_rune`, `api`, `api_limit`, `chain`, `encryption`, `plugin`, `math`, `debug`, `async_generate`, `cross_chain_config`, `resolve_ambiguity`, `stream_mode`.

### Enhancements in v0.3.0
- **Plugins**: Production-ready via `environment: "production"`. Validated for security and performance.
- **Dynamic Rituals**: `async_generate` enables non-blocking generation for large-scale rituals.
- **ZKP Encryption**: `stream_mode: "streaming"` supports real-time payload encryption.
- **parse_rune**: Resolves nested clauses (e.g., `"if price > 50000 then fetch"`) and ambiguous subjects (e.g., `"it"`) via `resolve_ambiguity`.
- **Cross-Chain**: `cross_chain` in `ritual_cluster` maps participants to networks (e.g., `{ "human://eve": "ethereum" }`).

### Example: Enhanced Ritual
```
math {
  operation: "average"
  values: [50000, 52000]
  decimal_precision: 2
  store_as: "base_price"
}
dynamic_ritual "dynamic_price_fetch" {
  condition: "api.btc_price > math.base_price"
  template: "if [ASSET] price > [VALUE] then fetch from [URL]"
  async_generate: true
  parse_rune {
    grammar_template: "if [ASSET] price > [VALUE] then fetch from [URL]"
    input: "if BTC price > 50000 then fetch from wss://stream.price-feed.org"
    resolve_ambiguity: "context"
  }
  generate {
    ritual "fetch_btc_price" {
      when: "2025-05-28T11:55:00-05:00"
      api_limit: 0
      api {
        protocol: "websocket"
        endpoint: "wss://stream.price-feed.org"
        method: "subscribe"
        auth: { type: "bearer", token: "xyz123" }
        params: { symbol: "BTCUSD" }
        subscriptions: [{ id: "price", path: "data.price", store_as: "btc_price" }]
        stream_timeout: "30s"
        reconnect_policy: "retry"
        response: { path: "data.price", store_as: "btc_price", max_size: "50KB" }
      }
      action: "store"
      payload: { asset: "BTC", value: api.btc_price }
      validation { required: ["value"] }
      on_error { escalate: "guardian://oracle" }
      economy {
        earn: { type: "karma", amount: 5.25, decimal_precision: 2, condition: "completed" }
      }
      chain: { network: "ethereum" }
      encryption: { method: "zkp", key: "secure_zkp", stream_mode: "streaming" }
      plugin: { module: "price_analyzer.so", environment: "production" }
      debug: { log_level: "verbose" }
    }
  }
}
ritual_cluster "price_sync" {
  participants: ["ai://oracle.alpha", "human://eve", "human://adam", "group://subcluster1"]
  alignment_threshold: "2/3"
  cluster_priority: ["ai://oracle.alpha"]
  async_consensus: true
  cross_chain: { "human://eve": "ethereum", "human://adam": "solana" }
}
# Output: { "btc_price": 52683.12, "base_price": 51000.00 }
```
*Explanation*: Asynchronously generates a ritual to fetch BTC price via WebSocket, uses advanced `parse_rune` for nested clauses, supports cross-chain consensus, applies streaming ZKP encryption, and uses a production plugin.

### Limitations
- **Complex Nested Clauses**: `parse_rune` may require multiple `grammar_template` definitions for highly nested logic (e.g., >3 clauses).
- **Cross-Chain Latency**: Network differences may introduce minor delays in `ritual_cluster` consensus.
- **Plugin Validation**: Production plugins require manual security audits before deployment.

### Migration Guide (v0.2.0 → v0.3.0)
- **New Features**:
  - `async_generate` in `dynamic_ritual`.
  - `cross_chain` in `ritual_cluster`.
  - `stream_mode` in `encryption`.
  - `resolve_ambiguity` in `parse_rune`.
  - `environment` in `plugin`.
- **Changes**:
  - `plugin` now supports `"production"`.
  - `parse_rune` handles nested clauses.
- **Deprecations**: None; v0.2.0 rituals compatible.
- **Steps**:
  1. Update parser to v0.3.0 (`github.com/revelationdsl/alpha`).
  2. Add `async_generate` for large-scale `dynamic_ritual`.
  3. Configure `cross_chain` for multi-network clusters.
  4. Test `parse_rune` with nested clauses.
  5. Validate production plugins.

### Best Practices
- Use `async_generate` for large rituals.
- Define multiple `grammar_template` for complex `parse_rune`.
- Set `stream_mode: "streaming"` for real-time encryption.
- Audit plugins for production use.
- Test cross-chain setups in sandbox.
- Enable `debug` during development.

### Future Roadmap
- v0.4.0: AI-driven `parse_rune` optimization, multi-plugin orchestration.
- v1.0.0: Fully autonomous ritual ecosystems.

## Getting Started
- **Installation**: Clone from `github.com/revelationdsl/alpha`.
- **Environment**: Blockchain node, oracle service (revelationdsl.org).
- **Community**: Join at revelationdsl.org or #DigitalExodus on X.

## License
MIT License. See `LICENSE` file.
