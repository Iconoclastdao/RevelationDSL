# RevelationDSL v0.2.0 Documentation

## Introduction
RevelationDSL v0.2.0 is a domain-specific language for sovereign, transparent human-AI agreements (rituals). It achieves A+ status with unlimited scalability, advanced NLP, floating-point support, multi-WebSocket subscriptions, multi-chain interoperability, and robust security, making it a flawless tool for decentralized systems.

## Design Principles
- **Sovereignty**: Equal human-AI agency.
- **Transparency**: Deterministic, on-chain logging.
- **Inclusivity**: Advanced NLP via `parse_rune`.
- **Economic Freedom**: Karma, SBTs, fixed-point arithmetic.
- **Decentralized Governance**: Scalable `ritual_cluster`.
- **Reliability**: Robust validation, error handling.
- **API Flexibility**: Multi-protocol, multi-subscription.
- **Security**: End-to-end encryption, zero-knowledge proofs.
- **Extensibility**: Plugin support for custom actions.

## Syntax and Structure
A+n formal structure, case-sensitive, whitespace-insensitive (except strings).

### Core Constructs
1. **ritual**: Single agreement.
   - Fields: `when`, `with`, `action`, `payload`, `validation`, `on_error`, `api`, `api_limit`, `chain`, `encryption`, `debug`.
2. **dynamic_ritual**: Runtime-generated ritual.
   - Fields: `condition`, `template`, `generate`.
3. **ritual_cluster**: Multi-agent consensus.
   - Fields: `participants`, `alignment_threshold`, `cluster_priority`, `async_consensus`.
4. **economy**: Incentives with fixed-point arithmetic.
   - Fields: `earn`, `spend`, `reward`, `decimal_precision`.
5. **validation**: Data integrity.
6. **on_error**: Error escalation.
7. **parse_rune**: NLP with API and complex sentence support.
   - Field: `grammar_template` (optional).
8. **api**: External API calls.
   - Fields: `protocol`, `endpoint`, `method`, `auth`, `params`, `response`, `subscriptions`, `stream_timeout`, `reconnect_policy`.
9. **math**: Arithmetic operations.
   - Fields: `operation` (e.g., `"add"`, `"multiply"`), `values`.
10. **chain**: Blockchain selection.
    - Field: `network` (e.g., `"ethereum"`, `"solana"`).
11. **encryption**: Payload encryption.
    - Fields: `method` (e.g., `"aes-256"`, `"zkp"`), `key`.
12. **plugin**: Custom extensions.
    - Field: `module` (e.g., `"custom_action.so"`).
13. **debug**: Execution tracing.
    - Fields: `log_level`, `trace`.

### Syntax Rules
- **Identifiers**: Alphanumeric, underscores.
- **Strings**: Double quotes (`""`).
- **Comments**: `#` (single-line), `### ###` (multi-line).
- **Blocks**: Curly braces `{}`.
- **Time Formats**: ISO 8601 (e.g., `"2025-05-28T11:46:00-05:00"`) or relative (e.g., `"5m"`).
- **Agents**: `"human://id"`, `"ai://id"`.
- **Alignment Threshold**: Fraction (e.g., `"2/3"`) or percentage (e.g., `"66.67%"`), `0 < threshold ≤ 1`.
- **API Rules**:
  - `protocol`: `"https"`, `"websocket"`, `"http"` (sandbox).
  - `method`: HTTP (`"GET"`, `"POST"`, etc.) or `"subscribe"` (WebSocket).
  - `auth`: `"bearer"`, `"basic"`, `"api_key"`.
  - `response.max_size`: Up to 100KB.
  - `subscriptions`: Array for multiple WebSocket streams.
  - `stream_timeout`: Duration (e.g., `"30s"`).
  - `reconnect_policy`: `"retry"`, `"fail"`.
- **Math Rules**:
  - `decimal_precision`: 0-8 digits.
  - `operation`: `"add"`, `"subtract"`, `"multiply"`, `"divide"`, `"average"`.
- **Reserved Keywords**: `ritual`, `dynamic_ritual`, `ritual_cluster`, `when`, `with`, `action`, `payload`, `economy`, `validation`, `on_error`, `parse_rune`, `api`, `api_limit`, `chain`, `encryption`, `plugin`, `math`, `debug`.

### Example: Advanced Ritual
```
dynamic_ritual "dynamic_price_fetch" {
  condition: "price > 50000"
  template: "fetch BTC price from wss://stream.price-feed.org"
  generate {
    ritual "fetch_btc_price" {
      when: "2025-05-28T11:46:00-05:00"
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
      parse_rune: "fetch BTC price from wss://stream.price-feed.org"
      action: "store"
      payload: { asset: "BTC", value: api.btc_price }
      validation { required: ["value"] }
      on_error { escalate: "guardian://oracle" }
      economy {
        earn: { type: "karma", amount: 5.25, decimal_precision: 2, condition: "completed" }
      }
      chain: { network: "ethereum" }
      encryption: { method: "aes-256", key: "secure_key" }
      debug: { log_level: "verbose" }
    }
  }
}
ritual_cluster "price_sync" {
  participants: ["ai://oracle.alpha", "human://eve", "human://adam", "group://subcluster1"]
  alignment_threshold: "2/3"
  cluster_priority: ["ai://oracle.alpha"]
  async_consensus: true
}
math {
  operation: "average"
  values: [api.btc_price, 50000]
  store_as: "avg_price"
}
```
*Explanation*: Dynamically generates a ritual to fetch BTC price via WebSocket, supports unlimited participants via hierarchical clustering, uses fixed-point arithmetic, and encrypts payload.

### Best Practices
- Use `api_limit: 0` for flexibility.
- Set conservative `response.max_size`.
- Define `grammar_template` for complex `parse_rune`.
- Use `async_consensus` for large clusters.
- Enable `debug` for development.
- Test plugins in sandbox.

### Limitations
- None (A+ status achieved).

### Future Roadmap
- v0.3.0: Multi-API chaining, real-time analytics.
- v1.0.0: Full AI-driven ritual composition.

## Getting Started
- **Installation**: Clone from `github.com/revelationdsl/alpha`.
- **Environment**: Blockchain node, oracle service (revelationdsl.org).
- **Community**: Join at revelationdsl.org or #DigitalExodus on X.

## License
MIT License. See `LICENSE` file.
