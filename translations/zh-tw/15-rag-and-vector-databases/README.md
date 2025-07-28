<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e2861bbca91c0567ef32bc77fe054f9e",
  "translation_date": "2025-07-09T16:00:58+00:00",
  "source_file": "15-rag-and-vector-databases/README.md",
  "language_code": "zh-tw"
}
-->
# 檢索增強生成 (RAG) 和向量資料庫

[![檢索增強生成 (RAG) 和向量資料庫](../../../translated_images/15-lesson-banner.ac49e59506175d4fc6ce521561dab2f9ccc6187410236376cfaed13cde371b90.en.png)](https://aka.ms/gen-ai-lesson15-gh?WT.mc_id=academic-105485-koreyst)

在搜尋應用程式課程中，我們簡要探討了如何將您自己的資料整合到大型語言模型 (LLM) 中。在本課中，我們將深入探討如何在您的 LLM 應用程式中建立資料基礎、處理機制以及儲存資料的方法，包括嵌入和文字。

> **影片即將推出**

## 簡介

在本課中，我們將涵蓋：

- RAG 簡介，它是什麼，以及為何在 AI (人工智慧) 中使用它。

- 了解向量資料庫以及如何為我們的應用程式建立一個。

- 將 RAG 整合到應用程式中的實際範例。

## 學習目標

在本課結束時，您將能夠：

- 解釋 RAG 在資料檢索和處理中的重要性。

- 設定 RAG 應用程式並將您的資料建立到 LLM 中。

- 有效地將 RAG 和向量資料庫整合到 LLM 應用程式中。

## 我們的情境：用我們自己的資料增強我們的 LLM

在本課中，我們希望將我們自己的筆記新增到教育新創公司中，讓聊天機器人能夠存取更多關於各種主題的資訊。透過這些筆記，學習者將能夠更有效地學習並更好地理解不同的主題，使考試複習更容易。為了建置我們的情境，我們將使用：

- `Azure OpenAI:` 為我們的聊天機器人提供動力的 LLM

- `AI for beginners' lesson on Neural Networks:` 我們將 LLM 建立基礎的資料

- `Azure AI Search` 和 `Azure Cosmos DB:` 向量資料庫，用於儲存我們的資料並建立搜尋索引

使用者將能夠從他們的筆記中建立練習測驗、複習抽認卡和摘要以獲得簡潔的概述。首先，讓我們探討 RAG 是什麼以及它是如何運作的：

## 檢索增強生成 (RAG)

由 LLM 驅動的聊天機器人處理使用者提示以產生回應。它旨在互動並讓使用者參與廣泛的主題。然而，它的回應僅限於所提供的上下文及其基礎訓練資料。例如，GPT-4 的知識截止日期是 2021 年 9 月，因此它缺乏該日期之後的事件資訊。此外，用於訓練 LLM 的資料不包括機密資訊，例如個人筆記或公司產品手冊。

### RAG (檢索增強生成) 的運作方式

![顯示 RAG 如何運作的圖示](../../../translated_images/how-rag-works.f5d0ff63942bd3a638e7efee7a6fce7f0787f6d7a1fca4e43f2a7a4d03cde3e0.en.png)

假設您想部署一個聊天機器人，可以從您的筆記中建立測驗——您將需要連接到知識庫。這就是 RAG 發揮作用的地方。RAG 的運作方式如下：

- **知識庫：** 在檢索之前，文件必須經過攝取和預處理，通常是將大型文件分解成較小的區塊，將它們轉換為文字嵌入，並將它們儲存在資料庫中。

- **使用者查詢：** 使用者提出問題。

- **檢索：** 當使用者提出問題時，嵌入模型會從知識庫中檢索相關資訊，以提供將包含在提示中的額外上下文。

- **增強生成：** LLM 根據檢索到的資料增強其回應。這使得回應不僅基於預訓練資料，還基於來自新增上下文的相關資訊。檢索到的資料用於增強 LLM 的回應，然後 LLM 會向使用者問題傳回答案。

![顯示 RAG 架構的圖示](../../../translated_images/encoder-decode.f2658c25d0eadee2377bb28cf3aee8b67aa9249bf64d3d57bb9be077c4bc4e1a.en.png)

RAG 的架構是使用由兩部分組成的轉換器實現的：編碼器和解碼器。例如，當使用者提出問題時，輸入文字會被「編碼」成捕捉單字意義的向量，然後這些向量會被「解碼」到我們的文件索引中，以根據使用者查詢產生新文字。LLM 使用編碼器-解碼器模型來產生輸出。

根據論文 [Retrieval-Augmented Generation for Knowledge Intensive NLP Tasks](https://arxiv.org/pdf/2005.11401.pdf?WT.mc_id=academic-105485-koreyst)，實現 RAG 的兩種方法是：

- **_RAG-Sequence_**：使用檢索到的文件來預測使用者查詢的最佳可能答案。

- **RAG-Token**：使用文件來產生下一個權杖，然後檢索它們以回答使用者的查詢。

### 為何使用 RAG？

- **資訊豐富性：** 確保文字回應是最新的，並透過存取內部知識庫來提高特定領域任務的效能。

- 透過使用知識庫中**可驗證的資料**為使用者查詢提供上下文，從而減少捏造。

- 它**具有成本效益**，因為它比微調 LLM 更經濟。

## 建立知識庫

我們的應用程式基於我們的個人資料，特別是來自「AI for Beginners」課程的「神經網路」課程。

### 向量資料庫

向量資料庫與傳統資料庫不同，它專門用於儲存、管理和搜尋嵌入向量。它儲存文件的數值表示。將資料分解為數值嵌入，使我們的 AI 系統更容易理解和處理。

我們將嵌入儲存在向量資料庫中，因為 LLM 對其接受的權杖數量有限制。由於您無法將整個嵌入傳遞給 LLM，因此我們將它們分解成區塊。當使用者提出問題時，與問題最相關的嵌入會與提示一起傳回。分塊還可以透過限制傳遞給 LLM 的權杖數量來降低成本。

流行的向量資料庫包括 Azure Cosmos DB、Clarifyai、Pinecone、Chromadb、ScaNN、Qdrant 和 DeepLake。您可以使用 Azure CLI 透過以下命令建立 Azure Cosmos DB 模型：

```bash
az loginaz group create -n <resource-group-name> -l <location>az cosmosdb create -n <cosmos-db-name> -r <resource-group-name>az cosmosdb list-keys -n <cosmos-db-name> -g <resource-group-name>
```

### 從文字到嵌入

在儲存資料之前，我們需要將其轉換為向量嵌入。如果您正在處理大型文件或長文本，您可以根據預期的查詢將它們分塊。分塊可以在句子或段落層級進行。由於分塊是從周圍的單字中獲取意義，因此您可以向區塊添加額外的上下文，例如文件標題或區塊之前或之後的一些文本。您可以按如下方式分塊資料：

```python
def split_text(text, max_length, min_length):
    words = text.split()
    chunks = []
    current_chunk = []

    for word in words:
        current_chunk.append(word)
        if len(' '.join(current_chunk)) < max_length and len(' '.join(current_chunk)) > min_length:
            chunks.append(' '.join(current_chunk))
            current_chunk = []

    # 如果最後一個區塊未達到最小長度，則無論如何都將其新增
    if current_chunk:
        chunks.append(' '.join(current_chunk))

    return chunks
```

分塊後，我們使用不同的嵌入模型嵌入文字。一些選項包括 word2vec、OpenAI 的 ada-002、Azure Computer Vision 等。模型的選擇取決於您使用的語言、內容類型（文字/影像/音訊）、它可以編碼的輸入大小以及嵌入輸出的長度。

使用 OpenAI 的 `text-embedding-ada-002` 模型嵌入文字的範例是：
![單字 cat 的嵌入](../../../translated_images/cat.74cbd7946bc9ca380a8894c4de0c706a4f85b16296ffabbf52d6175df6bf841e.en.png)

## 檢索和向量搜尋

當使用者提出問題時，檢索器會使用查詢編碼器將其轉換為向量，然後在我們的文件搜尋索引中搜尋與輸入相關的向量。之後，它會將輸入向量和文件向量都轉換回文字，並將它們傳遞給 LLM。

### 檢索

檢索發生在系統快速從索引中找到符合搜尋條件的文件時。檢索器的目標是擷取提供上下文並將 LLM 建立在您的資料中的文件。

在我們的資料庫中有幾種搜尋方式：

- **關鍵字搜尋：** 用於文字搜尋。

- **語意搜尋：** 使用單字的語意意義。

- **向量搜尋：** 使用嵌入模型將文件從文字轉換為向量表示。檢索是透過查詢向量表示最接近使用者問題的文件來完成的。

- **混合：** 關鍵字搜尋和向量搜尋的組合。

當資料庫中沒有與查詢相似的回應時，就會出現挑戰。系統將傳回最佳可用資訊，但您可以使用諸如設定相關性最大距離或使用結合關鍵字和向量搜尋的混合搜尋等策略。在本課中，我們將使用混合搜尋，結合向量和關鍵字搜尋。我們將資料儲存在一個資料框中，其中包含區塊和嵌入的欄位。

### 向量相似度

檢索器在知識庫中搜尋彼此接近的嵌入——最近的鄰居——因為它們代表相似的文本。當使用者提出查詢時，它會首先被嵌入，然後與相似的嵌入進行匹配。向量之間最常見的相似度測量是餘弦相似度，它基於兩個向量之間的角度。

其他相似度測量包括歐幾里得距離（即向量端點之間的直線距離）和點積（即測量兩個向量對應元素乘積的總和）。

### 搜尋索引

在執行檢索之前，我們需要為我們的知識庫建置一個搜尋索引。索引儲存嵌入，即使在大型資料庫中，也可以快速檢索最相似的區塊。我們可以使用以下方式在本機建立索引：

```python
from sklearn.neighbors import NearestNeighbors

embeddings = flattened_df['embeddings'].to_list()

# 建立搜尋索引
nbrs = NearestNeighbors(n_neighbors=5, algorithm='ball_tree').fit(embeddings)

# 若要查詢索引，您可以使用 kneighbors 方法
distances, indices = nbrs.kneighbors(embeddings)
```

### 重新排名

查詢資料庫後，您可能需要根據相關性對結果進行排序。重新排名 LLM 使用機器學習來提高搜尋結果的相關性，方法是將它們從最相關到最不相關進行排序。使用 Azure AI Search，重新排名會自動透過語意重新排名器完成。以下是使用最近鄰居的重新排名運作方式的範例：

```python
# 尋找最相似的文件
distances, indices = nbrs.kneighbors([query_vector])

index = []
# 列印最相似的文件
for i in range(3):
    index = indices[0][i]
    for index in indices[0]:
        print(flattened_df['chunks'].iloc[index])
        print(flattened_df['path'].iloc[index])
        print(flattened_df['distances'].iloc[index])
    else:
        print(f"索引 {index} 在 DataFrame 中找不到")
```

## 整合所有內容

最後一步是整合我們的 LLM，以產生基於我們資料的回應。我們可以按如下方式實作它：

```python
user_input = "什麼是感知器？"

def chatbot(user_input):
    # 將問題轉換為查詢向量
    query_vector = create_embeddings(user_input)

    # 尋找最相似的文件
    distances, indices = nbrs.kneighbors([query_vector])

    # 將文件新增到查詢中以提供上下文
    history = []
    for index in indices[0]:
        history.append(flattened_df['chunks'].iloc[index])

    # 結合歷史記錄和使用者輸入
    history.append(user_input)

    # 建立訊息物件
    messages=[
        {"role": "system", "content": "您是一個協助回答 AI 問題的 AI 助理。"},
        {"role": "user", "content": history[-1]}
    ]

    # 使用聊天完成來產生回應
    response = openai.chat.completions.create(
        model="gpt-4",
        temperature=0.7,
        max_tokens=800,
        messages=messages
    )

    return response.choices[0].message

chatbot(user_input)
```

## 評估我們的應用程式

### 評估指標

- 回應品質：確保它們聽起來自然、流暢且像人類。

- 資料的基礎性：評估回應是否基於所提供的文件。

- 相關性：評估回應是否與所提出的問題相符且相關。

- 流暢性：檢查回應是否語法連貫。

## RAG 和向量資料庫的使用案例

有許多使用案例可以透過函式呼叫來增強您的應用程式，例如：

- 問答：將您的公司資料建立在員工可以用來提問的聊天中。

- 推薦系統：建立匹配最相似項目的系統，例如電影、餐廳等等。

- 聊天機器人服務：儲存聊天歷史記錄並根據使用者資料個人化對話。

- 基於向量嵌入的影像搜尋，適用於影像辨識和異常偵測。

## 摘要

我們已經涵蓋了 RAG 的基礎知識，從將資料新增到應用程式，到使用者查詢和輸出。為了簡化 RAG 的建立，您可以使用 Semantic Kernel、LangChain 或 Autogen 等框架。

## 作業

若要繼續學習檢索增強生成 (RAG)，您可以：

- 使用您偏好的框架為應用程式建置前端。

- 使用 LangChain 或 Semantic Kernel 等框架重新建立您的應用程式。

恭喜您完成本課👏。

## 學習永不止步，繼續旅程

完成本課後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 技能！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。