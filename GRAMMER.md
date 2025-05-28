# UniRitualDSL v1.0.4 Grammar Documentation

## Overview

This document provides the formal grammar for UniRitualDSL v1.0.4, a domain-specific language (DSL) for defining transparent, secure, and emotionally intelligent human-AI agreements, data schemas, and automated workflows. The grammar is specified using Parsing Expression Grammar (PEG) notation, ensuring a robust foundation for parsing, compiling, and interpreting UniRitualDSL code. It supports advanced features like `emotion`, `self_prompt`, `inward_execution`, `clone_ritual`, `reflect_ritual`, and `shard_execution`, enabling dynamic, empathetic, and scalable workflows across blockchain, cloud, edge, and IoT environments.

The grammar is case-sensitive, whitespace-insensitive (except within strings), and uses A+n notation for extensibility. It integrates with external systems (e.g., Ethereum, IPFS, JSON-LD) and supports emotional intelligence through the `emotion` field.

## Grammar Notation

- **PEG Syntax**:
  - `<-` defines a rule.
  - `/` denotes ordered choice (try first option, then next if it fails).
  - `*` means zero or more repetitions.
  - `+` means one or more repetitions.
  - `?` means optional (zero or one).
  - `&` means positive lookahead (match without consuming).
  - `!` means negative lookahead (fail if matches).
  - Parentheses `()` group expressions.
  - Square brackets `[]` define character classes.
  - Literal strings are enclosed in single quotes `''`.
  - `{ return ... }` specifies semantic actions to build the AST.

- **Conventions**:
  - Rules are written as `RuleName <- Expression`.
  - Non-terminals are CamelCase or snake_case.
  - Terminals are literal strings or character classes.
  - Comments in PEG use `#`.

## Full Grammar

Below is the complete PEG grammar for UniRitualDSL v1.0.4:

```peg
# Top-level structure
Program <- Spacing (Include / Agent / Schema / ContextualSchema / ParseRune / Ritual / DynamicRitual / MetaRitual / RitualCluster / CloneRitual / ReflectRitual / ShardExecution / CompilerDirective)* EndOfFile

# Include directive for modularity
Include <- 'include' String Spacing

# Agent definition
Agent <- 'agent' Identifier '{' AgentField* '}'
AgentField <- (Capabilities / TrustLevel / AuditPolicy) Spacing
Capabilities <- 'capabilities' ':' Array
TrustLevel <- 'trust_level' ':' Number
AuditPolicy <- 'audit_policy' ':' String

# Schema definition
Schema <- 'schema' Identifier '{' SchemaField* '}'
SchemaField <- (Type / Properties / Required / Format / Items / Enum / Union / CustomFormat / AllOf) Spacing
Type <- 'type' ':' String
Properties <- 'properties' ':' '{' Property* '}'
Property <- Identifier ':' Schema
Required <- 'required' ':' Array
Format <- 'format' ':' String
Items <- 'items' ':' Schema
Enum <- 'enum' ':' Array
Union <- 'union' ':' Array
CustomFormat <- 'custom_format' ':' String
AllOf <- 'allOf' ':' Array

# Contextual schema
ContextualSchema <- 'contextual_schema' Identifier '{' ContextualSchemaField* '}'
ContextualSchemaField <- (SchemaRef / Context / DynamicFields) Spacing
SchemaRef <- 'schema' ':' String
Context <- 'context' ':' String
DynamicFields <- 'dynamic_fields' ':' '{' Property* '}'

# Parse rune for natural language processing
ParseRune <- 'parse_rune' '{' ParseRuneField* '}'
ParseRuneField <- (SelfPrompt / GrammarTemplate / Input / ResolveAmbiguity / StoreAs / Lang) Spacing
SelfPrompt <- 'self_prompt' '{' SelfPromptField* '}'
SelfPromptField <- (Trigger / Template / ContextArray / Output / Lang / MaxSuggestions) Spacing
Trigger <- 'trigger' ':' String
Template <- 'template' ':' String
ContextArray <- 'context' ':' Array
Output <- 'output' ':' Object
MaxSuggestions <- 'max_suggestions' ':' Number
GrammarTemplate <- 'grammar_template' ':' String
Input <- 'input' ':' String
ResolveAmbiguity <- 'resolve_ambiguity' ':' String
StoreAs <- 'store_as' ':' String

# Ritual definition
Ritual <- 'ritual' Identifier '{' RitualField* '}'
RitualField <- (Emotion / When / With / Action / Payload / SchemaRef / Validation / OnError / Api / Encryption / RitualLog / RitualSign / Debug / Lang / UI / ACL) Spacing
Emotion <- 'emotion' '{' EmotionField* '}'
EmotionField <- (EmotionType / Intensity / Expression / Transmutation / Target / ContextTrigger / LogisticsUI) Spacing
EmotionType <- 'type' ':' String
Intensity <- 'intensity' ':' Number
Expression <- 'expression' ':' String
Transmutation <- 'transmutation' ':' String
Target <- 'target' ':' String
ContextTrigger <- 'context.trigger' ':' String
LogisticsUI <- 'logistics.ui' ':' Object
When <- 'when' ':' (String / Time)
With <- 'with' ':' Array
Action <- 'action' ':' String
Payload <- 'payload' ':' Object
Validation <- 'validation' ':' Object
OnError <- 'on_error' ':' Object
Api <- 'api' ':' Object
Encryption <- 'encryption' ':' Object
RitualLog <- 'ritual_log' ':' Object
RitualSign <- 'ritual_sign' ':' Object
Debug <- 'debug' ':' Object
UI <- 'ui' ':' Object
ACL <- 'acl' ':' Object

# Dynamic ritual
DynamicRitual <- 'dynamic_ritual' Identifier '{' DynamicRitualField* '}'
DynamicRitualField <- (Condition / Template / AsyncGenerate / ParseRune / SchemaRef / Lang / UI / Emotion) Spacing
Condition <- 'condition' ':' String
AsyncGenerate <- 'async_generate' ':' Boolean
Generate <- 'generate' '{' Ritual '}'

# Meta ritual
MetaRitual <- 'meta_ritual' Identifier '{' MetaRitualField* '}'
MetaRitualField <- (MetaTarget / Operation / InwardExecution / SchemaRef) Spacing
MetaTarget <- 'target' ':' String
Operation <- 'operation' ':' String
InwardExecution <- 'inward_execution' '{' InwardExecutionField* '}'
InwardExecutionField <- (Condition / Modify / SchemaRef / MaxIterations) Spacing
Modify <- 'modify' ':' Object
MaxIterations <- 'max_iterations' ':' Number

# Ritual cluster
RitualCluster <- 'ritual_cluster' Identifier '{' RitualClusterField* '}'
RitualClusterField <- (Participants / AlignmentThreshold / EmotionWeight / AsyncConsensus / CrossChain) Spacing
Participants <- 'participants' ':' Array
AlignmentThreshold <- 'alignment_threshold' ':' String
EmotionWeight <- 'emotion_weight' ':' Object
AsyncConsensus <- 'async_consensus' ':' Boolean
CrossChain <- 'cross_chain' ':' Object

# Clone ritual
CloneRitual <- 'clone_ritual' Identifier '{' CloneRitualField* '}'
CloneRitualField <- (Source / CloneCount / ParamsVariations / Coordination / MergeStrategy) Spacing
Source <- 'source' ':' String
CloneCount <- 'clone_count' ':' Number
ParamsVariations <- 'params_variations' ':' Array
Coordination <- 'coordination' ':' Object
MergeStrategy <- 'merge_strategy' ':' Object

# Reflect ritual
ReflectRitual <- 'reflect_ritual' Identifier '{' ReflectRitualField* '}'
ReflectRitualField <- (ReflectTarget / Metrics / Optimization / RitualLog) Spacing
ReflectTarget <- 'target' ':' String
Metrics <- 'metrics' ':' Array
Optimization <- 'optimization' ':' Object

# Shard execution
ShardExecution <- 'shard_execution' Identifier '{' ShardExecutionField* '}'
ShardExecutionField <- (Task / Domains / ShardingStrategy / Coordination / MergeStrategy / FaultTolerance / RitualLog / RitualSign / UI) Spacing
Task <- 'task' ':' String
Domains <- 'domains' ':' Array
ShardingStrategy <- 'sharding_strategy' ':' Object
FaultTolerance <- 'fault_tolerance' ':' Object

# Compiler directive
CompilerDirective <- 'compiler_directive' '{' CompilerDirectiveField* '}'
CompilerDirectiveField <- (Target / Optimize / Output / Dependencies) Spacing
Target <- 'target' ':' String
Optimize <- 'optimize' ':' Object
Output <- 'output' ':' String
Dependencies <- 'dependencies' ':' Array

# Basic types
Identifier <- [a-zA-Z_][a-zA-Z0-9_]* { return text(); }
String <- '"' [^"]* '"' { return text().slice(1, -1); }
Number <- ('-'? [0-9]+ ('.' [0-9]+)? ('e' '-'? [0-9]+)?) { return parseFloat(text()); }
Boolean <- 'true' / 'false' { return text() === 'true'; }
Time <- String # ISO 8601 or relative time (e.g., "5m", "2h30m")
Array <- '[' (Value (',' Value)*)? ']' { return Array.isArray(options.result) ? options.result : []; }
Object <- '{' (KeyValue (',' KeyValue)*)? '}' { return options.result || {}; }
KeyValue <- Identifier ':' Value
Value <- String / Number / Boolean / Array / Object / Time
Spacing <- [ \t\n\r]* # Whitespace-insensitive
EndOfFile <- !.
Comment <- '#' [^\n]* / '###' .*? '###' Spacing
```

## Constraints

The grammar enforces the following constraints:

- **Identifiers**: Alphanumeric with underscores, no leading digits (e.g., `user_123`).
- **Strings**: Double-quoted (e.g., `"Hello, World!"`).
- **Numbers**: Integers (`42`), decimals (`3.14`), scientific notation (`1.0e-10`).
- **Booleans**: `true`, `false`.
- **Time Formats**: ISO 8601 (`"2025-05-28T20:20:00+02:00"`) or relative (`"5m"`, `"2h30m"`).
- **Agents**: URI-style (e.g., `human://alice`, `ai://bot1`).
- **Alignment Threshold**: Fraction (`"2/3"`) or percentage (`"75%"`), `0 < threshold ≤ 1`.
- **Emotion Constraints**:
  - `type`: Predefined (`"joy"`, `"grief"`, etc.) or custom string.
  - `intensity`: Float, `0 ≤ intensity ≤ 1`.
  - `expression`: `"somatic"`, `"symbolic"`, `"visual"`, `"poetic"`, `"haptic"`, or plugin-defined.
  - `transmutation`: Optional; valid emotion type.
  - `target`: `"self"`, `"others"`, `"ai"`, `"collective"`, or agent URI.
  - `context.trigger`: Valid event or symbol (e.g., `"event:task_completed"`).
  - `logistics.ui`: Schema-validated object (e.g., `{ colors: ["#FF0000"], animations: ["fade"] }`).
- **Other Constraints**:
  - `self_prompt.max_suggestions`: 1–10.
  - `inward_execution.max_iterations`: 1–10.
  - `clone_ritual.clone_count`: 1–100.
  - `reflect_ritual.max_optimizations`: 1–5.
  - `shard_execution.domains`: At least one domain required.
  - `fault_tolerance.retry.max_attempts`: 1–5.

## Reserved Keywords

- **Constructs**: `include`, `agent`, `schema`, `contextual_schema`, `parse_rune`, `ritual`, `dynamic_ritual`, `meta_ritual`, `ritual_cluster`, `clone_ritual`, `reflect_ritual`, `shard_execution`, `compiler_directive`.
- **Fields**: `capabilities`, `trust_level`, `audit_policy`, `type`, `properties`, `required`, `format`, `items`, `enum`, `union`, `custom_format`, `allOf`, `schema`, `context`, `dynamic_fields`, `self_prompt`, `trigger`, `template`, `context`, `output`, `max_suggestions`, `grammar_template`, `input`, `resolve_ambiguity`, `store_as`, `lang`, `emotion`, `intensity`, `expression`, `transmutation`, `target`, `context.trigger`, `logistics.ui`, `when`, `with`, `action`, `payload`, `validation`, `on_error`, `api`, `encryption`, `ritual_log`, `ritual_sign`, `debug`, `ui`, `acl`, `condition`, `async_generate`, `generate`, `operation`, `inward_execution`, `modify`, `max_iterations`, `participants`, `alignment_threshold`, `emotion_weight`, `async_consensus`, `cross_chain`, `source`, `clone_count`, `params_variations`, `coordination`, `merge_strategy`, `metrics`, `optimization`, `task`, `domains`, `sharding_strategy`, `fault_tolerance`, `target`, `optimize`, `output`, `dependencies`.

## Semantic Actions

The grammar includes semantic actions (e.g., `{ return ... }`) to build an Abstract Syntax Tree (AST). For example:

- `Identifier`: Returns the matched string.
- `String`: Strips quotes and returns the content.
- `Number`: Parses as a float.
- `Boolean`: Converts to `true` or `false`.
- `Array` and `Object`: Aggregate values into arrays or objects.

The AST can be serialized to JSON-LD for interoperability:

```json
{
  "@context": "http://uniritualdsl.org/schema",
  "@type": "Ritual",
  "name": "welcome_user",
  "fields": {
    "emotion": {
      "type": "joy",
      "intensity": 0.8,
      "expression": "visual"
    },
    "action": "notify"
  }
}
```

## Example Usage

### Simple Ritual with Emotion
```dsl
ritual "welcome_user" {
  when: "now"
  with: ["human://new_user", "ai://notifier"]
  action: "notify"
  payload: { message: "Welcome to UniRitualDSL!" }
  emotion: {
    type: "joy" # Positive emotion
    intensity: 0.7
    expression: "visual"
    target: "self"
    context.trigger: "event:user_joined"
    logistics.ui: { colors: ["#FFD700"], animations: ["sparkle"] }
  }
}
```

**Parsed AST**:
```json
{
  "type": "ritual",
  "name": "welcome_user",
  "fields": [
    { "when": "now" },
    { "with": ["human://new_user", "ai://notifier"] },
    { "action": "notify" },
    { "payload": { "message": "Welcome to UniRitualDSL!" } },
    {
      "emotion": {
        "type": "joy",
        "intensity": 0.7,
        "expression": "visual",
        "target": "self",
        "context.trigger": "event:user_joined",
        "logistics.ui": { "colors": ["#FFD700"], "animations": ["sparkle"] }
      }
    }
  ]
}
```

### DAO Voting
```dsl
schema "vote_data" {
  type: "object"
  properties: {
    proposal_id: { type: "string" }
    vote: { type: "string", enum: ["yes", "no"] }
    emotion: { type: "emotion", properties: { type: { type: "string" }, intensity: { type: "number" } } }
  }
}

ritual_cluster "dao_voting" {
  participants: ["human://alice", "human://bob", "ai://validator"]
  alignment_threshold: "2/3"
  emotion_weight: { source: "emotion.intensity", multiplier: 1.5 }
}

ritual "submit_vote" {
  action: "vote"
  payload: { proposal_id: "prop001", vote: "yes" }
  emotion: {
    type: "trust"
    intensity: 0.8
    expression: "visual"
  }
}
```

## Interoperability

- **Ethereum**: Rituals compile to Solidity smart contracts:
  ```solidity
  function executeRitual(bytes memory payload) public {
    // Parse and execute ritual
  }
  ```
- **IPFS**: Store AST as JSON-LD (`ipfs add ritual.jsonld`).
- **JSON-LD**: Serialize for semantic web compatibility.
- **Parser Implementation**: Use PEG.js or similar (e.g., `const parser = peggy.generate(grammar);`).

## Validation and Error Handling

- **Invalid `emotion.intensity`**:
  ```dsl
  ritual_test "test_emotion" {
    input: { emotion: { type: "joy", intensity: 1.5 } }
    expect: { error: "intensity must be <= 1" }
    action: "validate"
  }
  ```
- **Invalid Domain**:
  ```dsl
  ritual_test "test_shard" {
    input: { task: "generate_art", domains: [{ type: "blockchain", gas_limit: 1000 }] }
    expect: { error: "gas_limit_exceeded" }
    action: "execute"
  }
  ```

## Best Practices

- Use `ritual_test` to validate syntax and constraints.
- Enable `debug: { log_level: "verbose" }` for detailed parsing errors.
- Modularize with `include` for reusable schemas and rituals.
- Validate `emotion` fields with schemas to ensure correct `type` and `intensity`.
- Test interoperability with `uniritual test <file.dsl>`.

## References

- Full grammar and updates: `uniritualdsl.org/grammar`.
- CLI tools: `uniritual parse <file.dsl>`, `uniritual validate <file.dsl>`.
- Community: `#UniRitualDSL` on X, `uniritualdsl.org/community`.

## License

MIT License. See `LICENSE` file.
