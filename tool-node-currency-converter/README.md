# LLM Function Calling - Currency Converter

This is a serverless function for converting currency from USD to other currencies and vice versa.

You can grab your api-key from [Exchange Rate API](https://www.exchangerate-api.com/) for free, then, add it to your `.env` file:

```sh
YOMO_SFN_NAME=my_first_llm_function_tool
YOMO_SFN_ZIPPER=zipper.vivgrid.com:9000
YOMO_SFN_CREDENTIAL=<your-yomo-sfn-credential>
OPENEXCHANGERATES_API_KEY=<your-openexchangerates.org-api-key>
```

Other environment variables can be found in the [vivgrid dashboard](https://dashboard.vivgrid.com/) serverless page

## Development

### 1. Install YoMo CLI

```bash
curl -fsSL https://get.yomo.run | sh
```

Detail usages of the cli can be found on [Doc: YoMo CLI](https://yomo.run/docs/cli).

### 2. Attach this function calling to your LLM Bridge

```bash
yomo run app.ts -n llm-tool-currency-converter
```

### 3. Trigger the function calling

Test in your terminal:

```bash
curl https://api.vivgrid.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  -d '{
    "model": "gpt-4o",
    "messages": [
      {
        "role": "user",
        "content": "I have $10. Can I afford sunglasses that cost 1,499 yen?"
      }
    ]
  }'
```

Based on the real time weather ifo, you may get response like:

```json
{
  "id": "chatcmpl-Acss0I5tuh2ibDWr13E2p0X3LHVrG",
  "object": "chat.completion",
  "created": 1733830748,
  "model": "gpt-4o-2024-08-06",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "With $10, you have approximately 1,510.25 yen (using an exchange rate of about 151.02 JPY per USD). Since the sunglasses cost 1,499 yen, you can afford them."
      },
      "finish_reason": "stop",
      "content_filter_results": {
        "hate": {
          "filtered": false,
          "severity": "safe"
        },
        "self_harm": {
          "filtered": false,
          "severity": "safe"
        },
        "sexual": {
          "filtered": false,
          "severity": "safe"
        },
        "violence": {
          "filtered": false,
          "severity": "safe"
        },
        "jailbreak": {
          "filtered": false,
          "detected": false
        },
        "profanity": {
          "filtered": false,
          "detected": false
        }
      }
    }
  ],
  "usage": {
    "prompt_tokens": 226,
    "completion_tokens": 118,
    "total_tokens": 240,
    "prompt_tokens_details": null,
    "completion_tokens_details": null
  },
  "system_fingerprint": "fp_04751d0b65",
  "prompt_filter_results": [
    {
      "index": 0,
      "content_filter_results": {
        "hate": {
          "filtered": false,
          "severity": "safe"
        },
        "self_harm": {
          "filtered": false,
          "severity": "safe"
        },
        "sexual": {
          "filtered": false,
          "severity": "safe"
        },
        "violence": {
          "filtered": false,
          "severity": "safe"
        },
        "jailbreak": {
          "filtered": false,
          "detected": false
        },
        "profanity": {
          "filtered": false,
          "detected": false
        }
      }
    }
  ]
}
```
