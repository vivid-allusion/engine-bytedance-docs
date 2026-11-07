---
title: "Semantic classification (ai_classify)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-classify"
---

1. ## Definition

`rds_ai.ai_classify` uses chat/LLM models to classify input text into a set of tags provided by the caller and returns the result in a fixed JSONB envelope.

2. ## Syntax

```SQL
rds_ai.ai_classify(
  content text,
  labels jsonb,
  options jsonb DEFAULT '{}'::jsonb,
  model_name text DEFAULT NULL,
  model_args jsonb DEFAULT '{}'::jsonb
) RETURNS jsonb
```

3. ## Parameter

|**Parameter** |**Type** |**Default value** |**Tip** |
|---|---|---|---|
|`content` |`text` |Null |Text to be classified, must not be SQL NULL or empty text. |
|`labels` |`jsonb` |Null |2 to 500 tags. Accepts a string array or an object of "tag name → description". Tag name: 1~100 characters. Description: up to 1,000 characters. |
|`options` |`jsonb` |`{}` |Close control object, which only supports the keys listed in the table below. |
|`model_name` |`text` |SQL NULL |chat/LLM model. Use `ai_query` default model if NULL. |
|`model_args` |`jsonb` |`{}` |Open parameter object passed to model request body. |

### options key

|**Key** |**Default value** |**Tip** |
|---|---|---|
|`version` |`1.0` |Currently only supports string `1.0`. |
|`instructions` |Empty string |Additional classification command. |
|`multilabel` |`false` |Whether to allow returning multiple tags. |
|`enableConfidenceScores` |`false` |Whether to require each tag to return `confidence_score`. |
|`enableRationales` |`false` |Require each tag to return `rationale`. |

Boolean options must use JSON Boolean values `true`/`false`, not strings `\"true\"`/`\"false\"`.

4. ## Return

Return fixed JSONB envelope: `response` is an array of classification results; `metadata.version` is currently `1.0`; `error_message` is JSON null when succeeded. Single\-tag mode returns exactly one element; multi\-tag mode returns one or more elements. Confidence and explanation fields appear only when the corresponding options are enabled.

```JSON
{
  "response": [
    {
      "value": "positive",
      "confidence_score": 0.92,
      "rationale": "The text expresses approval."
    }
  ],
  "metadata": {"version": "1.0"},
  "error_message": null
}
```

5. ## Error behavior

* A parameter error occurs immediately if input, tag, options, or model parameters are invalid, unknown options or boolean option type errors appear.

* An error occurs when the default/explicit model does not exist or the type is incompatible, as well as for common HTTP/authentication/timeout errors.

* If the model returns invalid JSON, tags are outside the set, single/multi\-tag count mismatches, or enabled confidence/explanation fields are missing, it returns `response: null` and a non\-empty `error_message`, not a parameter error.

* Return error envelope when structured output capability is rejected by the model. If automatically injected by the extension, prompt to disable `rds.ai_auto_structured_output` and retry.

* Resource errors like insufficient resources or response size limits will still be thrown directly.

6. ## Sample

* Single\-tag classification with confidence and explanation

```SQL
SELECT rds_ai.ai_classify(
  'classify detailed',
  '{"positive":"favorable","negative":"unfavorable"}'::jsonb,
  '{"instructions":"prefer sentiment","enableConfidenceScores":true,"enableRationales":true}'::jsonb,
  'Doc-Semantic-Chat'
);
```

* Multi\-tag classification

```SQL
SELECT rds_ai.ai_classify(
  'classify multiple',
  '["positive","negative"]'::jsonb,
  '{"multilabel":true}'::jsonb,
  'Doc-Semantic-Chat'
);
```

7. ## Optimization suggestions

Classification quality mainly depends on the clarity of the tag set and tag description. Follow these principles to improve accuracy and reduce ambiguity:

* **Tag semantics are mutually exclusive and boundaries are clear**: Avoid overlapping meaning tags, so each input falls into one clear type as much as possible.

* **Add a description to tags**: Use the "tag name → description" object format to specify the criteria and typical scenarios for each tag, instead of only listing tag names.

* **Cover fallback/outlier cases**: Prepare an explicit "other/unrelated" tag for inputs that do not belong to any target type to avoid forced misclassification by the model.

* **Choose mode as needed**: Enable `multilabel` only when an input can belong to multiple types. Enable `enableConfidenceScores`/`enableRationales` when downstream filtering or manual review is required.

* **Express orientation with instructions**: Write priority judgment preferences (such as "prioritize sentiment polarity") into `instructions` to reduce boundary sample fluctuation.

8. ## Quality metrics

Benchmark results based on public evaluation datasets (QMSum, WikiLingua EN/ZH):

|**Quality dimension** |**Metric** |**Result** |
|---|---|---|
|Availability |Valid output rate |100% |
|Accuracy |Single tag accuracy |81.61%–92.00% |
|Stability |Single tag macro accuracy |80.72%–92.00% |
|Integrity |CLINC150 OOS recall |91.89% |
