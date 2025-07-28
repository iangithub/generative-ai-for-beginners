<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d46aad0917a1a342d613e2c13d457da5",
  "translation_date": "2025-07-09T12:45:17+00:00",
  "source_file": "08-building-search-applications/README.md",
  "language_code": "zh-tw"
}
-->
# 建置搜尋應用程式

[![生成式 AI 與大型語言模型簡介](../../../translated_images/08-lesson-banner.8fff48c566dad08a1cbb9f4b4a2c16adfdd288a7bbfffdd30770b466fe08c25c.en.png)](https://aka.ms/gen-ai-lesson8-gh?WT.mc_id=academic-105485-koreyst)

> > _點擊上方圖片觀看本課影片_

LLM 不僅僅是聊天機器人和文字產生器。您還可以使用嵌入來建立搜尋應用程式。嵌入是資料的數值表示，也稱為向量，可用於語意搜尋。

在本課中，您將為我們的教育新創公司建置一個搜尋應用程式。我們的新創公司是一個非營利組織，為發展中國家的學生提供免費教育。我們有大量的 YouTube 影片，學生可以用來學習 AI。目標是建置一個搜尋應用程式，讓學生可以透過輸入問題來尋找 YouTube 影片。

例如，學生可能會輸入「什麼是 Jupyter Notebooks？」或「什麼是 Azure ML？」，搜尋應用程式將傳回相關的 YouTube 影片清單。更棒的是，該應用程式將提供一個連結，直接連到影片中可以找到答案的確切時間點。

## 簡介

在本課中，我們將涵蓋：

- 語意搜尋與關鍵字搜尋。
- 什麼是文字嵌入。
- 如何建立文字嵌入索引。
- 如何搜尋文字嵌入索引。

## 學習目標

在本課結束時，您將能夠：

- 區分語意搜尋和關鍵字搜尋。
- 解釋什麼是文字嵌入。
- 建置一個使用嵌入來搜尋資料的應用程式。

## 為何要建置搜尋應用程式？

建置搜尋應用程式將幫助您了解如何使用嵌入進行資料搜尋。您還將學習如何建立一個工具，讓學生可以快速找到資訊。

本課程包含來自微軟 [AI Show](https://www.youtube.com/playlist?list=PLlrxD0HtieHi0mwteKBOfEeOYf0LJU4O1) YouTube 頻道的 YouTube 逐字稿嵌入索引。AI Show 教授 AI 和機器學習概念。嵌入索引包含截至 2023 年 10 月所有逐字稿的嵌入。您將使用此索引為我們的新創公司建置一個搜尋應用程式。該應用程式將傳回一個連結，直接連到影片中答案所在的位置，讓學生可以輕鬆快速地找到他們需要的內容。

這裡有一個針對問題「我可以在 azure ml 中使用 rstudio 嗎？」的語意查詢範例。請注意，YouTube URL 包含一個時間戳記，可將您直接帶到影片中包含答案的部分。

![針對問題「我可以在 Azure ML 中使用 rstudio 嗎？」的語意查詢](../../../translated_images/query-results.bb0480ebf025fac69c5179ad4d53b6627d643046838c857dc9e2b1281f1cdeb7.en.png)

## 什麼是語意搜尋？

您可能想知道，語意搜尋到底是什麼？語意搜尋是一種使用查詢中單字意義來傳回相關結果的技術。

例如，如果您想買車並搜尋「我的夢想車」，語意搜尋會理解您並非字面上在夢見一輛車，而是在尋找您理想的車。它會解讀您的意圖並傳回相關結果。相較之下，關鍵字搜尋會尋找確切的單字「夢想」和「車」，通常會傳回不相關的結果。

## 什麼是文字嵌入？

[文字嵌入](https://en.wikipedia.org/wiki/Word_embedding?WT.mc_id=academic-105485-koreyst) 是在[自然語言處理](https://en.wikipedia.org/wiki/Natural_language_processing?WT.mc_id=academic-105485-koreyst)中表示文字的一種方式。它們是文字的語意數值表示，讓機器更容易理解。有許多模型可用於建立文字嵌入；在本課中，我們專注於使用 OpenAI 嵌入模型產生嵌入。

例如，想像以下文字來自 AI Show 某一集的逐字稿：

```text
今天我們要來學習 Azure Machine Learning。
```

我們將此文字傳送至 OpenAI 嵌入 API，它會傳回一個包含 1536 個數字的嵌入向量。每個數字都捕捉了文字的不同面向。為求簡潔，以下是向量中的前 10 個數字：

```python
[-0.006655829958617687, 0.0026128944009542465, 0.008792596869170666, -0.02446001023054123, -0.008540431968867779, 0.022071078419685364, -0.010703742504119873, 0.003311325330287218, -0.011632772162556648, -0.02187200076878071, ...]
```

## 嵌入索引是如何建立的？

本課程的嵌入索引是使用一系列 Python 指令碼建立的。您可以在本課程的「scripts」資料夾中的 [README](./scripts/README.md?WT.mc_id=academic-105485-koreyst) 中找到這些指令碼和說明。您不需要自己執行這些指令碼，因為嵌入索引已經提供。

這些指令碼會執行以下步驟：

1. 下載 [AI Show](https://www.youtube.com/playlist?list=PLlrxD0HtieHi0mwteKBOfEeOYf0LJU4O1) 播放清單中每個 YouTube 影片的逐字稿。
2. 使用 [OpenAI Functions](https://learn.microsoft.com/azure/ai-services/openai/how-to/function-calling?WT.mc_id=academic-105485-koreyst)，嘗試從每個逐字稿的前 3 分鐘擷取演講者的姓名。每個影片的演講者姓名都儲存在嵌入索引檔案 `embedding_index_3m.json` 中。
3. 將逐字稿分割成 **3 分鐘的文字片段**。每個片段與下一個片段重疊約 20 個字，以避免切斷嵌入並提供更好的搜尋上下文。
4. 將每個文字片段傳遞給 OpenAI 聊天 API 以產生 60 字的摘要。此摘要也儲存在 `embedding_index_3m.json` 中。
5. 將每個片段傳送至 OpenAI 嵌入 API，它會傳回一個代表該片段語意意義的 1536 個數字的向量。該片段及其嵌入向量儲存在 `embedding_index_3m.json` 中。

### 向量資料庫

為求簡單，嵌入索引儲存為名為 `embedding_index_3m.json` 的 JSON 檔案，並載入到 Pandas DataFrame 中。然而，在生產環境中，嵌入索引會儲存在向量資料庫中，例如 [Azure Cognitive Search](https://learn.microsoft.com/training/modules/improve-search-results-vector-search?WT.mc_id=academic-105485-koreyst)、[Redis](https://cookbook.openai.com/examples/vector_databases/redis/readme?WT.mc_id=academic-105485-koreyst)、[Pinecone](https://cookbook.openai.com/examples/vector_databases/pinecone/readme?WT.mc_id=academic-105485-koreyst) 或 [Weaviate](https://cookbook.openai.com/examples/vector_databases/weaviate/readme?WT.mc_id=academic-105485-koreyst) 等。

## 了解餘弦相似度

現在我們已經介紹了文字嵌入，下一步是學習如何使用它們來搜尋資料，特別是透過使用餘弦相似度來尋找與查詢最相似的嵌入。

### 什麼是餘弦相似度？

餘弦相似度測量兩個向量的相似程度。這也稱為「最近鄰搜尋」。若要執行餘弦相似度搜尋，您首先需要使用 OpenAI 嵌入 API 將「查詢」文字「向量化」。然後，計算查詢向量與嵌入索引中每個向量之間的「餘弦相似度」。請記住，嵌入索引包含每個 YouTube 逐字稿片段的向量。最後，按餘弦相似度對結果進行排序——分數最高的片段與查詢最相似。

在數學上，餘弦相似度測量多維空間中兩個向量之間夾角的餘弦值。這很有用，因為即使兩個文件由於大小差異而在歐幾里得距離上相距甚遠，它們之間的夾角仍然可以很小，從而導致較高的餘弦相似度。有關數學的更多詳細資訊，請參閱[餘弦相似度](https://en.wikipedia.org/wiki/Cosine_similarity?WT.mc_id=academic-105485-koreyst)。

## 建置您的第一個搜尋應用程式

接下來，我們將使用嵌入來建置一個搜尋應用程式。這個應用程式將讓學生可以透過輸入問題來搜尋影片。它會傳回相關影片的清單，並提供一個連結，直接連到影片中可以找到答案的位置。

此解決方案已在 Windows 11、macOS 和 Ubuntu 22.04 上使用 Python 3.10 或更高版本進行建置和測試。您可以從 [python.org](https://www.python.org/downloads/?WT.mc_id=academic-105485-koreyst) 下載 Python。

## 作業 - 建置一個搜尋應用程式來幫助學生

我們在本課開始時介紹了我們的新創公司。現在是時候讓學生建置一個搜尋應用程式作為他們評量的一部分了。

在此作業中，您將建立建置搜尋應用程式所需的 Azure OpenAI 服務。您將設定以下 Azure OpenAI 服務。完成此作業需要 Azure 訂閱。

### 啟動 Azure Cloud Shell

1. 登入 [Azure 入口網站](https://portal.azure.com/?WT.mc_id=academic-105485-koreyst)。
2. 按一下右上角的 Cloud Shell 圖示。
3. 選擇 **Bash** 作為環境。

#### 建立資源群組

> 在這些說明中，我們在美國東部使用名為「semantic-video-search」的資源群組。
> 您可以變更資源群組名稱，但如果您變更資源位置，
> 請查看[模型可用性表](https://aka.ms/oai/models?WT.mc_id=academic-105485-koreyst)。

```shell
az group create --name semantic-video-search --location eastus
```

#### 建立 Azure OpenAI 服務資源

在 Azure Cloud Shell 中，執行下列指令以建立 Azure OpenAI 服務資源。

```shell
az cognitiveservices account create --name semantic-video-openai --resource-group semantic-video-search \
    --location eastus --kind OpenAI --sku s0
```

#### 取得在此應用程式中使用的端點和金鑰

在 Azure Cloud Shell 中，執行這些指令以擷取您的 Azure OpenAI 服務資源的端點和金鑰。

```shell
az cognitiveservices account show --name semantic-video-openai \
   --resource-group  semantic-video-search | jq -r .properties.endpoint
az cognitiveservices account keys list --name semantic-video-openai \
   --resource-group semantic-video-search | jq -r .key1
```

#### 部署 OpenAI 嵌入模型

在 Azure Cloud Shell 中，執行下列指令以部署 OpenAI 嵌入模型。

```shell
az cognitiveservices account deployment create \
    --name semantic-video-openai \
    --resource-group  semantic-video-search \
    --deployment-name text-embedding-ada-002 \
    --model-name text-embedding-ada-002 \
    --model-version "2"  \
    --model-format OpenAI \
    --sku-capacity 100 --sku-name "Standard"
```

## 解決方案

在 GitHub Codespaces 中開啟[解決方案筆記本](../../../08-building-search-applications/python/aoai-solution.ipynb)並遵循 Jupyter Notebook 中的說明。

當您執行筆記本時，系統會提示您輸入查詢。輸入框會像這樣：

![使用者輸入查詢的輸入框](../../../translated_images/notebook-search.1e320b9c7fcbb0bc1436d98ea6ee73b4b54ca47990a1c952b340a2cadf8ac1ca.en.png)

## 做得好！繼續學習

完成本課後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您對生成式 AI 的了解！

接下來，前往第 9 課，我們將探討如何[建置影像生成應用程式](../09-building-image-applications/README.md?WT.mc_id=academic-105485-koreyst)！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。
