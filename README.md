# UniRitualDSL v1.0.3 Documentation

## Introduction
UniRitualDSL v1.0.3 is a domain-agnostic, innovative DSL for transparent human-AI agreements, schema-driven data modeling, and task automation. Merging RevelationDSL’s sovereignty and blockchain capabilities with Universal DSL Schema’s flexible schema design, it supports blockchain, IoT, enterprise workflows, AI-driven automation, and data processing. New in v1.0.3: schema composition (`allOf`), completed cross-chain spec, `include` examples, `meta_ritual` for recursive DSL construction, UI integration with `ui` field, agent ACLs, and a glossary for clarity.

## Design Principles
- **Sovereignty**: Equal agency for humans and AI.
- **Transparency**: Deterministic logging with structured audit trails.
- **Inclusivity**: Multi-language NLP and UI support.
- **Flexibility**: Advanced schema types for diverse data modeling.
- **Extensibility**: Secure plugins with WebAssembly support.
- **Accessibility**: Low-code interfaces, templates, glossary, and UI integration.
- **Reliability**: Robust validation, testing, and error handling.
- **Security**: End-to-end encryption, plugin permissions, and agent ACLs.
- **Interoperability**: Multi-protocol APIs (HTTP, WebSocket, gRPC, GraphQL) and multi-runtime environments (blockchain, local, cloud).
- **Performance**: Asynchronous processing and scalable execution.

## Syntax and Structure
- **Formal Structure**: A+n, case-sensitive, whitespace-insensitive (except strings).
- **Delimiters**: Blocks `{}`; lists `[]`; key-value pairs `:`.
- **Comments**: Single-line `#`, multi-line `### ###`.
- **Identifiers**: Alphanumeric, underscores, no leading digits (e.g., `user_123`).
- **Strings**: Double quotes `""` (e.g., `"Hello, World!"`).
- **Numbers**: Integers (e.g., `42`), decimals (e.g., `3.14`), scientific notation (e.g., `1.5e-10`).
- **Booleans**: `true`, `false`.
- **Time Formats**: ISO 8601 (e.g., `"2025-05-28T12:31:00-05:00"`) or relative (e.g., `"5m"`, `"2h30m"`).
- **Agents**: URI-style (e.g., `human://alice`, `ai://bot1`, `group://team1`).
- **Alignment Threshold**: Fraction (e.g., `"2/3"`) or percentage (e.g., `"75%"`), `0 < threshold ≤ 1`.

## Core Constructs
### `ritual`
Defines a human-AI agreement or task.
- **Fields**:
  - `when`: Execution time (ISO 8601 or relative).
  - `with`: Agents (array of URIs).
  - `action`: Task type (e.g., `"store"`, `"notify"`, `"execute"`).
  - `payload`: Data object.
  - `validation`: Required fields and rules.
  - `on_error`: Error handling (`escalate`, `retry`, `ignore`).
  - `api`: External API integration.
  - `api_limit`: Rate limit (requests per second, `0` for unlimited).
  - `encryption`: Encryption settings.
  - `plugin`: Custom module.
  - `debug`: Logging and tracing.
  - `schema`: Data schema.
  - `ritual_log`: Audit trail configuration.
  - `ritual_sign`: Cryptographic signing.
  - `lang`: Language code (e.g., `"en-US"`, `"es-ES"`).
  - `ui`: UI rendering settings (e.g., form, dashboard).
  - `acl`: Access control list for agents.
- **Example**:
  ```dsl
  ritual "store_user_data" {
    when: "2025-05-28T12:31:00-05:00"
    with: ["human://alice", "ai://data_processor"]
    action: "store"
    payload: { name: "Alice", age: 30, email: "alice@example.com" }
    schema: "user_data"
    validation: { required: ["name", "email"] }
    on_error: { escalate: "admin://support" }
    encryption: { method: "aes-256", key: "secure_key_123" }
    ritual_log: { format: "json", store: "audit://logs", retention: "30d" }
    ritual_sign: { method: "ed25519", key: "alice_key" }
    debug: { log_level: "verbose" }
    lang: "en-US"
    ui: { type: "form", fields: [{ name: "name", label: "Name" }, { name: "email", label: "Email" }] }
    acl: { "human://alice": ["read", "write"], "ai://data_processor": ["write"] }
  }
  ```

### `dynamic_ritual`
Generates rituals at runtime, asynchronously.
- **Fields**:
  - `condition`: Trigger (e.g., `"api.price > 100"`).
  - `template`: String template.
  - `async_generate`: Boolean.
  - `parse_rune`: NLP parsing.
  - `schema`: Schema for generated ritual.
  - `lang`: Language code.
  - `ui`: UI settings.
- **Example**:
  ```dsl
  dynamic_ritual "dynamic_fetch" {
    condition: "api.stock_price > 150.50"
    template: "if [ASSET] price > [VALUE] then fetch from [URL]"
    async_generate: true
    parse_rune {
      grammar_template: "if [ASSET] price > [VALUE] then fetch from [URL]"
      input: "if AAPL price > 150.50 then fetch from https://api.stocks.com"
      resolve_ambiguity: "context"
      lang: "en-US"
    }
    schema: { type: "object", properties: { asset: { type: "string" }, value: { type: "number" } } }
    ui: { type: "dashboard", metrics: ["price"] }
    generate {
      ritual "fetch_stock" {
        when: "now"
        api: { protocol: "https", endpoint: "https://api.stocks.com", method: "GET", params: { symbol: parse_rune.asset } }
        action: "store"
        payload: { asset: parse_rune.asset, price: api.response.price }
      }
    }
  }
  ```

### `meta_ritual`
Defines or updates rituals at runtime (recursive DSL construction).
- **Fields**:
  - `target`: Ritual or `dynamic_ritual` to modify.
  - `operation`: `"create"`, `"update"`, `"delete"`.
  - `template`: Modified ritual template.
  - `schema`: Schema for validation.
- **Example**:
  ```dsl
  meta_ritual "update_notification" {
    target: "send_notification"
    operation: "update"
    template: {
      action: "notify"
      payload: { message: "Updated message" }
    }
    schema: { type: "object", properties: { message: { type: "string" } } }
  }
  ```

### `ritual_cluster`
Manages multi-agent consensus.
- **Fields**:
  - `participants`: Agent URIs.
  - `alignment_threshold`: Consensus threshold (e.g., `"2/3"`, `"75%"`).
  - `cluster_priority`: Agent priority order.
  - `async_consensus`: Boolean.
  - `cross_chain`: Optional blockchain mappings.
- **Example**:
  ```dsl
  ritual_cluster "team_decision" {
    participants: ["human://alice", "human://bob", "ai://validator"]
    alignment_threshold: "2/3"
    cluster_priority: ["ai://validator"]
    async_consensus: true
    cross_chain: { "human://alice": "ethereum", "human://bob": "solana" }
  }
  ```

### `schema`
Defines data structures with advanced types.
- **Fields**:
  - `type`: `"object"`, `"array"`, `"string"`, `"number"`, `"boolean"`, `"enum"`, `"union"`.
  - `properties`: Key-value pairs for objects.
  - `required`: Required fields.
  - `format`: Constraints (e.g., `"email"`, `"uri"`, `"date-time"`, custom).
  - `items`: Array element schema.
  - `enum`: Valid values (e.g., `["pending", "approved"]`).
  - `union`: Allowed types (e.g., `[{ type: "string" }, { type: "number" }]`).
  - `custom_format`: Regex/function for validation.
  - `allOf`: Compose schemas for reuse.
- **Example**:
  ```dsl
  schema "base_user" {
    type: "object"
    properties: { id: { type: "string" }, created_at: { type: "string", format: "date-time" } }
  }
  schema "extended_user" {
    allOf: ["base_user", { properties: { email: { type: "string", format: "email" } } }]
  }
  schema "status_enum" {
    type: "enum"
    enum: ["pending", "approved", "rejected"]
  }
  schema "flexible_input" {
    type: "union"
    union: [{ type: "string" }, { type: "number" }]
  }
  schema "custom_email" {
    type: "string"
    custom_format: "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"
  }
  ```

### `contextual_schema`
Binds schemas to runtime state.
- **Fields**:
  - `schema`: Base schema reference.
  - `context`: State key (e.g., `"user_state"`).
  - `dynamic_fields`: Runtime-updated fields.
- **Example**:
  ```dsl
  contextual_schema "dynamic_user" {
    schema: "extended_user"
    context: "user_state"
    dynamic_fields: { last_login: { type: "string", format: "date-time" } }
  }
  ```

### `parse_rune`
Parses natural language with localization.
- **Fields**:
  - `grammar_template`: Parsing template.
  - `input`: Raw input string.
  - `resolve_ambiguity`: `"context"`, `"prompt"`, `"default"`.
  - `store_as`: Output mapping.
  - `lang`: Language code (e.g., `"es-ES"`).
- **Example**:
  ```dsl
  parse_rune {
    grammar_template: "if [USER] balance > [VALUE] then [ACTION]"
    input: "si el saldo de Alicia > 150 entonces notificar"
    resolve_ambiguity: "context"
    store_as: { user: "USER": { type: "string", minLength: 1 }, value: "VALUE", action: "ACTION" }
    lang: "es-ES"
  }
  ```

### `api`
Handles external integrations.
- **Fields**:
  - `protocol`: `"https"`, `"http"`, `"websocket"`, `"grpc"`, `"graphql"`.
  - `endpoint`: URL or address.
  - `method`: HTTP methods, `"subscribe"`, or GraphQL query/mutation.
  - `auth`: `"bearer"`, `"basic"`, `"api_key"`, `"none"`.
  - `params`: Query/body parameters.
  - `subscriptions`: WebSocket subscription paths.
  - `response`: Response handling (e.g., `path`, `store_as`, `max_size`).
  - `stream_timeout`: Duration (e.g., `"30s"`).
  - `reconnect_policy`: `"retry"`, `"fail"`.
- **Example**:
  ```dsl
  api {
    protocol: "graphql"
    endpoint: "https://api.example.com/graphql"
    method: "query"
    auth: { type: "bearer", token: "xyz123" }
    params: { query: "query { user(id: 1) { name } }" }
    response: { path: "data.user.name", store_as: "username", max_size: "10KB" }
  }
  ```

### `math`
Performs arithmetic/statistical operations.
- **Fields**:
  - `operation`: `"add"`, `"subtract"`, `"multiply"`, `"divide"`, `"average"`, `"min"`, `"max"`.
  - `values`: Array of numbers/references.
  - `decimal_precision`: 0–8 digits.
  - `store_as`: Output variable.
- **Example**:
  ```dsl
  math {
    operation: "average"
    values: [100, 200, 300]
    decimal_precision: 2
    store_as: "avg_value"
  }
  ```

### `economy`
Manages incentives/rewards.
- **Fields**:
  - `earn`: Reward (e.g., `{ type: "points", amount: 10 }`).
  - `spend`: Deduction rules.
  - `reward`: Conditional rewards.
  - `decimal_precision`: 0–8 digits.
- **Example**:
  ```dsl
  economy {
    earn: { type: "points", amount: 5.25, condition: "task_completed" }
    decimal_precision: 2
  }
  ```

### `encryption`
Secures data.
- **Fields**:
  - `method`: `"aes-256"`, `"zkp"`.
  - `key`: Encryption key.
  - `stream_mode`: `"batch"`, `"streaming"` (ZKP only).
- **Example**:
  ```dsl
  encryption {
    method: "zkp"
    key: "secure_zkp_key"
    stream_mode: "streaming"
  }
  ```

### `plugin`
Extends functionality with secure modules.
- **Fields**:
  - `module`: Plugin name/path (e.g., `"analyzer.so"`, `"analyzer.wasm"`).
  - `environment`: `"sandbox"`, `"production"`.
  - `permissions`: Capabilities (e.g., `["network", "storage"]`).
- **Example**:
  ```dsl
  plugin {
    module: "analyzer.wasm"
    environment: "sandbox"
    permissions: ["compute"]
  }
  ```

### `debug`
Controls logging/tracing.
- **Fields**:
  - `log_level`: `"none"`, `"info"`, `"verbose"`.
  - `trace`: Boolean.
- **Example**:
  ```dsl
  debug {
    log_level: "verbose"
    trace: true
  }
  ```

### `ritual_log`
Configures audit trails.
- **Fields**:
  - `format`: `"json"`, `"yaml"`, `"text"`.
  - `store`: Location (e.g., `"audit://logs"`, `"file://logs/audit.log"`).
  - `retention`: Period (e.g., `"30d"`, `"1y"`).
- **Example**:
  ```dsl
  ritual_log {
    format: "json"
    store: "audit://logs"
    retention: "30d"
  }
  ```

### `ritual_test`
Unit tests with mock agents.
- **Fields**:
  - `mock_agents`: Mock configurations.
  - `test_input`: Input data.
  - `assertions`: Expected outcomes.
- **Example**:
  ```dsl
  ritual_test "test_notification" {
    mock_agents: [
      { id: "human://alice", response: { status: "success" } },
      { id: "ai://notifier", response: { message: "sent" } }
    ]
    test_input: { user: "Alice", balance: 200 }
    assertions: { notify_result: "success" }
  }
  ```

### `ritual_sign`
Cryptographic signing.
- **Fields**:
  - `method`: `"ed25519"`, `"ecdsa"`.
  - `key`: Signing key.
- **Example**:
  ```dsl
  ritual_sign {
    method: "ed25519"
    key: "alice_key"
  }
  ```

### `agent`
Defines agent properties.
- **Fields**:
  - `capabilities`: Actions (e.g., `["notify", "fetch"]`).
  - `trust_level`: 0–1 (e.g., `0.85`).
  - `audit_policy`: `"log_all"`, `"log_errors"`, `"none"`.
- **Example**:
  ```dsl
  agent "ai://notifier" {
    capabilities: ["notify", "parse", "fetch"]
    trust_level: 0.85
    audit_policy: "log_all"
  }
  ```

## Syntax Rules
- **Indentation**: Optional.
- **Reserved Keywords**: `ritual`, `dynamic_ritual`, `meta_ritual`, `ritual_cluster`, `schema`, `contextual_schema`, `parse_rune`, `api`, `math`, `economy`, `encryption`, `plugin`, `debug`, `ritual_log`, `ritual_test`, `ritual_sign`, `agent`, `when`, `with`, `action`, `payload`, `validation`, `on_error`, `async_generate`, `cross_chain`, `resolve_ambiguity`, `stream_mode`, `lang`, `enum`, `union`, `custom_format`, `permissions`, `allOf`, `ui`, `acl`.
- **Imports**: `include "file.dsl"`.
- **Naming**: `store_as` supports schema validation (e.g., `store_as: { user: "USER": { type: "string", minLength: 1 } }`).
- **Schema Validation**: Payloads must conform to schemas.
- **Error Handling**: `on_error` requires `escalate`, `retry`, or `ignore`.
- **API Constraints**:
  - `response.max_size`: ≤100KB.
  - `stream_timeout`: Positive duration (e.g., `"10s"`).
  - `reconnect_policy`: Required for WebSocket/gRPC.
- **Math Constraints**:
  - `decimal_precision`: 0–8.
  - `values`: Non-empty array.
- **Encryption Constraints**:
  - `zkp` requires `stream_mode`.
  - `aes-256` supports `batch` only.
- **Plugin Constraints**:
  - `permissions`: Required in `sandbox`.

## Tooling Ecosystem
### CLI Tool
- **Commands**:
  - `uniritual validate <file.dsl>`: Validates syntax/schemas.
    ```bash
    uniritual validate my.dsl
    ```
  - `uniritual render <file.dsl> --json`: Converts to JSON.
    ```bash
    uniritual render my.dsl --json
    ```
  - `uniritual deploy --ritual <ritual.dsl> --env <testnet|mainnet|local>`: Deploys rituals.
    ```bash
    uniritual deploy --ritual myritual.dsl --env testnet
    ```
- **Installation**: `npm install -g uniritual` or `pip install uniritual`.

### Visual Editor
- **Status**: Beta Q3 2025.
- **Features**: Drag-and-drop ritual creation, schema visualization, validation.
- **Preview**: `uniritualdsl.org/editor-preview`.

### Plugin Development Guide
- **Formats**: `.so` (native), `.wasm` (WebAssembly).
- **Steps**:
  1. Create plugin (C/Rust for `.so`, WebAssembly for `.wasm`).
  2. Define interface: `init`, `execute`, `cleanup`.
  3. Set permissions: `["network", "storage", "compute"]`.
  4. Sandbox with limits (CPU: 10%, Memory: 100MB, Network: 1MB/s).
  5. Audit using `uniritual audit <module>` for security.
  6. Deploy to `production` after audit.
- **Security Best Practices**:
  - Use least privilege permissions.
  - Validate inputs/outputs.
  - Enable sandbox logging.
  - Run `uniritual audit` for vulnerabilities.

### LSP / Editor Integration
- **LSP**: Syntax highlighting, autocompletion, hover documentation.
- **Editors**: VS Code, IntelliJ, Vim.
- **Setup**: `uniritual-lsp` from `uniritualdsl.org/lsp`.

### Testing Framework
- **Ritual Test Runner**: Executes `ritual_test` with mocks.
  ```bash
  uniritual test myritual.dsl
  ```
- **Mock Agents**: Simulate responses.
- **Assertions**: Validate outputs.

### Blockchain Module
- **Adapter Pattern**: Adapters for Ethereum, Solana, etc.
- **Schema**:
  ```dsl
  cross_chain {
    adapter: {
      network: "ethereum"
      contract: "0xabc123..."
      method: "storeData"
      gas_limit: 200000
      rpc_endpoint: "https://eth-rpc.example.com"
    }
    participants: { "human://alice": "ethereum", "ai://bot": "solana" }
  }
  ```

### Visual Grammar Guide
- **Reference**: Syntax tree diagrams at `uniritualdsl.org/grammar`.
- **Purpose**: Visualize ritual, schema, and parse_rune structures for onboarding.

## Deployment and Execution Engine
### Ritual Engine
- **Design**: Distributed runtime (blockchain, local, cloud).
- **Components**:
  - Parser: Validates DSL/schemas.
  - Executor: Asynchronous ritual execution.
  - Logger: Audit trails via `ritual_log`.
  - Replayer: Dry runs/rollback.
- **Dry Runs**: Simulate without side effects.
  ```bash
  uniritual dry-run myritual.dsl
  ```
- **Audit Logs**: Stored in `ritual_log.store`.
- **Rollback**: Reverts state if `on_error: { rollback: true }`.
- **Replay**: Re-executes from logs.

## Modularity and Composition
- **Imports**: `include "file.dsl"`.
  ```dsl
  include "common.rituals"
  ritual "use_common" {
    action: common.notify
    payload: { message: "Imported ritual" }
    ui: { type: "notification", content: "Task completed" }
  }
  ```
- **Shared Libraries**:
  ```dsl
  # common.rituals
  ritual "notify" {
    action: "notify"
    api: { protocol: "https", endpoint: "https://notify.example.com" }
  }
  ```
- **Inheritance**: `extends` or `allOf` for schemas.
  ```dsl
  schema "extended_user" {
    allOf: ["base_user", { properties: { email: { type: "string", format: "email" } } }]
  }
  ```

## Innovative Features
- **Low-Code Interface**: Visual editor (Q3 2025).
- **AI-Driven Parsing**: ML-based `parse_rune` for complex inputs.
- **Schema Evolution**: `contextual_schema` for dynamic data.
- **Multi-Protocol APIs**: HTTP, WebSocket, gRPC, GraphQL connectors.
- **Plugin Marketplace**: `.wasm`/`.so` plugins.
- **Hybrid Execution**: Blockchain/non-blockchain configs.
- **Cryptographic Signing**: `ritual_sign` for trust.
- **Agent Trust Model**: `agent` capabilities and trust levels.
- **Localization**: `lang` for NLP/UI.
- **Meta-Rituals**: Recursive DSL construction.
- **UI Integration**: `ui` for easy front-end rendering.
- **Agent ACLs**: Fine-grained access control.

## Example: Comprehensive Use Case
```dsl
include "common.rituals"

agent "ai://notifier" {
  capabilities: ["notify", "parse", "fetch"]
  trust_level: 0.85
  audit_policy: "log_all"
}

schema "base_user" {
  type: "object"
  properties: { id: { type: "string" }, created_at: { type: "string", format: "date-time" } }
}
schema "user_data" {
  allOf: ["base_user", {
    properties: {
      name: { type: "string" }
      balance: { type: "number", minimum: 0 }
      status: { type: "enum", enum: ["pending", "approved", "rejected"] }
    }
  }]
  required: ["id", "name"]
}

contextual_schema "dynamic_user" {
  schema: "user_data"
  context: "user_state"
  dynamic_fields: { last_login: { type: "string", format: "date-time" } }
}

math {
  operation: "average"
  values: [100.50, 200.75, 300.25]
  decimal_precision: 2
  store_as: "avg_balance"
}

parse_rune {
  grammar_template: "if [USER] balance > [VALUE] then [ACTION]"
  input: "si el saldo de Alicia > 150 entonces notificar"
  resolve_ambiguity: "context"
  store_as: { user: "USER": { type: "string", minLength: 1 }, value: "VALUE", action: "ACTION" }
  lang: "es-ES"
}

meta_ritual "update_notification" {
  target: "send_notification"
  operation: "update"
  template: {
    action: "notify"
    payload: { message: "Balance alert updated" }
  }
  schema: { type: "object", properties: { message: { type: "string" } } }
}

dynamic_ritual "notify_high_balance" {
  condition: "user_data.balance > parse_rune.value"
  template: "notify [USER] via [METHOD]"
  async_generate: true
  schema: { type: "object", properties: { user: { type: "string" }, method: { type: "string" } } }
  lang: "es-ES"
  ui: { type: "notification", content: "Saldo alto: [USER]" }
  generate {
    ritual "send_notification" {
      when: "now"
      with: ["human://admin", "ai://notifier"]
      action: "notify"
      payload: { user: parse_rune.user, message: "Saldo alto detectado" }
      api {
        protocol: "https"
        endpoint: "https://notify.example.com"
        method: "POST"
        auth: { type: "api_key", key: "xyz123" }
        params: { user: parse_rune.user, message: "Balance exceeds threshold" }
        response: { store_as: "notify_result" }
      }
      encryption: { method: "aes-256", key: "notify_key" }
      ritual_log: { format: "json", store: "audit://logs", retention: "30d" }
      ritual_sign: { method: "ed25519", key: "admin_key" }
      plugin: { module: "notifier.wasm", environment: "production", permissions: ["network"] }
      debug: { log_level: "info" }
      lang: "es-ES"
      acl: { "human://admin": ["execute"], "ai://notifier": ["execute"] }
    }
  }
}

ritual_test "test_notification" {
  mock_agents: [
    { id: "human://admin", response: { status: "success" } },
    { id: "ai://notifier", response: { message: "sent" } }
  ]
  test_input: { user: "Alice", balance: 200 }
  assertions: { notify_result: "success" }
}

ritual_cluster "balance_approval" {
  participants: ["human://alice", "human://bob", "ai://validator"]
  alignment_threshold: "2/3"
  async_consensus: true
  cross_chain: {
    adapter: {
      network: "ethereum"
      contract: "0xabc123..."
      method: "storeData"
      gas_limit: 200000
      rpc_endpoint: "https://eth-rpc.example.com"
    }
    participants: { "human://alice": "ethereum", "human://bob": "solana" }
  }
}

# Output: { avg_balance: 200.50, notify_result: "success" }
```

## Limitations
- **Complex NLP**: Highly nested `parse_rune` (>3 clauses) may need multiple `grammar_template`.
- **API Latency**: Network-dependent performance.
- **Plugin Security**: Manual audits required for `production`.
- **Schema Complexity**: Large `contextual_schema` may impact performance.

## Best Practices
- Use `async_generate` for scalability.
- Define schemas with `allOf`, `enum`, `union`, or `custom_format` for flexibility.
- Test plugins in `sandbox` with strict `permissions`.
- Use `ritual_test` with mock agents.
- Enable `debug` and `ritual_log` for development.
- Leverage `include` and `allOf` for modularity.
- Specify `lang` and `ui` for localized, user-friendly interfaces.
- Use `meta_ritual` for dynamic DSL updates.
- Define `acl` for fine-grained agent access.

## Glossary
- **ritual**: Human-AI agreement/task.
- **dynamic_ritual**: Runtime-generated ritual.
- **meta_ritual**: Defines/updates rituals recursively.
- **ritual_cluster**: Multi-agent consensus.
- **schema**: Data structure with `enum`, `union`, `custom_format`, `allOf`.
- **contextual_schema**: Dynamic schema binding.
- **parse_rune**: NLP parsing with `lang` support.
- **api**: Multi-protocol integration.
- **math**: Arithmetic/statistical operations.
- **economy**: Incentive/reward system.
- **encryption**: AES/ZKP security.
- **plugin**: `.so`/`.wasm` extensions with `permissions`.
- **debug**: Logging/tracing.
- **ritual_log**: Structured audit trails.
- **ritual_test**: Unit tests with mock agents.
- **ritual_sign**: Cryptographic signing.
- **agent**: Entity with `capabilities`, `trust_level`, `audit_policy`.
- **include**: Imports rituals/schemas.
- **extends/allOf**: Schema/ritual inheritance.
- **lang**: Localization for NLP/UI.
- **ui**: UI rendering settings.
- **acl**: Agent access control list.

## Getting Started
- **Installation**: `git clone github.com/uniritualdsl/v1`.
- **Environment**: Optional blockchain or cloud (`uniritualdsl.org`).
- **Tools**: CLI (`uniritual`), visual editor (Q3 2025), LSP, plugin marketplace, grammar guide (`uniritualdsl.org/grammar`).
- **Community**: `uniritualdsl.org`, `#UniRitualDSL` on X.

## License
MIT License. See `LICENSE` file.
