<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "11f03c81f190d9cbafd0f977dcbede6c",
  "translation_date": "2025-07-09T17:17:13+00:00",
  "source_file": "17-ai-agents/README.md",
  "language_code": "zh-tw"
}
-->
[![開源模型](../../../translated_images/17-lesson-banner.a5b918fb0920e4e6d8d391a100f5cb1d5929f4c2752c937d40392905dec82592.en.png)](https://aka.ms/gen-ai-lesson17-gh?WT.mc_id=academic-105485-koreyst)

## 簡介

AI 代理代表了生成式 AI 的一個令人興奮的進步，它允許大型語言模型 (LLM) 從助理演變為可以採取行動的代理。AI 代理框架使開發人員能夠建置應用程式，為 LLM 提供工具和狀態管理。這些框架還提高了透明度，讓使用者和開發人員能夠追蹤 LLM 規劃的行動，從而增強體驗管理。

本課將涵蓋以下主題：

- 了解什麼是 AI 代理 – AI 代理到底是什麼？
- 探索四種不同的 AI 代理框架 – 每種框架的獨特之處是什麼？
- 將這些 AI 代理應用於各種使用案例 – 我們應該何時使用 AI 代理？

## 學習目標

在本課結束時，您將能夠：

- 解釋什麼是 AI 代理以及如何使用它們。
- 了解一些流行的 AI 代理框架之間的差異以及它們的不同之處。
- 了解 AI 代理如何運作以建置使用它們的應用程式。

## 什麼是 AI 代理？

AI 代理是生成式 AI 中一個非常令人興奮的領域。伴隨著這種興奮，有時會對術語及其應用產生混淆。為了保持簡單並涵蓋大多數指稱 AI 代理的工具，我們將使用以下定義：

AI 代理允許大型語言模型 (LLM) 透過讓它們存取**狀態**和**工具**來執行任務。

![代理模型](../../../translated_images/what-agent.21f2893bdf01e6a7fd09b0416c2b15594d97f44bbb2ab5a1ff8bf643d2fcb3d.en.png)

讓我們定義這些術語：

**大型語言模型** – 這些是本課程中引用的模型，例如 GPT-3.5、GPT-4、Llama-2 等。

**狀態** – 這指的是 LLM 運作的上下文。LLM 使用其過去行動的上下文和當前情況來指導其未來行動的決策。AI 代理框架幫助開發人員更輕鬆地管理此上下文。

**工具** – 為了完成使用者請求並由 LLM 規劃的任務，LLM 需要存取工具。工具的範例包括資料庫、API、外部應用程式，甚至其他 LLM！

這些定義應該為我們探索這些概念如何實作奠定堅實的基礎。讓我們看看幾個不同的 AI 代理框架：

## LangChain 代理

[LangChain 代理](https://python.langchain.com/docs/how_to/#agents?WT.mc_id=academic-105485-koreyst) 實作了我們剛剛涵蓋的定義。

為了管理**狀態**，它使用一個名為 `AgentExecutor` 的內建函式。這接受已定義的 `agent` 和可用的 `tools`。

`AgentExecutor` 還會儲存聊天歷史記錄，以提供對話的上下文。

![Langchain 代理](../../../translated_images/langchain-agents.edcc55b5d5c437169a2037211284154561183c58bcec6d4ac2f8a79046fac9af.en.png)

LangChain 提供了一個[工具目錄](https://integrations.langchain.com/tools?WT.mc_id=academic-105485-koreyst)，可以匯入到您的應用程式中供 LLM 存取。這些工具由社群和 LangChain 團隊建立。

您可以定義這些工具並將它們傳遞給 `AgentExecutor`。

可見性是使用 AI 代理時的另一個關鍵方面。開發人員了解 LLM 正在使用哪個工具以及原因很重要。為了支援這一點，LangChain 團隊開發了 LangSmith。

## AutoGen

我們將討論的下一個 AI 代理框架是 [AutoGen](https://microsoft.github.io/autogen/?WT.mc_id=academic-105485-koreyst)。AutoGen 主要關注對話。代理既**可對話**又**可自訂**。

**可對話** – LLM 可以開始並繼續與其他 LLM 對話以完成任務。這是透過建立 `AssistantAgents` 並為其指派特定的系統訊息來完成的。

```python

autogen.AssistantAgent( name="Coder", llm_config=llm_config, ) pm = autogen.AssistantAgent( name="Product_manager", system_message="軟體產品創意富有創意。", llm_config=llm_config, )

```

**可自訂** – 代理不僅可以定義為 LLM，還可以定義為使用者或工具。作為開發人員，您可以定義一個 `UserProxyAgent`，負責與使用者互動以在任務完成期間收集回饋。此回饋可以繼續或停止任務執行。

```python
user_proxy = UserProxyAgent(name="user_proxy")
```

### 狀態和工具

為了管理和更新狀態，助理代理會產生 Python 程式碼來完成任務。

以下是該過程的範例：

![AutoGen](../../../translated_images/autogen.dee9a25a45fde584fedd84b812a6e31de5a6464687cdb66bb4f2cb7521391856.en.png)

#### 使用系統訊息定義的 LLM

```python
system_message="對於與天氣相關的任務，僅使用您已提供的函式。任務完成時回覆 TERMINATE。"
```

此系統訊息指示特定的 LLM 哪些函式與其任務相關。請記住，使用 AutoGen，您可以定義多個 AssistantAgents，每個都有不同的系統訊息。

#### 由使用者啟動聊天

```python
user_proxy.initiate_chat( chatbot, message="我下週要去紐約市旅行，你能幫我挑選穿什麼嗎？", )

```

來自 user_proxy (人類) 的此訊息啟動了代理的過程，以探索它應該執行哪些函式。

#### 函式已執行

```bash
聊天機器人 (對 user_proxy)：

***** 建議的工具呼叫：get_weather ***** 引數：{"location":"紐約市，紐約","time_periond:"7","temperature_unit":"攝氏"} ******************************************************** --------------------------------------------------------------------------------

>>>>>>>> 正在執行函式 get_weather... user_proxy (對聊天機器人)：***** 呼叫函式 "get_weather" 的回應 ***** 112.22727272727272 歐元 ****************************************************************

```

處理完初始聊天後，代理會建議呼叫一個工具。在這種情況下，它是一個名為 `get_weather` 的函式。根據您的設定，此函式可以自動執行並由代理讀取，或根據使用者輸入執行。

您可以找到 [AutoGen 程式碼範例](https://microsoft.github.io/autogen/docs/Examples/?WT.mc_id=academic-105485-koreyst) 清單，以探索如何開始建置。

## Taskweaver

我們將探索的下一個代理框架是 [Taskweaver](https://microsoft.github.io/TaskWeaver/?WT.mc_id=academic-105485-koreyst)。它被稱為「程式碼優先」代理，因為它不嚴格使用 `strings`，而是可以使用 Python 中的 DataFrames。這對於資料分析和生成任務特別有用，例如建立圖表或生成隨機數。

### 狀態和工具

為了管理對話狀態，TaskWeaver 使用了「規劃器」的概念。「規劃器」是一個 LLM，它接收使用者請求並規劃完成這些請求所需的任務。

為了完成這些任務，「規劃器」可以存取一個名為「外掛程式」的工具集合。這些可以是 Python 類別或通用程式碼解釋器。這些外掛程式以嵌入的形式儲存，因此 LLM 可以更好地搜尋正確的外掛程式。

![Taskweaver](../../../translated_images/taskweaver.da8559999267715a95b7677cf9b7d7dd8420aee6f3c484ced1833f081988dcd5.en.png)

以下是異常偵測外掛程式的範例：

```python
class AnomalyDetectionPlugin(Plugin): def __call__(self, df: pd.DataFrame, time_col_name: str, value_col_name: str):
```

程式碼在執行前會進行驗證。Taskweaver 中管理上下文的另一個功能是「經驗」。經驗允許對話上下文長期儲存在 YAML 檔案中。這可以進行設定，以便 LLM 透過從先前的對話中學習，隨著時間的推移在某些任務上有所改進。

## JARVIS

我們將探索的最後一個代理框架是 [JARVIS](https://github.com/microsoft/JARVIS?tab=readme-ov-file?WT.mc_id=academic-105485-koreyst)。JARVIS 的獨特之處在於它使用 LLM 來管理對話的「狀態」，而「工具」則是其他 AI 模型。每個 AI 模型都專門用於特定任務，例如物件偵測、轉錄或影像標註。

![JARVIS](../../../translated_images/jarvis.762ddbadbd1a3a3364d4ca3db1a7a9c0d2180060c0f8da6f7bd5b5ea2a115aa7.en.png)

LLM 作為通用模型，接收使用者的請求並識別特定任務以及完成任務所需的任何引數或資料。

```python
[{"task": "物件偵測", "id": 0, "dep": [-1], "args": {"image": "e1.jpg" }}]
```

LLM 然後以專業 AI 模型可以理解的方式格式化請求，例如 JSON。一旦 AI 模型傳回其預測，LLM 就會收到回應。

如果需要多個模型才能完成任務，LLM 會在組合它們以產生對使用者的最終回應之前，解釋每個模型的回應。

下面的範例顯示了當使用者請求影像中物件的描述和計數時，這是如何運作的：

## 作業

若要繼續學習 AI 代理，您可以使用 AutoGen 建置：

- 一個模擬與教育新創公司不同部門進行商務會議的應用程式。
- 建立系統訊息，引導 LLM 了解不同的角色和優先順序，讓使用者能夠提出新的產品構想。
- LLM 應隨後產生來自每個部門的後續問題，以完善和改進提案和產品構想。

## 學習永不止步，繼續旅程

完成本課後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 技能！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。