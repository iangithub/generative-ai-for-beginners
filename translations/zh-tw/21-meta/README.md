<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4c2a0b0c738b649ef049fb99a23be661",
  "translation_date": "2025-07-09T19:05:23+00:00",
  "source_file": "21-meta/README.md",
  "language_code": "zh-tw"
}
-->
# 使用 Meta 系列模型建置

## 簡介

本課程將涵蓋：

- 探索兩個主要的 Meta 系列模型 - Llama 3.1 和 Llama 3.2
- 了解每個模型的使用案例和情境
- 示範每個模型獨特功能的程式碼範例


## Meta 系列模型

在本課程中，我們將探索 Meta 系列或「Llama 群」中的 2 個模型 - Llama 3.1 和 Llama 3.2

這些模型有不同的變體，並可在 GitHub 模型市集上取得。以下是關於使用 GitHub 模型來[使用 AI 模型進行原型設計](https://docs.github.com/en/github-models/prototyping-with-ai-models?WT.mc_id=academic-105485-koreyst)的更多詳細資訊。

模型變體：
- Llama 3.1 - 70B Instruct
- Llama 3.1 - 405B Instruct
- Llama 3.2 - 11B Vision Instruct
- Llama 3.2 - 90B Vision Instruct

*注意：Llama 3 也可在 GitHub 模型上取得，但不會在本課程中涵蓋*

## Llama 3.1

Llama 3.1 擁有 4050 億個參數，屬於開源 LLM 類別。

此模型是早期發布的 Llama 3 的升級版，提供：

- 更大的上下文視窗 - 128k 權杖 vs 8k 權杖
- 更大的最大輸出權杖 - 4096 vs 2048
- 更好的多語言支援 - 歸功於訓練權杖的增加

這些改進使 Llama 3.1 能夠在建置生成式 AI 應用程式時處理更複雜的使用案例，包括：
- 原生函式呼叫 - 能夠呼叫 LLM 工作流程之外的外部工具和函式
- 更好的 RAG 效能 - 由於更大的上下文視窗
- 合成資料生成 - 能夠為微調等任務建立有效資料

### 原生函式呼叫

Llama 3.1 已經過微調，在函式或工具呼叫方面更有效。它還包含兩個內建工具，模型可以根據使用者的提示在需要時識別。這些工具是：

- **Brave Search** - 可用於透過執行網路搜尋來獲取最新資訊，例如天氣
- **Wolfram Alpha** - 可用於更複雜的數學計算，因此您無需編寫自己的函式。

您還可以建立自己的自訂工具，供 LLM 呼叫。

在下面的程式碼範例中：

- 我們在系統提示中定義了可用的工具 (brave_search, wolfram_alpha)。
- 傳送一個使用者提示，詢問特定城市的天氣。
- LLM 將回應一個對 Brave Search 工具的工具呼叫，它看起來會像這樣 `<|python_tag|>brave_search.call(query="Stockholm weather")`

*注意：此範例僅進行工具呼叫；如果您想獲取結果，您需要 Brave API 頁面上建立一個免費帳戶並定義函式本身*

```python
import os
from azure.ai.inference import ChatCompletionsClient
from azure.ai.inference.models import AssistantMessage, SystemMessage, UserMessage
from azure.core.credentials import AzureKeyCredential

token = os.environ["GITHUB_TOKEN"]
endpoint = "https://models.inference.ai.azure.com"
model_name = "meta-llama-3.1-405b-instruct"

client = ChatCompletionsClient(
    endpoint=endpoint,
    credential=AzureKeyCredential(token),
)


tool_prompt=f"""
<|begin_of_text|><|start_header_id|>system<|end_header_id|>

環境：ipython
工具：brave_search, wolfram_alpha
知識截止日期：2023 年 12 月
今天日期：2024 年 7 月 23 日

您是一位樂於助人的助理<|eot_id|>
"""

messages = [
    SystemMessage(content=tool_prompt),
    UserMessage(content="斯德哥爾摩天氣如何？"),

]

response = client.complete(messages=messages, model=model_name)

print(response.choices[0].message.content)
```

## Llama 3.2

儘管 Llama 3.1 是一個功能強大的 LLM，但其限制之一是多模態——即能夠使用不同類型的輸入（例如影像）作為提示並提供回應。此功能是 Llama 3.2 的主要功能之一。其他功能包括：

- 多模態 - 可以處理文字和影像提示
- 小型到中型變體 (11B 和 90B) - 提供靈活的部署選項
- 純文字變體 (1B 和 3B) - 允許在邊緣/行動裝置上以低延遲部署

多模態支援標誌著開源模型的一個重大進步。下面的程式碼範例同時接受影像和文字提示，以從 Llama 3.2 90B 獲取影像分析。


### Llama 3.2 的多模態支援

```python
import os
from azure.ai.inference import ChatCompletionsClient
from azure.ai.inference.models import (
    SystemMessage,
    UserMessage,
    TextContentItem,
    ImageContentItem,
    ImageUrl,
    ImageDetailLevel,
)
from azure.core.credentials import AzureKeyCredential

token = os.environ["GITHUB_TOKEN"]
endpoint = "https://models.inference.ai.azure.com"
model_name = "Llama-3.2-90B-Vision-Instruct"

client = ChatCompletionsClient(
    endpoint=endpoint,
    credential=AzureKeyCredential(token),
)

response = client.complete(
    messages=[
        SystemMessage(
            content="您是一個樂於助人的助理，詳細描述影像。"
        ),
        UserMessage(
            content=[
                TextContentItem(text="這張圖片裡有什麼？"),
                ImageContentItem(
                    image_url=ImageUrl.load(
                        image_file="sample.jpg",
                        image_format="jpg",
                        detail=ImageDetailLevel.LOW)
                ),
            ],
        ),
    ],
    model=model_name,
)

print(response.choices[0].message.content)
```

## 學習永不止步，繼續旅程

完成本課後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 技能！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。