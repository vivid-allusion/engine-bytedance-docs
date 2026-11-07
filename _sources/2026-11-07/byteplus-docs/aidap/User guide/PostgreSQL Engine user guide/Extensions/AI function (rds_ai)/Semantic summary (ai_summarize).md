---
title: "Semantic summary (ai_summarize)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-summary-ai-summarize"
---

1. ## Definition

`rds_ai.ai_summarize` compresses input text into a summary with a specified maximum word count using a chat/LLM model.

2. ## Syntax

```SQL
rds_ai.ai_summarize(
  content text,
  max_words integer DEFAULT 50,
  model_name text DEFAULT NULL,
  model_args jsonb DEFAULT '{}'::jsonb
) RETURNS text
```

3. ## Parameter

|**Parameter** |**Type** |**Default value** |**Tip** |
|---|---|---|---|
|`content` |`text` |Null |Text to be summarized. SQL NULL returns SQL NULL. Blank text is not allowed. |
|`max_words` |`integer` |`50` |Expected maximum word count, must be greater than or equal to 0. `0` means no word count limit is set. |
|`model_name` |`text` |SQL NULL |chat/LLM model. Use `ai_query` default model if NULL. |
|`model_args` |`jsonb` |`{}` |Parameter object passed to the model request body. |

4. ## Return

Returns summary text. It returns SQL NULL if `content` is SQL NULL. `max_words` is a constraint for writing prompts. Actual model output depends on the model's compliance.

5. ## Error behavior

* `content` throws a parameter error if it contains only whitespace, `max_words` is NULL or negative, or `model_args` is not a JSON object.

* `model_name` throws an error if it is an empty string, or if the default/explicit model does not exist or has an incompatible type.

* HTTP, allowlist, timeout, response parsing, concurrency, and token quota errors propagate according to the behavior of `ai_query`.

6. ## Sample

```SQL
SELECT rds_ai.ai_summarize(
  'The team approved the release.',
  5,
  'Doc-Chat',
  '{"temperature":0}'::jsonb
);
```

7. ## Optimization suggestions

Summary quality mainly depends on expressing the "key point scope" and "length constraints". Follow these principles to improve coverage and controllability:

* **Set max_words reasonably**: Too small sacrifices coverage; too large dilutes focus; choose values based on target use (single\-sentence summary vs. paragraph summary); pass `0` to indicate no limit.

* **Use model_args to express focal points**: When you need a specific topic/role/conclusion, add the focus in the input via model parameters or upstream concatenation, making the summary more aligned with intent.

* **Maintain language consistency**: Default summary language follows the input; cross\-language requirements should explicitly specify the target language in the input.

* **Faithfulness priority**: Summary must not fabricate information absent from the original text. For fact\-heavy texts, lowering `temperature` can improve stability and faithfulness.

8. ## Quality metrics

Benchmark results based on public evaluation datasets (QMSum, WikiLingua EN/ZH):

|**Quality dimension** |**Metric** |**Result** |
|---|---|---|
|Completeness |Coverage |QMSum 79.89%–83.56%；WikiLingua EN 87.50%–91.88%；ZH 85.00%–90.00% |
|Authenticity |Loyalty |QMSum 96.67%–97.33%；EN 100%；ZH 95.00%–98.00% |
|Focus |Relevance |QMSum 96.89%–98.67%；EN/ZH 100% |
|Controllability |Length compliance rate |99.50%（1194/1200） |
|Auxiliary |Output efficiency |All three rounds are 100% |
|Auxiliary |Language consistency |99.83%（1198/1200） |
