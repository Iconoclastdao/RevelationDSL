# UniRitualDSL v1.0.4 Documentation 

## Introduction

UniRitualDSL v1.0.4 is a domain-agnostic DSL for transparent, secure, and scalable human-AI agreements, schema-driven data modeling, and task automation. It extends v1.0.3 with advanced AI coding capabilities (self-prompting, inward code execution, self-cloning, self-reflection, sharded execution) and introduces a new `emotion` field to enable emotionally intelligent rituals. The `emotion` field supports dynamic scaling, controlled randomness, and meta-cycles of emotional transformation, making it a powerful solution for creative, empathetic, and adaptive workflows. Merging RevelationDSL’s sovereignty and blockchain capabilities with Universal DSL Schema’s flexible schema design, it supports blockchain, IoT, enterprise workflows, AI-driven automation, and emotionally resonant applications. New in v1.0.4: `self_prompt`, `inward_execution`, `clone_ritual`, `reflect_ritual`, `shard_execution`, the `emotion` field, enhanced risk mitigations, and expanded use cases.

## Design Principles

- **Sovereignty**: Equal agency for humans and AI via opt-in rituals and trust thresholds.
- **Transparency**: Cryptographically signed, tamper-proof audit trails.
- **Inclusivity**: Multi-language NLP and UI for global accessibility, enhanced by emotional intelligence.
- **Flexibility**: Advanced schema types, dynamic rituals, and emotional scaling.
- **Extensibility**: Secure plugins (.wasm/.so), sharded execution, and emotional meta-cycles.
- **Accessibility**: Low-code interfaces, visual editor, and emotionally expressive UI.
- **Reliability**: Robust validation, testing, and fault tolerance.
- **Security**: End-to-end encryption, zero-knowledge proofs (ZKP), and agent ACLs.
- **Interoperability**: Multi-protocol APIs (HTTP, WebSocket, gRPC, GraphQL) and multi-runtime environments (blockchain, cloud, edge, IoT).
- **Performance**: Asynchronous processing, sharded computation, and self-optimizing rituals.
- **Adaptability**: Self-prompting, self-modifying, self-reflective, and emotionally responsive capabilities.
- **Emotional Intelligence**: Rituals scale and adapt based on emotional weight, enabling creative randomness and transformation.

## Syntax and Structure

- **Formal Structure**: A+n, case-sensitive, whitespace-insensitive (except strings).
- **Delimiters**: Blocks `{}`, lists `[]`, key-value pairs `:`.
- **Comments**: Single-line `#`, multi-line `### ###`.
- **Identifiers**: Alphanumeric, underscores, no leading digits (e.g., `user_123`).
- **Strings**: Double quotes `""` (e.g., `"Hello, World!"`).
- **Numbers**: Integers (e.g., `42`), decimals (e.g., `3.14`), scientific notation (e.g., `1.0e-10`).
- **Booleans**: `true`, `false`.
- **Time Formats**: ISO 8601 (e.g., `"2025-05-28T20:20:00+02:00"`) or relative (e.g., `"5m"`, `"2h30m"`).
- **Agents**: URI-style (e.g., `human://alice`, `ai://bot1`, `group://team1`).
- **Alignment Threshold**: Fraction (e.g., `"2/3"`) or percentage (e.g., `"75%"`), `0 < threshold ≤ 1`.

## Core Constructs

### `emotion` (New)

Enables rituals to incorporate emotional intelligence, scaling behavior based on emotional weight, introducing controlled randomness, and supporting meta-cycles of emotional transformation.

- **Fields**:
  - `type`: Emotion type (e.g., `"joy"`, `"grief"`, `"rage"`, `"love"`, `"awe"`, `"forgiveness"`).
  - `intensity`: Float (0–1) indicating emotional weight; higher values amplify ritual impact or randomness.
  - `expression`: Rendering method (e.g., `"somatic"`, `"symbolic"`, `"visual"`, `"poetic"`, `"haptic"`).
  - `transmutation`: Target emotion after transformation (e.g., `"grief"` → `"rebirth"`), enabling meta-cycles.
  - `target`: Recipient of emotion (e.g., `"self"`, `"others"`, `"ai"`, `"collective"`).
  - `context.trigger`: Event, symbol, or interaction invoking the emotion (e.g., `"event:task_completed"`, `"symbol:sunrise"`).
  - `logistics.ui`: Guides UI rendering (e.g., colors, animations, audio) for frontend agents or XR/VR renderers.
- **Constraints**:
  - `type`: Must be a predefined or custom emotion string.
  - `intensity`: 0 ≤ intensity ≤ 1.
  - `expression`: Must be a supported method; custom expressions require plugin support.
  - `transmutation`: Optional; must be a valid emotion type.
  - `target`: Must be `"self"`, `"others"`, `"ai"`, `"collective"`, or a specific agent URI.
  - `context.trigger`: Must reference a valid event, symbol, or interaction.
  - `logistics.ui`: Schema-validated UI settings (e.g., `{ colors: ["#FF0000"], animations: ["fade"] }`).
- **Example**:
  ```dsl
  emotion {
    type: "joy"
    intensity: 0.8
    expression: "visual"
    transmutation: "awe"
    target: "collective"
    context.trigger: "event:project_completed"
    logistics.ui: { colors: ["#FFD700"], animations: ["sparkle"], audio: "celebration.mp3" }
  }
  ```
- **Purpose**: Scales ritual behavior (e.g., amplify notifications for high `intensity`), introduces randomness (e.g., varied `expression` for creativity), and supports emotional meta-cycles (e.g., transforming `grief` to `rebirth`).

### `ritual`

Defines a human-AI agreement or task, now supporting `emotion`.

- **Fields** (New/Updated):
  - `emotion`: Optional; defines emotional context and behavior.
  - Other fields: `when`, `with`, `action`, `payload`, `schema`, `validation`, `on_error`, `api`, `encryption`, `ritual_log`, `ritual_sign`, `debug`, `lang`, `ui`, `acl`.
- **Example**:
  ```dsl
  ritual "celebrate_milestone" {
    when: "2025-05-28T20:20:00+02:00"
    with: ["human://alice", "ai://notifier"]
    action: "notify"
    payload: { message: "Project milestone achieved!" }
    emotion: {
      type: "joy"
      intensity: 0.9
      expression: "visual"
      transmutation: "awe"
      target: "collective"
      context.trigger: "event:milestone_achieved"
      logistics.ui: { colors: ["#FFD700"], animations: ["fireworks"] }
    }
    schema: "notification_data"
    validation: { required: ["message"] }
    on_error: { escalate: "admin://support" }
    encryption: { method: "aes-256", key: "secure_key_123" }
    ritual_log: { format: "json", store: "audit://logs", retention: "30d" }
    ritual_sign: { method: "ed25519", key: "alice_key" }
    debug: { log_level: "verbose" }
    lang: "en-US"
    ui: { type: "notification", content: "payload.message" }
    acl: { "human://alice": ["read", "write"], "ai://notifier": ["execute"] }
  }
  ```

### `dynamic_ritual`

Generates rituals at runtime, asynchronously, with `emotion` support.

- **Fields** (New/Updated):
  - `emotion`: Optional; influences generated ritual’s emotional context.
  - Other fields: `condition`, `template`, `async_generate`, `parse_rune`, `schema`, `lang`, `ui`.
- **Example**:
  ```dsl
  dynamic_ritual "dynamic_notification" {
    condition: "api.project_status == 'completed'"
    template: "notify [USER] with [MESSAGE]"
    async_generate: true
    emotion: {
      type: "joy"
      intensity: 0.7
      expression: "poetic"
      target: "others"
      context.trigger: "event:project_completed"
      logistics.ui: { colors: ["#00FF00"], animations: ["pulse"] }
    }
    parse_rune {
      grammar_template: "notify [USER] with [MESSAGE]"
      input: "notify Alice with 'Great job!'"
      resolve_ambiguity: "context"
      lang: "en-US"
    }
    schema: { type: "object", properties: { user: { type: "string" }, message: { type: "string" } } }
    ui: { type: "notification", content: "parse_rune.message" }
    generate {
      ritual "send_notification" {
        when: "now"
        action: "notify"
        payload: { user: parse_rune.user, message: parse_rune.message }
        emotion: { type: "joy", intensity: 0.7, expression: "poetic", target: "others" }
      }
    }
  }
  ```

### `meta_ritual`

Defines or updates rituals at runtime with recursive DSL construction, now supporting `emotion`.

- **Fields** (New/Updated):
  - `inward_execution`: Self-modification rules, now supports `emotion` for emotionally driven updates.
  - Other fields: `target`, `operation`, `template`, `schema`.
- **Example**:
  ```dsl
  meta_ritual "self_evolving_ritual" {
    target: "self"
    operation: "update"
    inward_execution: {
      condition: "ritual_log.success_rate < 0.8 || emotion.intensity > 0.9"
      modify: {
        payload: { retry_count: "payload.retry_count + 1" }
        emotion: { type: "effort", intensity: "emotion.intensity + 0.1", expression: "haptic" }
      }
      schema: { type: "object", properties: { retry_count: { type: "number", minimum: 0 }, emotion: { type: "object" } } }
      max_iterations: 5
    }
  }
  ```

### `ritual_cluster`

Manages multi-agent consensus, with `emotion` influencing consensus weight.

- **Fields** (New/Updated):
  - `emotion_weight`: Optional; adjusts agent priority based on `emotion.intensity`.
  - Other fields: `participants`, `alignment_threshold`, `cluster_priority`, `async_consensus`, `cross_chain`.
- **Example**:
  ```dsl
  ritual_cluster "team_decision" {
    participants: ["human://alice", "human://bob", "ai://validator"]
    alignment_threshold: "2/3"
    emotion_weight: { source: "emotion.intensity", multiplier: 1.5 }
    async_consensus: true
  }
  ```

### `schema`

Defines data structures, now supporting `emotion` types.

- **Fields** (Updated):
  - `type`: Added `"emotion"` as a valid type.
  - Other fields: `properties`, `required`, `format`, `items`, `enum`, `union`, `custom_format`, `allOf`.
- **Example**:
  ```dsl
  schema "emotion_data" {
    type: "object"
    properties: {
      emotion: {
        type: "emotion"
        properties: {
          type: { type: "string", enum: ["joy", "grief", "rage", "love", "awe", "forgiveness"] }
          intensity: { type: "number", minimum: 0, maximum: 1 }
          expression: { type: "string", enum: ["somatic", "symbolic", "visual", "poetic", "haptic"] }
        }
      }
    }
  }
  ```

### `contextual_schema`

Binds schemas to runtime state, now supporting `emotion` dynamics.

- **Fields** (Updated):
  - `dynamic_fields`: Can include `emotion` properties.
  - Other fields: `schema`, `context`.
- **Example**:
  ```dsl
  contextual_schema "dynamic_user" {
    schema: "user_data"
    context: "user_state"
    dynamic_fields: { emotion: { type: "emotion", properties: { type: { type: "string" }, intensity: { type: "number" } } } }
  }
  ```

### `parse_rune`

Parses natural language with localization, enhanced with `emotion` for context-aware prompting.

- **Fields** (Updated):
  - `self_prompt`: Now supports `emotion` to trigger emotionally relevant suggestions.
  - Other fields: `grammar_template`, `input`, `resolve_ambiguity`, `store_as`, `lang`.
- **Example**:
  ```dsl
  parse_rune {
    self_prompt: {
      trigger: "contextual_schema.user_state.activity == 'idle' && emotion.type == 'grief'"
      template: "Suggest [ACTION] for [USER] to transmute [EMOTION]"
      context: ["user_state", "ritual_log", "emotion"]
      output: { action: "ACTION", user: "USER", emotion: "EMOTION" }
      lang: "en-US"
      max_suggestions: 3
    }
  }
  ```

### `clone_ritual` (New)

Enables self-cloning for parallel execution, with `emotion` influencing clone variations.

- **Fields** (Updated):
  - `params_variations`: Can include `emotion` for emotionally varied clones.
  - Other fields: `source`, `clone_count`, `coordination`, `merge_strategy`.
- **Example**:
  ```dsl
  clone_ritual "parallel_art_generation" {
    source: "generate_art"
    clone_count: 4
    params_variations: [
      { emotion: { type: "joy", intensity: 0.8, expression: "visual" } },
      { emotion: { type: "grief", intensity: 0.6, expression: "poetic" } },
      { emotion: { type: "rage", intensity: 0.7, expression: "somatic" } },
      { emotion: { type: "awe", intensity: 0.9, expression: "haptic" } }
    ]
    coordination: {
      ritual_cluster: {
        participants: ["ai://artist1", "ai://artist2", "ai://artist3", "ai://artist4"]
        alignment_threshold: "1/1"
        async_consensus: true
      }
    }
    merge_strategy: {
      method: "aggregate"
      store_as: "art_collection"
      schema: { type: "array", items: { type: "object" } }
    }
  }
  ```

### `reflect_ritual` (New)

Enables self-reflection and optimization, now incorporating `emotion` metrics.

- **Fields** (Updated):
  - `metrics`: Can include `emotion.intensity` or `emotion.type` for emotional optimization.
  - Other fields: `target`, `optimization`, `ritual_log`.
- **Example**:
  ```dsl
  reflect_ritual "optimize_art_generation" {
    target: "generate_art"
    metrics: [
      { name: "emotion_impact", source: "emotion.intensity", threshold: "0.7" },
      { name: "success_rate", source: "ritual_log.success_count / ritual_log.total", threshold: "0.9" }
    ]
    optimization: {
      condition: "metrics.emotion_impact < 0.7 || metrics.success_rate < 0.9"
      action: {
        update: {
          emotion: { expression: "visual", intensity: "emotion.intensity + 0.2" }
          api: { endpoint: "https://faster.art.api" }
        }
      }
      schema: { type: "object", properties: { expression: { type: "string" }, intensity: { type: "number" } } }
      max_optimizations: 3
    }
    ritual_log: { format: "json", store: "audit://optimization_logs", retention: "90d" }
  }
  ```

### `shard_execution` (New)

Distributes computation across interoperable domains, with `emotion` influencing task allocation.

- **Fields** (Updated):
  - `sharding_strategy`: Can use `emotion.intensity` to weight domain assignments.
  - Other fields: `task`, `domains`, `coordination`, `merge_strategy`, `fault_tolerance`, `ritual_log`, `ritual_sign`.
- **Example**:
  ```dsl
  shard_execution "distributed_art_computation" {
    task: "generate_art"
    domains: [
      { type: "blockchain", network: "ethereum", contract: "0xabc123...", gas_limit: 500000 },
      { type: "cloud", endpoint: "https://cloud.compute.example.com", auth: { type: "api_key", key: "cloud_key" } },
      { type: "edge", plugin: "art.wasm", environment: "sandbox", permissions: ["compute"] },
      { type: "iot", endpoint: "mqtt://iot.device.local", topic: "art_tasks" }
    ]
    sharding_strategy: {
      method: "divide_and_conquer"
      split: { input_size: "payload.art_size", chunks: 4 }
      assign: { domain_weights: { blockchain: "emotion.intensity * 0.2", cloud: "emotion.intensity * 0.5", edge: 0.2, iot: 0.1 } }
    }
    coordination: {
      ritual_cluster: {
        participants: ["ai://coordinator", "blockchain://eth_node", "cloud://compute_node", "edge://device1", "iot://sensor1"]
        alignment_threshold: "1/1"
        async_consensus: true
      }
    }
    merge_strategy: {
      method: "aggregate"
      store_as: "art_result"
      schema: { type: "array", items: { type: "object" } }
    }
    fault_tolerance: {
      retry: { max_attempts: 3, delay: "5s" }
      fallback: { domain: "cloud", endpoint: "https://backup.compute.example.com" }
    }
    ritual_log: { format: "json", store: "audit://compute_logs", retention: "60d" }
    ritual_sign: { method: "ed25519", key: "coordinator_key" }
  }
  ```

### `api`, `math`, `economy`, `encryption`, `plugin`, `debug`, `ritual_log`, `ritual_test`, `ritual_sign`, `agent`

- **Fields**: Unchanged from v1.0.3, with `emotion` integration where applicable (e.g., `api` can fetch emotional data, `economy` can reward based on `emotion.intensity`).
- **Examples**: See v1.0.3 documentation.

## Syntax Rules

- **New Reserved Keywords**: `emotion`, `type`, `intensity`, `expression`, `transmutation`, `target`, `context.trigger`, `logistics.ui`, `emotion_weight`.
- **Constraints**:
  - `emotion.type`: Predefined or custom emotion string.
  - `emotion.intensity`: 0 ≤ intensity ≤ 1.
  - `emotion.expression`: Supported methods or plugin-defined.
  - `emotion.transmutation`: Optional; valid emotion type.
  - `emotion.target`: `"self"`, `"others"`, `"ai"`, `"collective"`, or agent URI.
  - `emotion.context.trigger`: Valid event, symbol, or interaction.
  - `emotion.logistics.ui`: Schema-validated UI settings.
  - `self_prompt.max_suggestions`: 1–10.
  - `inward_execution.max_iterations`: 1–10.
  - `clone_ritual.clone_count`: 1–100.
  - `reflect_ritual.max_optimizations`: 1–5.
  - `shard_execution.domains`: At least one domain required.
  - `fault_tolerance.retry.max_attempts`: 1–5.
- **Other Rules**: Unchanged from v1.0.3.

## Role of `emotion` in Introducing Randomness and More

The `emotion` field enhances UniRitualDSL by:

- **Scaling Behavior**: `intensity` (0–1) amplifies ritual actions (e.g., higher notification frequency for `joy` with `intensity: 0.9`).
- **Controlled Randomness**: `expression` introduces variability (e.g., random visual styles for `"visual"` expression), with `intensity` modulating randomness degree (e.g., higher intensity → more diverse outputs).
- **Emotional Meta-Cycles**: `transmutation` enables rituals to evolve emotions (e.g., `grief` → `rebirth`), creating adaptive workflows.
- **Context-Aware Triggers**: `context.trigger` ties emotions to events or symbols, ensuring relevance.
- **Expressive Rendering**: `logistics.ui` customizes outputs for XR/VR, enhancing user engagement.
- **Solution to All**: By integrating emotional intelligence, `emotion` enables creative, empathetic, and adaptive applications, from art generation to mental health support, making rituals more human-centric and dynamic.

## Risk Mitigation Strategies

1. **Complexity Risk** (Self-Modifying/Reflective/Emotional Systems):
   - **Mitigation**: Enforce `max_iterations`, `max_optimizations`, and `max_suggestions` to limit cycles. Use `ritual_test` with mock agents to validate emotional behaviors.
   - **Example**: `inward_execution { max_iterations: 5 }`, `emotion { intensity: 0.8 }`.
2. **Security Risk** (Plugins/Self-Modifying Code/Emotional Data):
   - **Mitigation**: Require `sandbox` for plugins and emotional expressions, with strict `permissions`. Use `ritual_sign` for verifiable changes and `uniritual audit` for vulnerability scanning. Encrypt emotional data with `encryption`.
   - **Example**: `plugin { environment: "sandbox", permissions: ["compute"] }`, `emotion { encryption: { method: "zkp" } }`.
3. **Performance Risk** (Sharded Execution/Emotional Rendering):
   - **Mitigation**: Implement `fault_tolerance` with retries and fallbacks. Use `async_generate` and `async_consensus` for scalability. Optimize `logistics.ui` rendering with lightweight schemas.
   - **Example**: `fault_tolerance { retry: { max_attempts: 3, delay: "5s" } }`, `logistics.ui: { animations: ["lightweight_fade"] }`.
4. **Interoperability Risk** (Heterogeneous Domains):
   - **Mitigation**: Use `ritual_cluster` for coordination and schema-validated `merge_strategy`. Validate `emotion` across domains with `schema`.
   - **Example**: `merge_strategy { method: "aggregate", schema: { type: "array" } }`.
5. **Trust/Consent Risk** (AI Autonomy/Emotional Manipulation):
   - **Mitigation**: Require `acl` and `trust_level` for AI-driven emotional actions. Use `ui` for user approval of `self_prompt` and `emotion` outputs. Log all actions via `ritual_log`.
   - **Example**: `acl { "human://alice": ["approve"], "ai://bot": ["suggest"] }`, `emotion { target: "self", logistics.ui: { content: "Approve this action?" } }`.
6. **Emotional Bias Risk**:
   - **Mitigation**: Use `reflect_ritual` to monitor `emotion.intensity` and `type` for unintended biases. Validate `transmutation` outcomes with `ritual_test`.
   - **Example**: `reflect_ritual { metrics: [{ name: "emotion_balance", source: "emotion.type", threshold: "balanced" }] }`.

## Tooling Ecosystem

- **CLI Tool**:
  - New Commands:
    - `uniritual optimize <ritual.dsl>`: Simulates `reflect_ritual` and `emotion` optimizations.
    - `uniritual shard <ritual.dsl> --domains <domains.json>`: Tests sharded execution with `emotion` weighting.
    - `uniritual emotion <ritual.dsl> --simulate`: Simulates emotional rendering.
  - Example:
    ```bash
    uniritual optimize art_ritual.dsl
    uniritual shard compute_ritual.dsl --domains domains.json
    uniritual emotion art_ritual.dsl --simulate
    ```
- **Visual Editor**: (Beta Q3 2025) Supports drag-and-drop for `emotion`, `clone_ritual`, and `shard_execution`.
- **Plugin Development**: Added `audit_policy` for emotional plugins and expressions.
- **LSP**: Enhanced with `emotion`, `self_prompt`, `reflect_ritual`, and `shard_execution` autocompletion.
- **Testing Framework**: Supports mocks for emotional, sharded, and cloned rituals.

## Innovative Features

1. **Emotional Intelligence**: `emotion` enables rituals to scale, randomize, and transmute based on emotional weight, enhancing creativity and empathy.
2. **Self-Prompting**: `parse_rune.self_prompt` suggests emotionally relevant tasks, approved via `ui`.
3. **Inward Code Execution**: `meta_ritual.inward_execution` allows emotionally driven self-modification.
4. **Self-Cloning/Parallel Execution**: `clone_ritual` spawns emotionally varied instances, coordinated via `ritual_cluster`.
5. **Self-Reflection/Optimization**: `reflect_ritual` optimizes based on `emotion` and performance metrics.
6. **Sharded Execution**: `shard_execution` distributes tasks with `emotion.intensity` weighting.
7. **Low-Code Interface**: Visual editor for all constructs (Q3 2025).
8. **AI-Driven Parsing**: `parse_rune` with `emotion`-enhanced NLP.
9. **Schema Evolution**: `contextual_schema` for dynamic emotional data.
10. **Multi-Protocol APIs**: HTTP, WebSocket, gRPC, GraphQL support.
11. **Plugin Marketplace**: `.wasm`/`.so` extensions with emotional rendering.
12. **Hybrid Execution**: Blockchain and non-blockchain environments.
13. **Cryptographic Signing**: `ritual_sign` for trust.
14. **Agent Trust Model**: `agent` capabilities and `trust_level`.
15. **Localization**: `lang` for NLP/UI.
16. **UI Integration**: `ui` and `logistics.ui` for emotionally expressive interfaces.
17. **Agent ACLs**: Fine-grained access control.

## What Sets UniRitualDSL v1.0.4 Apart

- **Emotional Intelligence**: `emotion` enables dynamic, empathetic workflows with randomness and transformation, unlike static DSLs (e.g., YAML, Terraform).
- **Adaptive AI Coding**: Self-prompting, self-modification, and self-reflection create autonomous, evolving systems, enhanced by emotional context.
- **Scalable Sharding**: Distributes tasks across heterogeneous domains with `emotion`-weighted assignments, surpassing Kubernetes with trust-aware execution.
- **Trust and Sovereignty**: `acl`, `trust_level`, `ritual_sign`, and `emotion` ensure user consent and transparency, addressing AI autonomy risks absent in platforms like Apache Airflow.
- **Interoperability**: Integrates blockchain, cloud, edge, and IoT, with `emotion` enhancing cross-domain coordination.
- **Auditability**: Cryptographic `ritual_log` ensures verifiable emotional and computational outcomes.
- **Low-Code Accessibility**: `ui`, `logistics.ui`, and visual editor make complex automation accessible, unlike BPMN or n8n.

## New Use Cases

1. **Decentralized Governance**:
   - Rituals for voting and proposals, with `emotion` scaling consensus weight (e.g., `joy` amplifies participation).
   - Example: A DAO uses `clone_ritual` for parallel vote tallying and `emotion { type: "awe", intensity: 0.9 }` to celebrate consensus.
2. **Sovereign AI Assistants**:
   - Self-prompting assistants suggest tasks (e.g., reminders) with `emotion` for empathetic responses, approved via `ui`.
   - Example: An assistant uses `emotion { type: "grief", transmutation: "rebirth" }` to suggest healing actions.
3. **Agent-Orchestrated Workflows**:
   - AI clusters coordinate tasks with `emotion` varying outputs (e.g., creative styles).
   - Example: A supply chain AI uses `clone_ritual` with `emotion { expression: "visual" }` for diverse reports.
4. **Regenerative Finance (ReFi)**:
   - Rituals for staking, with `emotion` influencing reward distribution.
   - Example: A ReFi protocol uses `shard_execution` with `emotion.intensity` to prioritize high-impact investments.
5. **Health & Data Sovereignty**:
   - Opt-in rituals for data sharing, with `emotion` ensuring empathetic handling.
   - Example: A health DAO uses `emotion { type: "forgiveness", expression: "poetic" }` for patient consent dialogs.
6. **AI-Human Legal Agreements**:
   - Rituals codify agreements with `emotion` for emotional alignment.
   - Example: A contract uses `emotion { type: "trust", intensity: 0.8 }` to reinforce compliance.
7. **Edge AI + IoT Coordination**:
   - Rituals coordinate drones with `emotion` for expressive outputs.
   - Example: Agricultural drones use `shard_execution` with `emotion { expression: "haptic" }` for tactile feedback.
8. **Web3 Identity & Reputation**:
   - Rituals track reputation with `emotion` adjusting trust scores.
   - Example: A user’s reputation evolves with `emotion { type: "awe", intensity: 0.9 }` for impactful contributions.
9. **Creative Art Generation**:
   - Rituals generate art with `emotion` driving randomness and style.
   - Example: `clone_ritual` creates varied artworks with `emotion { type: "rage", expression: "visual" }`.

## Comprehensive Example with `emotion`

```dsl
include "common.rituals"

agent "ai://artist" {
  capabilities: ["compute", "notify", "parse", "create"]
  trust_level: 0.9
  audit_policy: "log_all"
}

schema "art_data" {
  type: "object"
  properties: {
    id: { type: "string" }
    style: { type: "string", enum: ["abstract", "realism", "surrealism"] }
    emotion: {
      type: "emotion"
      properties: {
        type: { type: "string", enum: ["joy", "grief", "rage", "awe"] }
        intensity: { type: "number", minimum: 0, maximum: 1 }
        expression: { type: "string", enum: ["visual", "poetic", "haptic"] }
      }
    }
  }
  required: ["id", "style", "emotion"]
}

contextual_schema "dynamic_art" {
  schema: "art_data"
  context: "user_state"
  dynamic_fields: { created_at: { type: "string", format: "date-time" } }
}

parse_rune {
  self_prompt: {
    trigger: "contextual_schema.user_state.mood == 'reflective' && emotion.intensity > 0.5"
    template: "Create [STYLE] art for [USER] expressing [EMOTION]"
    context: ["user_state", "ritual_log", "emotion"]
    output: { style: "STYLE", user: "USER", emotion: "EMOTION" }
    lang: "en-US"
    max_suggestions: 3
  }
}

reflect_ritual "optimize_art" {
  target: "generate_art"
  metrics: [
    { name: "emotion_impact", source: "emotion.intensity", threshold: "0.7" },
    { name: "user_engagement", source: "ritual_log.interaction_count", threshold: "10" }
  ]
  optimization: {
    condition: "metrics.emotion_impact < 0.7 || metrics.user_engagement < 10"
    action: {
      update: {
        emotion: { expression: "poetic", intensity: "emotion.intensity + 0.2" }
        api: { endpoint: "https://creative.api.example.com" }
      }
    }
    schema: { type: "object", properties: { expression: { type: "string" }, intensity: { type: "number" } } }
    max_optimizations: 3
  }
  ritual_log: { format: "json", store: "audit://art_logs", retention: "90d" }
}

clone_ritual "parallel_art_generation" {
  source: "generate_art"
  clone_count: 4
  params_variations: [
    { emotion: { type: "joy", intensity: 0.8, expression: "visual" } },
    { emotion: { type: "grief", intensity: 0.6, expression: "poetic" } },
    { emotion: { type: "rage", intensity: 0.7, expression: "somatic" } },
    { emotion: { type: "awe", intensity: 0.9, expression: "haptic" } }
  ]
  coordination: {
    ritual_cluster: {
      participants: ["ai://artist1", "ai://artist2", "ai://artist3", "ai://artist4"]
      alignment_threshold: "1/1"
      async_consensus: true
    }
  }
  merge_strategy: {
    method: "aggregate"
    store_as: "art_collection"
    schema: { type: "array", items: { type: "object" } }
  }
}

shard_execution "distributed_art_computation" {
  task: "generate_art"
  domains: [
    { type: "blockchain", network: "ethereum", contract: "0xabc123...", gas_limit: 500000 },
    { type: "cloud", endpoint: "https://cloud.compute.example.com", auth: { type: "api_key", key: "cloud_key" } },
    { type: "edge", plugin: "art.wasm", environment: "sandbox", permissions: ["compute"] }
  ]
  sharding_strategy: {
    method: "divide_and_conquer"
    split: { input_size: "payload.art_size", chunks: 3 }
    assign: { domain_weights: { blockchain: "emotion.intensity * 0.2", cloud: "emotion.intensity * 0.5", edge: 0.3 } }
  }
  coordination: {
    ritual_cluster: {
      participants: ["ai://coordinator", "blockchain://eth_node", "cloud://compute_node", "edge://device1"]
      alignment_threshold: "1/1"
      async_consensus: true
    }
  }
  merge_strategy: {
    method: "aggregate"
    store_as: "art_result"
    schema: { type: "array", items: { type: "object" } }
  }
  fault_tolerance: {
    retry: { max_attempts: 3, delay: "5s" }
    fallback: { domain: "cloud", endpoint: "https://backup.compute.example.com" }
  }
  ritual_log: { format: "json", store: "audit://compute_logs", retention: "60d" }
  ritual_sign: { method: "ed25519", key: "coordinator_key" }
  ui: { type: "gallery", content: "art_result" }
}

ritual "generate_art" {
  when: "now"
  with: ["human://alice", "ai://artist"]
  action: "create"
  payload: { id: "art001", style: "abstract", art_size: 1000 }
  emotion: {
    type: "awe"
    intensity: 0.9
    expression: "visual"
    transmutation: "joy"
    target: "collective"
    context.trigger: "event:user_request"
    logistics.ui: { colors: ["#FFD700", "#00FF00"], animations: ["sparkle"] }
  }
  schema: "art_data"
  validation: { required: ["id", "style"] }
  api: { protocol: "https", endpoint: "https://art.api.example.com", method: "POST", params: { style: "payload.style" } }
  on_error: { retry: { max_attempts: 3, delay: "5s" } }
  ui: { type: "preview", content: "api.response.art" }
  acl: { "human://alice": ["approve"], "ai://artist": ["execute"] }
}
```

## Limitations

- **Complex NLP**: Nested `parse_rune.self_prompt` with `emotion` may require multiple templates.
- **Performance**: Sharded execution and emotional rendering may face latency; mitigated by `fault_tolerance` and lightweight `logistics.ui`.
- **Security**: Emotional plugins and self-modifying rituals require strict audits; enforced by `sandbox` and `uniritual audit`.
- **Adoption**: Learning curve for `emotion` and new constructs; mitigated by visual editor and `uniritualdsl.org/grammar`.

## Best Practices

- Use `emotion` with `ui` and `logistics.ui` for expressive, user-approved outputs.
- Limit `inward_execution`, `reflect_ritual`, and `self_prompt` cycles with `max_iterations`, `max_optimizations`, and `max_suggestions`.
- Test `emotion`, `clone_ritual`, and `shard_execution` with `ritual_test`.
- Enable `ritual_log` and `debug` for development.
- Use `include` and `allOf` for modularity.
- Define `acl` for secure agent and emotional access.
- Audit plugins with `uniritual audit` before `production`.

## Getting Started

- **Installation**: `git clone github.com/uniritualdsl/v1`.
- **Environment**: Blockchain, cloud, or local (`uniritualdsl.org`).
- **Tools**: CLI (`uniritual`), visual editor (Q3 2025), LSP, plugin marketplace, grammar guide (`uniritualdsl.org/grammar`).
- **Community**: `uniritualdsl.org`, `#UniRitualDSL` on X.

## License

MIT License. See `LICENSE` file.

## Chart: Emotion-Driven Sharded Workflow

To visualize the `emotion`-enhanced sharded execution, here’s a chart showing task distribution weighted by `emotion.intensity`:

```json
{
  "type": "bar",
  "data": {
    "labels": ["Blockchain", "Cloud", "Edge"],
    "datasets": [{
      "label": "Task Allocation (%)",
      "data": [20, 50, 30],
      "backgroundColor": ["#4CAF50", "#2196F3", "#FF9800"],
      "borderColor": ["#388E3C", "#1976D2", "#F57C00"],
      "borderWidth": 1
    }]
  },
  "options": {
    "scales": {
      "y": {
        "beginAtZero": true,
        "title": { "display": true, "text": "Percentage of Tasks (Emotion-Weighted)" }
      },
      "x": {
        "title": { "display": true, "text": "Domain" }
      }
    },
    "plugins": {
      "title": { "display": true, "text": "Emotion-Driven Sharded Workflow" }
    }
  }
}
```

This chart illustrates how `emotion.intensity` influences `shard_execution`, with cloud receiving 50% of tasks due to high performance, adjusted by emotional weight.

## Conclusion

UniRitualDSL v1.0.4’s `emotion` field transforms rituals into emotionally intelligent, dynamic, and creative workflows, enabling randomness, transformation, and empathy. Combined with self-prompting, inward execution, cloning, reflection, and sharding, it offers a comprehensive solution for adaptive automation. 
