---
title: "Semantic extraction (ai_extract)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-extract-ai-extract"
---

1. ## Definition

`rds_ai.ai_extract` uses chat/LLM models to extract structured fields from text based on a schema provided by the caller and returns the result in a fixed JSONB envelope.

2. ## Syntax

```SQL
rds_ai.ai_extract(
  content text,
  schema jsonb,
  options jsonb DEFAULT '{}'::jsonb,
  model_name text DEFAULT NULL,
  model_args jsonb DEFAULT '{}'::jsonb
) RETURNS jsonb
```

3. ## Parameter

|**Parameter** |**Type** |**Default value** |**Tip** |
|---|---|---|---|
|`content` |`text` |Null |Text to extract. SQL NULL returns SQL NULL. Blank text is not allowed. |
|`schema` |`jsonb` |Null |Field definition. Abbreviated available array of strings. Full form supports `string`, `integer`, `number`, `boolean`, `object`, `array`, and `enum`. |
|`options` |`jsonb` |`{}` |Close control object, which only supports the keys listed in the table below. |
|`model_name` |`text` |SQL NULL |chat/LLM model. When NULL, use the `ai_query` default model. |
|`model_args` |`jsonb` |`{}` |Open parameter object passed to model request body. |

### options key

|**Key** |**Default value** |**Tip** |
|---|---|---|
|`version` |`1.0` |Currently only supports string `1.0`. |
|`instructions` |Empty string |Additional extraction instructions. |
|`mode` |Empty string |Pass in the extraction mode string of the prompt, such as `precision`. |
|`enableConfidenceScores` |`false` |Whether to require each leaf value to include `confidence_score`. |

Boolean options must use JSON boolean values. Citations, `enableCitations`, and other unknown keys are currently not supported and will be rejected.

4. ## return

Return fixed JSONB envelope: `response` is an object organized by schema; each leaf field uses `{\"value\": ...}`, adding `confidence_score` when confidence is enabled; `metadata.version` is currently `1.0`; on success, `error_message` is JSON null. `content` returns SQL NULL for the entire function when it is SQL NULL.

5. ## Error behavior

* A parameter error occurs immediately for empty input, invalid schema structure or field type, options or model parameters not being objects, or unknown options.

* An error occurs when the default/explicit model does not exist or the type is incompatible, as well as for common HTTP/authentication/timeout errors.

* When model output is not valid JSON, or value type, enum value, object/array structure, or confidence field does not conform to schema, returns `response: null` with a non\-empty `error_message`.

* When structured output ability is rejected by the model, an error envelope is returned. Resource errors, such as insufficient resources or response size limits, are still thrown directly.

6. ## Sample

* Abbreviated schema

```SQL
SELECT rds_ai.ai_extract(
  'extract simple',
  '["name","city"]'::jsonb,
  '{}'::jsonb,
  'Doc-Semantic-Chat'
);
```

* Schema with type and confidence

```SQL
SELECT rds_ai.ai_extract(
  'extract advanced',
  '{"active":{"type":"boolean"},"score":{"type":"number"},"person":{"type":"object","properties":{"age":{"type":"integer"},"tags":{"type":"array","items":{"type":"string"}}}},"status":{"type":"enum","enum":["active","inactive"]}}'::jsonb,
  '{"mode":"precision","enableConfidenceScores":true}'::jsonb,
  'Doc-Semantic-Chat'
);
```

7. ## Optimization suggestions

The extraction quality mainly depends on the clarity of the schema and instructions. The review shows that most extraction errors or misses result from overly broad schema or unclear field constraints. Follow these principles to significantly improve precision and recall:

* **Narrow the schema as much as possible**: Only declare the fields that are truly needed. The broader the field, the easier it is for the model to extract "legal but unwanted" extra values, lowering precision.

* **Write constraints into the field description**: Specify clearly whether the field requires proper nouns or specific entities, the allowed value boundaries, and exclusion conditions, rather than just providing the field name.

* **Clearly state when original text segments are needed**: Require the extraction of "continuous segments appearing in the original text" in the field description or `instructions` to reduce model reconstruction or generalization.

* **Use options to express orientation**: For precision\-prioritized scenarios, set `mode` (such as `precision`) and supplement with `instructions`. Enable `enableConfidenceScores` when downstream filtering is needed.

* **Divide and conquer**: When field semantics differ greatly, splitting into multiple narrow schema calls often performs more reliably than one large comprehensive schema.

8. ## Quality metrics

Benchmark results based on public test sets (QMSum, WikiLingua EN/ZH):

|**Quality dimension** |**Metric** |**Result** |
|---|---|---|
|Availability |Valid output rate |100% |
|Accuracy |Field accuracy |89.36%–92.44% |
|Integrity |Field recall rate |89.11%–93.49% |
|Integrity |Three\-slice micro summary |90.45% |
|Credibility |Source fidelity |98.16%–99.44% |
