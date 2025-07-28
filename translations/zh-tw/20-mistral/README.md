<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4bd0fafda5d66cd9d60f1ebc7820415e",
  "translation_date": "2025-07-09T18:54:58+00:00",
  "source_file": "20-mistral/README.md",
  "language_code": "zh-tw"
}
-->
# 使用 Mistral 模型建置

## 簡介

本課程將涵蓋：
- 探索不同的 Mistral 模型
- 了解每個模型的使用案例和情境
- 示範每個模型獨特功能的程式碼範例。

## Mistral 模型

在本課程中，我們將探索 3 種不同的 Mistral 模型：
**Mistral Large**、**Mistral Small** 和 **Mistral NeMo**。

這些模型都可以在 Github 模型市集上免費取得。本筆記本中的程式碼將使用這些模型來執行範例。以下是關於使用 Github 模型來[使用 AI 模型進行原型設計](https://docs.github.com/en/github-models/prototyping-with-ai-models?WT.mc_id=academic-105485-koreyst)的更多詳細資訊。


## Mistral Large 2 (2407)
Mistral Large 2 是 Mistral 目前的旗艦模型，專為企業使用而設計。

此模型是原始 Mistral Large 的升級版，提供
- 更大的上下文視窗 - 128k vs 32k
- 在數學和編碼任務上表現更好 - 平均準確度 76.9% vs 60.4%
- 改進的多語言能力 - 支援英語、法語、德語、西班牙語、義大利語、葡萄牙語、荷蘭語、俄語、中文、日語、韓語、阿拉伯語和印地語。

憑藉這些功能，Mistral Large 在以下方面表現出色
- *檢索增強生成 (RAG)* - 歸功於更大的上下文視窗
- *函式呼叫* - 此模型支援原生函式呼叫，可與外部工具和 API 整合。這些呼叫可以並行或依序進行。
- *程式碼生成* - 此模型在 Python、Java、TypeScript 和 C++ 程式碼生成方面表現尤其出色。

### 使用 Mistral Large 2 的 RAG 範例

在此範例中，我們使用 Mistral Large 2 對文字文件執行 RAG 模式。問題以韓語撰寫，詢問作者在大學之前的主要活動。

它使用 Cohere Embeddings Model 為文字文件和問題建立嵌入。在此範例中，faiss Python 套件用作向量儲存。

傳送給 Mistral 模型的提示包含問題和與問題相似的檢索到的區塊。然後模型會產生自然語言回應。

```python
pip install faiss-cpu
```

```python
import requests
import numpy as np
import faiss
import os

from azure.ai.inference import ChatCompletionsClient
from azure.ai.inference.models import SystemMessage, UserMessage
from azure.core.credentials import AzureKeyCredential
from azure.ai.inference import EmbeddingsClient

endpoint = "https://models.inference.ai.azure.com"
model_name = "Mistral-large"
token = os.environ["GITHUB_TOKEN"]

client = ChatCompletionsClient(
    endpoint=endpoint,
    credential=AzureKeyCredential(token),
)

response = requests.get('https://raw.githubusercontent.com/run-llama/llama_index/main/docs/docs/examples/data/paul_graham/paul_graham_essay.txt')
text = response.text

chunk_size = 2048
chunks = [text[i:i + chunk_size] for i in range(0, len(text), chunk_size)]
len(chunks)

embed_model_name = "cohere-embed-v3-multilingual"

embed_client = EmbeddingsClient(
        endpoint=endpoint,
        credential=AzureKeyCredential(token)
)

embed_response = embed_client.embed(
    input=chunks,
    model=embed_model_name
)



text_embeddings = []
for item in embed_response.data:
    length = len(item.embedding)
    text_embeddings.append(item.embedding)
text_embeddings = np.array(text_embeddings)


d = text_embeddings.shape[1]
index = faiss.IndexFlatL2(d)
index.add(text_embeddings)

question = "저자가 대학에 오기 전에 주로 했던 두 가지 일은 무엇이었나요？"

question_embedding = embed_client.embed(
    input=[question],
    model=embed_model_name
)

question_embeddings = np.array(question_embedding.data[0].embedding)


D, I = index.search(question_embeddings.reshape(1, -1), k=2) # 距離，索引
retrieved_chunks = [chunks[i] for i in I.tolist()[0]]

prompt = f"""
上下文資訊如下。
---------------------
{retrieved_chunks}
---------------------
根據上下文資訊，而非先前的知識，回答查詢。
查詢：{question}
答案：
"""


chat_response = client.complete(
    messages=[
        SystemMessage(content="您是一個樂於助人的助理。"),
        UserMessage(content=prompt),
    ],
    temperature=1.0,
    top_p=1.0,
    max_tokens=1000,
    model=model_name
)

print(chat_response.choices[0].message.content)
```

## Mistral Small
Mistral Small 是 Mistral 系列中的另一個模型，定位於頂級/企業類別。顧名思義，這是一個小型語言模型 (SLM)。使用 Mistral Small 的好處包括：
- 與 Mistral Large 和 NeMo 等較大型 Mistral LLM 相比，成本更低 - 便宜高達 80%
- 低延遲 - 比 Mistral 較大型 LLM 更快的響應時間
- 彈性 - 可以在各種環境中部署，資源需求更少。


Mistral Small 非常適合：
- 文字任務，例如摘要、情感分析和翻譯。
- 由於其成本效益，適用於頻繁請求的應用程式
- 低延遲程式碼任務，例如程式碼審查和建議

## 比較 Mistral Small 和 Mistral Large

若要查看 Mistral Small 和 Large 之間的延遲差異，請執行以下儲存格。

您應該會注意到回應時間約有 3-5 秒的差異。此外，請觀察相同提示的回應長度和風格的差異。

```python

import os
endpoint = "https://models.inference.ai.azure.com"
model_name = "Mistral-small"
token = os.environ["GITHUB_TOKEN"]

client = ChatCompletionsClient(
    endpoint=endpoint,
    credential=AzureKeyCredential(token),
)

response = client.complete(
    messages=[
        SystemMessage(content="您是一個樂於助人的程式碼助理。"),
        UserMessage(content="你能寫一個 Python 函式來執行 fizz buzz 測試嗎？"),
    ],
    temperature=1.0,
    top_p=1.0,
    max_tokens=1000,
    model=model_name
)

print(response.choices[0].message.content)

```

```python

import os
from azure.ai.inference import ChatCompletionsClient
from azure.ai.inference.models import SystemMessage, UserMessage
from azure.core.credentials import AzureKeyCredential

endpoint = "https://models.inference.ai.azure.com"
model_name = "Mistral-large"
token = os.environ["GITHUB_TOKEN"]

client = ChatCompletionsClient(
    endpoint=endpoint,
    credential=AzureKeyCredential(token),
)

response = client.complete(
    messages=[
        SystemMessage(content="您是一個樂於助人的程式碼助理。"),
        UserMessage(content="你能寫一個 Python 函式來執行 fizz buzz 測試嗎？"),
    ],
    temperature=1.0,
    top_p=1.0,
    max_tokens=1000,
    model=model_name
)

print(response.choices[0].message.content)

```

## Mistral NeMo

與本課程中討論的其他兩個模型相比，Mistral NeMo 是唯一一個具有 Apache2 授權的免費模型。

它被認為是早期開源 LLM Mistral 7B 的升級版。

NeMo 模型的其他一些功能包括：

- *更高效的權杖化：* 此模型使用 Tekken 權杖化器，而不是更常用的 tiktoken。這使得在更多語言和程式碼中表現更好。

- *微調：* 基礎模型可用於微調，為需要自訂的使用案例提供更大的彈性。

- *原生函式呼叫* - 像 Mistral Large 一樣，此模型已針對函式呼叫進行訓練，使其成為首批支援此功能的開源模型之一。


### 比較權杖化器

在此範例中，我們比較 Mistral NeMo 和 Mistral Large 如何處理權杖化。

兩個範例都使用相同的提示，但您應該會看到 NeMo 傳回的權杖比 Mistral Large 少。

```bash
pip install mistral-common
```

```python
# 匯入所需套件：
from mistral_common.protocol.instruct.messages import (
    UserMessage,
)
from mistral_common.protocol.instruct.request import ChatCompletionRequest
from mistral_common.protocol.instruct.tool_calls import (
    Function,
    Tool,
)
from mistral_common.tokens.tokenizers.mistral import MistralTokenizer

# 載入 Mistral 權杖化器

model_name = "open-mistral-nemo	"

tokenizer = MistralTokenizer.from_model(model_name)

# 權杖化訊息清單
tokenized = tokenizer.encode_chat_completion(
    ChatCompletionRequest(
        tools=[
            Tool(
                function=Function(
                    name="get_current_weather",
                    description="取得目前天氣",
                    parameters={
                        "type": "object",
                        "properties": {
                            "location": {
                                "type": "string",
                                "description": "城市和州，例如舊金山，加利福尼亞州",
                            },
                            "format": {
                                "type": "string",
                                "enum": ["攝氏", "華氏"],
                                "description": "要使用的溫度單位。從使用者位置推斷。",
                            },
                        },
                        "required": ["location", "format"],
                    },
                )
            )
        ],
        messages=[
            UserMessage(content="巴黎今天天氣如何？"),
        ],
        model=model_name,
    )
)
tokens, text = tokenized.tokens, tokenized.text

# 計算權杖數量
print(len(tokens))
```

```python
# 匯入所需套件：
from mistral_common.protocol.instruct.messages import (
    UserMessage,
)
from mistral_common.protocol.instruct.request import ChatCompletionRequest
from mistral_common.protocol.instruct.tool_calls import (
    Function,
    Tool,
)
from mistral_common.tokens.tokenizers.mistral import MistralTokenizer

# 載入 Mistral 權杖化器

model_name = "mistral-large-latest"

tokenizer = MistralTokenizer.from_model(model_name)

# 權杖化訊息清單
tokenized = tokenizer.encode_chat_completion(
    ChatCompletionRequest(
        tools=[
            Tool(
                function=Function(
                    name="get_current_weather",
                    description="取得目前天氣",
                    parameters={
                        "type": "object",
                        "properties": {
                            "location": {
                                "type": "string",
                                "description": "城市和州，例如舊金山，加利福尼亞州",
                            },
                            "format": {
                                "type": "string",
                                "enum": ["攝氏", "華氏"],
                                "description": "要使用的溫度單位。從使用者位置推斷。",
                            },
                        },
                        "required": ["location", "format"],
                    },
                )
            )
        ],
        messages=[
            UserMessage(content="巴黎今天天氣如何？"),
        ],
        model=model_name,
    )
)
tokens, text = tokenized.tokens, tokenized.text

# 計算權杖數量
print(len(tokens))
```

## 學習永不止步，繼續旅程

完成本課後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 技能！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。