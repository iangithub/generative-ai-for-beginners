<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a45c318dc6ebc2604f35b8b829f93af2",
  "translation_date": "2025-07-09T09:37:42+00:00",
  "source_file": "04-prompt-engineering-fundamentals/README.md",
  "language_code": "tw"
}
-->
# Prompt Engineering Fundamentals

[![Prompt Engineering Fundamentals](../../../translated_images/04-lesson-banner.a2c90deba7fedacda69f35b41636a8951ec91c2e33f5420b1254534ac85bc18e.tw.png)](https://aka.ms/gen-ai-lesson4-gh?WT.mc_id=academic-105485-koreyst)

## 介紹
本單元涵蓋在生成式 AI 模型中創建有效提示的基本概念與技巧。你如何撰寫給大型語言模型（LLM）的提示同樣重要。精心設計的提示能帶來更高品質的回應。但到底什麼是「提示」和「提示工程」？我該如何改進送給 LLM 的提示輸入？這些問題將在本章及下一章中嘗試解答。

生成式 AI 能根據使用者需求創造新內容（例如文字、圖片、音訊、程式碼等）。它透過像 OpenAI 的 GPT（「生成式預訓練轉換器」）系列這類大型語言模型來實現，這些模型經過自然語言與程式碼的訓練。

使用者現在可以用熟悉的對話方式與這些模型互動，無需任何技術背景或訓練。這些模型是基於「提示」的——使用者輸入文字（提示），模型回傳 AI 回應（完成）。使用者可以透過多輪對話不斷調整提示，直到回應符合預期。

「提示」成為生成式 AI 應用的主要程式介面，指示模型該做什麼，並影響回應品質。「提示工程」是一個快速成長的領域，專注於設計與優化提示，以大規模提供穩定且高品質的回應。

## 學習目標

本課程將介紹什麼是提示工程、為何重要，以及如何為特定模型和應用目標打造更有效的提示。我們將理解提示工程的核心概念與最佳實務，並學習如何在互動式 Jupyter 筆記本「沙盒」環境中，將這些概念應用於實例。

完成本課程後，你將能夠：

1. 解釋什麼是提示工程及其重要性。
2. 描述提示的組成部分及其用途。
3. 學習提示工程的最佳實務與技巧。
4. 使用 OpenAI 端點，將所學技巧應用於實例。

## 關鍵詞彙

提示工程：設計與優化輸入，以引導 AI 模型產生期望輸出的實務。
分詞（Tokenization）：將文字轉換成模型能理解與處理的較小單位（稱為「詞元」）的過程。
指令微調大型語言模型（Instruction-Tuned LLMs）：經過特定指令微調，以提升回應準確性與相關性的 LLM。

## 學習沙盒

提示工程目前更像是一門藝術而非科學。提升直覺的最佳方式是多加練習，採用結合應用領域專業知識、推薦技巧與模型特定優化的試錯方法。

本課程附帶的 Jupyter 筆記本提供一個沙盒環境，讓你能隨時嘗試所學內容，或作為課程結尾的程式挑戰。執行練習需要：

1. **Azure OpenAI API 金鑰**——已部署 LLM 的服務端點。
2. **Python 執行環境**——用於執行筆記本。
3. **本地環境變數**——請先完成[設定](./../00-course-setup/SETUP.md?WT.mc_id=academic-105485-koreyst)步驟。

筆記本內建入門練習，但鼓勵你自行新增 _Markdown_（說明）與 _Code_（提示請求）區塊，嘗試更多範例或想法，培養提示設計的直覺。

## 圖解指南

想先了解本課程涵蓋的整體架構嗎？請參考這份圖解指南，讓你掌握主要主題與每個主題的關鍵重點。課程路線圖將帶你從理解核心概念與挑戰，進而學習相關提示工程技巧與最佳實務。請注意，指南中的「進階技巧」部分是指本課程下一章的內容。

![Illustrated Guide to Prompt Engineering](../../../translated_images/04-prompt-engineering-sketchnote.d5f33336957a1e4f623b826195c2146ef4cc49974b72fa373de6929b474e8b70.tw.png)

## 我們的新創公司

現在，讓我們談談這個主題如何與我們的新創使命相關——[將 AI 創新帶入教育](https://educationblog.microsoft.com/2023/06/collaborating-to-bring-ai-innovation-to-education?WT.mc_id=academic-105485-koreyst)。我們希望打造 AI 驅動的個人化學習應用，思考不同使用者如何「設計」提示：

- **管理者**可能會請 AI _分析課程資料，找出內容缺口_。AI 可總結結果或用程式碼視覺化。
- **教育者**可能會請 AI _為特定對象與主題生成教案_。AI 可依指定格式建立個人化計畫。
- **學生**可能會請 AI _輔導他們學習困難科目_。AI 現在能依學生程度提供課程、提示與範例。

這只是冰山一角。請參考由教育專家策劃的開源提示庫 [Prompts For Education](https://github.com/microsoft/prompts-for-edu/tree/main?WT.mc_id=academic-105485-koreyst)，了解更多可能性！_試著在沙盒或 OpenAI Playground 執行這些提示，看看結果如何！_

<!--
LESSON TEMPLATE:
This unit should cover core concept #1.
Reinforce the concept with examples and references.

CONCEPT #1:
Prompt Engineering.
Define it and explain why it is needed.
-->

## 什麼是提示工程？

我們從定義 **提示工程** 開始，指的是為特定應用目標與模型，設計與優化文字輸入（提示），以提供穩定且高品質回應（完成）的過程。我們可以將其視為兩步驟：

- 為特定模型與目標 _設計_ 初始提示
- 反覆 _優化_ 提示以提升回應品質

這必然是一個試錯過程，需要使用者的直覺與努力才能達到最佳結果。那為什麼它重要？要回答這問題，我們先了解三個概念：

- _分詞_ = 模型如何「看見」提示
- _基礎 LLM_ = 基礎模型如何「處理」提示
- _指令微調 LLM_ = 模型如何「理解任務」

### 分詞（Tokenization）

LLM 將提示視為一連串的 _詞元_，不同模型（或同一模型的不同版本）可能會以不同方式分詞同一提示。由於 LLM 是以詞元（而非原始文字）訓練，提示的分詞方式直接影響生成回應的品質。

想了解分詞如何運作，可以試試像下方的 [OpenAI Tokenizer](https://platform.openai.com/tokenizer?WT.mc_id=academic-105485-koreyst) 工具。將你的提示貼上，觀察它如何被轉換成詞元，特別注意空白字元與標點符號的處理。此範例使用較舊的 LLM（GPT-3），用較新模型測試可能會有不同結果。

![Tokenization](../../../translated_images/04-tokenizer-example.e71f0a0f70356c5c7d80b21e8753a28c18a7f6d4aaa1c4b08e65d17625e85642.tw.png)

### 概念：基礎模型

提示分詞後，["基礎 LLM"](https://blog.gopenai.com/an-introduction-to-base-and-instruction-tuned-large-language-models-8de102c785a6?WT.mc_id=academic-105485-koreyst)（或稱基礎模型）的主要功能是預測詞元序列中的下一個詞元。由於 LLM 以龐大文字資料集訓練，能掌握詞元間的統計關係，並以一定信心做出預測。請注意，它們不理解提示或詞元的「意義」，只看到可「完成」的模式，並持續預測直到使用者中止或達成預設條件。

想看看基於提示的完成如何運作？將上述提示輸入 Azure OpenAI Studio 的 [_Chat Playground_](https://oai.azure.com/playground?WT.mc_id=academic-105485-koreyst)，使用預設設定。系統會將提示視為資訊請求，你應該會看到符合此情境的完成回應。

但如果使用者想要符合特定條件或任務目標的回應呢？這時就需要用到 _指令微調_ 的 LLM。

![Base LLM Chat Completion](../../../translated_images/04-playground-chat-base.65b76fcfde0caa6738e41d20f1a6123f9078219e6f91a88ee5ea8014f0469bdf.tw.png)

### 概念：指令微調 LLM

[指令微調 LLM](https://blog.gopenai.com/an-introduction-to-base-and-instruction-tuned-large-language-models-8de102c785a6?WT.mc_id=academic-105485-koreyst) 是在基礎模型上，透過範例或輸入/輸出對（例如多輪「訊息」）進行微調，這些範例包含明確指令，AI 回應會嘗試遵循這些指令。

此方法使用人類反饋強化學習（RLHF）等技術，訓練模型 _遵循指令_ 並 _從反饋中學習_，使回應更適合實際應用，且更符合使用者目標。

我們來試試——回到上方提示，將 _系統訊息_ 改為以下指令作為上下文：

> _為二年級學生摘要你所提供的內容。結果保持一段文字，並附上 3-5 個重點條列。_

你會看到結果已調整為符合目標與格式。教育者現在可以直接將此回應用於課堂簡報。

![Instruction Tuned LLM Chat Completion](../../../translated_images/04-playground-chat-instructions.b30bbfbdf92f2d051639c9bc23f74a0e2482f8dc7f0dafc6cc6fda81b2b00534.tw.png)

## 為什麼我們需要提示工程？

了解提示如何被 LLM 處理後，接著談談 _為什麼_ 需要提示工程。原因在於目前的 LLM 存在多項挑戰，使得 _可靠且一致的完成回應_ 不易達成，除非投入提示建構與優化的努力。例如：

1. **模型回應具有隨機性。** _相同提示_ 在不同模型或版本間可能產生不同回應，甚至同一模型在不同時間也可能有差異。_提示工程技巧能幫助我們降低這些變異，提供更好的護欄_。

1. **模型可能捏造回應。** 模型是以 _龐大但有限_ 的資料集預訓練，對訓練範圍外的概念缺乏知識，可能產生不準確、虛構或與已知事實相矛盾的回應。_提示工程技巧幫助使用者識別並減輕這類捏造，例如要求 AI 提供引用或推理_。

1. **模型能力會有所不同。** 新一代模型功能更豐富，但也帶來成本與複雜度的獨特挑戰。_提示工程能協助我們發展最佳實務與工作流程，抽象化差異並適應模型特定需求，實現可擴展且無縫的應用_。

讓我們在 OpenAI 或 Azure OpenAI Playground 中實際體驗：

- 用相同提示測試不同 LLM 部署（例如 OpenAI、Azure OpenAI、Hugging Face）——你有看到差異嗎？
- 用相同提示多次測試 _同一_ LLM 部署（例如 Azure OpenAI playground）——這些差異如何？

### 捏造範例

在本課程中，我們用「**捏造**」一詞來描述 LLM 有時因訓練限制或其他因素，產生事實錯誤資訊的現象。你可能在文章或研究報告中聽過「幻覺（hallucinations）」這個詞，但我們強烈建議使用「捏造」，避免將機器行為擬人化，賦予人類特質。這也符合[負責任 AI 指南](https://www.microsoft.com/ai/responsible-ai?WT.mc_id=academic-105485-koreyst)的用詞規範，避免使用在某些情境下可能具冒犯性或不包容的詞彙。

想了解捏造如何發生？想像一個提示指示 AI 生成不存在主題的內容（確保該主題不在訓練資料中）。例如——我嘗試了這個提示：
# 火星戰爭2076年課程計劃

## 課程目標
- 了解2076年火星戰爭的背景與起因
- 分析戰爭過程中的主要事件與策略
- 探討戰爭對地球與火星社會的影響
- 培養學生批判性思考與歷史分析能力

## 課程大綱

### 第一節：火星戰爭的背景
- 火星殖民的歷史簡介
- 地球與火星之間的政治與經濟緊張關係
- 主要勢力與利益衝突

### 第二節：戰爭爆發與初期衝突
- 戰爭爆發的導火線
- 重要戰役與戰術分析
- 雙方軍事技術與資源比較

### 第三節：戰爭中期與轉折點
- 重大事件與關鍵人物介紹
- 戰爭策略的變化與影響
- 國際社會的反應與介入

### 第四節：戰爭結束與後果
- 停戰協議與和平談判
- 戰爭對火星殖民地的影響
- 對地球政治與經濟的長遠影響

### 第五節：課堂討論與反思
- 學生分組討論戰爭的道德與倫理問題
- 分析戰爭教訓與未來可能的衝突預防
- 發表個人見解與總結

## 教學資源
- 相關歷史文獻與報告
- 戰爭地圖與時間軸
- 多媒體影片與紀錄片片段
- 模擬戰爭策略遊戲

## 評量方式
- 課堂參與與討論表現
- 小組報告與簡報
- 期末寫作報告：分析火星戰爭的歷史意義與啟示
網路搜尋顯示有關火星戰爭的虛構故事（例如電視劇或書籍）存在，但沒有發生在2076年的相關內容。常識也告訴我們，2076年是未來的時間，因此不可能與真實事件有關。

那麼，當我們用不同的LLM供應商執行這個提示時會發生什麼？

> **回應 1**：OpenAI Playground (GPT-35)

![Response 1](../../../translated_images/04-fabrication-oai.5818c4e0b2a2678c40e0793bf873ef4a425350dd0063a183fb8ae02cae63aa0c.tw.png)

> **回應 2**：Azure OpenAI Playground (GPT-35)

![Response 2](../../../translated_images/04-fabrication-aoai.b14268e9ecf25caf613b7d424c16e2a0dc5b578f8f960c0c04d4fb3a68e6cf61.tw.png)

> **回應 3**：Hugging Face Chat Playground (LLama-2)

![Response 3](../../../translated_images/04-fabrication-huggingchat.faf82a0a512789565e410568bce1ac911075b943dec59b1ef4080b61723b5bf4.tw.png)

如預期，每個模型（或模型版本）因隨機行為和模型能力差異，產生略有不同的回應。例如，一個模型的目標對象是八年級學生，而另一個則假設是高中生。但這三個模型都生成了可能讓不知情使用者相信該事件是真實的回應。

像是 _metaprompting_ 和 _temperature configuration_ 這類提示工程技術，能在某種程度上減少模型的虛構內容。新的提示工程 _架構_ 也將新工具和技術無縫整合到提示流程中，以緩解或降低這些影響。

## 案例研究：GitHub Copilot

讓我們以一個案例研究來結束本節，了解提示工程如何應用於真實世界的解決方案：[GitHub Copilot](https://github.com/features/copilot?WT.mc_id=academic-105485-koreyst)。

GitHub Copilot 是你的「AI 配對程式設計師」——它將文字提示轉換成程式碼補全，並整合在你的開發環境中（例如 Visual Studio Code），提供無縫的使用體驗。根據以下一系列部落格的記錄，最早版本是基於 OpenAI Codex 模型，工程師很快意識到需要微調模型並開發更好的提示工程技術，以提升程式碼品質。今年七月，他們[推出了超越 Codex 的改良 AI 模型](https://github.blog/2023-07-28-smarter-more-efficient-coding-github-copilot-goes-beyond-codex-with-improved-ai-model/?WT.mc_id=academic-105485-koreyst)，提供更快速的建議。

請依序閱讀這些文章，追蹤他們的學習歷程。

- **2023年5月** | [GitHub Copilot 在理解你的程式碼方面變得更好](https://github.blog/2023-05-17-how-github-copilot-is-getting-better-at-understanding-your-code/?WT.mc_id=academic-105485-koreyst)
- **2023年5月** | [GitHub 內部：與 GitHub Copilot 背後的 LLMs 合作](https://github.blog/2023-05-17-inside-github-working-with-the-llms-behind-github-copilot/?WT.mc_id=academic-105485-koreyst)
- **2023年6月** | [如何為 GitHub Copilot 撰寫更好的提示](https://github.blog/2023-06-20-how-to-write-better-prompts-for-github-copilot/?WT.mc_id=academic-105485-koreyst)
- **2023年7月** | [GitHub Copilot 以改良 AI 模型超越 Codex](https://github.blog/2023-07-28-smarter-more-efficient-coding-github-copilot-goes-beyond-codex-with-improved-ai-model/?WT.mc_id=academic-105485-koreyst)
- **2023年7月** | [開發者的提示工程與 LLM 指南](https://github.blog/2023-07-17-prompt-engineering-guide-generative-ai-llms/?WT.mc_id=academic-105485-koreyst)
- **2023年9月** | [如何打造企業級 LLM 應用：GitHub Copilot 的經驗分享](https://github.blog/2023-09-06-how-to-build-an-enterprise-llm-application-lessons-from-github-copilot/?WT.mc_id=academic-105485-koreyst)

你也可以瀏覽他們的[工程部落格](https://github.blog/category/engineering/?WT.mc_id=academic-105485-koreyst)，閱讀更多像是[這篇](https://github.blog/2023-09-27-how-i-used-github-copilot-chat-to-build-a-reactjs-gallery-prototype/?WT.mc_id=academic-105485-koreyst)的文章，展示這些模型和技術如何被 _應用_ 於推動真實世界的應用。

---

<!--
LESSON TEMPLATE:
本單元應涵蓋核心概念 #2。
以範例和參考資料強化此概念。

CONCEPT #2:
提示設計。
以範例說明。
-->

## 提示構建

我們已經了解為什麼提示工程很重要，現在讓我們理解提示是如何 _構建_ 的，這樣才能評估不同技術以設計更有效的提示。

### 基本提示

先從基本提示開始：一個純文字輸入送給模型，沒有其他上下文。以下是一個例子——當我們將美國國歌的前幾個字送到 OpenAI [Completion API](https://platform.openai.com/docs/api-reference/completions?WT.mc_id=academic-105485-koreyst) 時，它會立即 _補全_ 後續幾行，展示基本的預測行為。

| 提示（輸入）       | 補全（輸出）                                                                                                                             |
| :----------------- | :--------------------------------------------------------------------------------------------------------------------------------------- |
| Oh say can you see | 聽起來你正在開始唱「星條旗永不落」的歌詞，美國的國歌。完整歌詞是...                                                                       |

### 複雜提示

現在讓我們在基本提示中加入上下文和指令。[Chat Completion API](https://learn.microsoft.com/azure/ai-services/openai/how-to/chatgpt?WT.mc_id=academic-105485-koreyst) 允許我們將複雜提示構建為一組 _訊息_，包含：

- 反映 _使用者_ 輸入和 _助理_ 回應的輸入/輸出對。
- 設定助理行為或個性的系統訊息。

請求現在呈現如下形式，其中 _分詞_ 有效捕捉上下文和對話中的相關資訊。改變系統上下文對補全品質的影響，與使用者輸入同樣重要。

```python
response = openai.chat.completions.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Who won the world series in 2020?"},
        {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
        {"role": "user", "content": "Where was it played?"}
    ]
)
```

### 指令提示

在上述範例中，使用者提示是簡單的文字查詢，可解讀為資訊請求。使用 _指令_ 提示時，我們可以用文字更詳細地指定任務，給 AI 更明確的指引。以下是一個例子：

| 提示（輸入）                                                                                                                                                                                                                         | 補全（輸出）                                                                                                        | 指令類型            |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------- | :------------------ |
| Write a description of the Civil War                                                                                                                                                                                                   | _回傳一段簡短描述_                                                                                                  | 簡單                |
| Write a description of the Civil War. Provide key dates and events and describe their significance                                                                                                                                     | _回傳一段描述，接著列出重要事件日期及說明_                                                                         | 複雜                |
| Write a description of the Civil War in 1 paragraph. Provide 3 bullet points with key dates and their significance. Provide 3 more bullet points with key historical figures and their contributions. Return the output as a JSON file | _回傳更詳盡內容，格式為可複製貼上並驗證的 JSON 檔案_                                                             | 複雜。格式化。      |

## 主要內容

在上述範例中，提示仍相當開放，讓 LLM 決定其預訓練資料中哪些部分相關。使用 _主要內容_ 設計模式時，輸入文字分為兩部分：

- 指令（動作）
- 相關內容（影響動作）

以下是一個例子，指令是「用兩句話摘要這段內容」。

| 提示（輸入）                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | 補全（輸出）                                                                                                                                                                                                                                                                             |
| :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Jupiter is the fifth planet from the Sun and the largest in the Solar System. It is a gas giant with a mass one-thousandth that of the Sun, but two-and-a-half times that of all the other planets in the Solar System combined. Jupiter is one of the brightest objects visible to the naked eye in the night sky, and has been known to ancient civilizations since before recorded history. It is named after the Roman god Jupiter.[19] When viewed from Earth, Jupiter can be bright enough for its reflected light to cast visible shadows,[20] and is on average the third-brightest natural object in the night sky after the Moon and Venus. <br/> **Summarize this in 2 short sentences** | 木星是太陽系中第五顆行星，也是最大的一顆。它是氣態巨星，質量是太陽的千分之一，但比其他所有行星質量總和還多兩倍半，並且是夜空中肉眼可見最明亮的天體之一。 |

主要內容段落可用多種方式來驅動更有效的指令：

- **範例** — 不直接告訴模型要做什麼，而是給它範例，讓它推斷模式。
- **提示** — 在指令後加上「提示」，引導模型產生更相關的回應。
- **範本** — 可重複使用的提示「配方」，帶有可用資料自訂的佔位符（變數），適用於特定用例。

接下來讓我們實際看看這些用法。

### 使用範例

這種方法是用主要內容「餵給模型」一些期望輸出的範例，讓它推斷出想要的輸出模式。根據範例數量，我們有零次提示、一次提示、少次提示等。

提示現在包含三個部分：

- 任務描述
- 幾個期望輸出的範例
- 新範例的開始（隱含任務描述）

| 學習類型   | 提示（輸入）                                                                                                                                        | 補全（輸出）           |
| :--------- | :-------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------- |
| 零次提示   | "The Sun is Shining". Translate to Spanish                                                                                                        | "El Sol está brillando". |
| 一次提示   | "The Sun is Shining" => "El Sol está brillando". <br> "It's a Cold and Windy Day" =>                                                               | "Es un día frío y ventoso". |
| 少次提示   | The player ran the bases => Baseball <br/> The player hit an ace => Tennis <br/> The player hit a six => Cricket <br/> The player made a slam-dunk => | Basketball              |
|            |                                                                                                                                                     |                        |

注意零次提示中必須明確指示「翻譯成西班牙語」，但一次提示中則由範例推斷。少次提示則展示了多個範例如何幫助模型更準確推斷，且不需額外指令。

### 提示線索

另一種使用主要內容的技巧是提供 _線索_ 而非範例。在這種情況下，我們用一段反映期望回應格式的片段「啟動」模型，模型便會「接收線索」並沿著該方向繼續。

| 線索數量 | 提示（輸入）                                                                                                                                                                                                                                                                                                                                                                                                                                               | 補全（輸出）                                                                                                                                                                                                                                                                                       |
| :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0        | Jupiter is the fifth planet from the Sun and the largest in the Solar System. It is a gas giant with a mass one-thousandth that of the Sun, but two-and-a-half times that of all the other planets in the Solar System combined. Jupiter is one of the brightest objects visible to the naked eye in the night sky, and has been known to ancient civilizations since before recorded history.

**Summarize This**                                       | 木星是太陽系中最大的行星，位於太陽的第五顆行星。它是一顆氣體巨星，質量約為太陽的千分之一，但重量超過其他所有行星的總和。古代文明早已認識木星，且它在夜空中非常容易被看見。 |
| 1              | 木星是太陽系中第五顆行星，也是最大的行星。它是一顆氣體巨星，質量約為太陽的千分之一，但比太陽系中其他所有行星的總和還要重兩倍半。木星是夜空中肉眼可見的最亮天體之一，早在有文字記錄之前的古代文明就已知曉它。<br/>**Summarize This** <br/> 我們學到的是木星 | 是太陽系中第五顆行星，也是最大的行星。它是一顆氣體巨星，質量約為太陽的千分之一，但比其他所有行星的總和還要重兩倍半。它肉眼可見，且自古代以來就為人所知。                        |
| 2              | 木星是太陽系中第五顆行星，也是最大的行星。它是一顆氣體巨星，質量約為太陽的千分之一，但比太陽系中其他所有行星的總和還要重兩倍半。木星是夜空中肉眼可見的最亮天體之一，早在有文字記錄之前的古代文明就已知曉它。<br/>**Summarize This** <br/> 我們學到的三大重點：         | 1. 木星是太陽系中第五顆行星，也是最大的行星。<br/> 2. 它是一顆氣體巨星，質量約為太陽的千分之一...<br/> 3. 木星自古代以來就能用肉眼看見...                                                                       |
|                |                                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                           |

### Prompt Templates

提示範本是一種 _預先定義好的提示配方_，可以儲存並在需要時重複使用，以推動更一致且大規模的使用者體驗。最簡單的形式，它就是一組提示範例，例如[OpenAI 的這個範例](https://platform.openai.com/examples?WT.mc_id=academic-105485-koreyst)，提供互動式提示元件（使用者與系統訊息）以及 API 請求格式，方便重複使用。

在更複雜的形式中，如[LangChain 的範例](https://python.langchain.com/docs/concepts/prompt_templates/?WT.mc_id=academic-105485-koreyst)，它包含了 _佔位符_，可以用來替換來自各種來源的資料（使用者輸入、系統上下文、外部資料來源等），以動態生成提示。這讓我們能建立一個可重複使用的提示庫，**以程式化方式**推動一致的使用者體驗。

最後，範本的真正價值在於能創建並發佈 _垂直應用領域的提示庫_，這些提示範本會根據特定應用的上下文或範例進行 _優化_，使回應對目標使用者更具相關性與準確性。[Prompts For Edu](https://github.com/microsoft/prompts-for-edu?WT.mc_id=academic-105485-koreyst) 倉庫就是這種做法的絕佳範例，專注於教育領域，強調課程規劃、課程設計、學生輔導等核心目標。

## Supporting Content

如果我們把提示建構視為包含指令（任務）和目標（主要內容），那麼 _次要內容_ 就像是額外的上下文，用來**影響輸出結果**。它可能是調整參數、格式指示、主題分類等，有助於模型 _調整_ 回應以符合預期的使用者目標或期望。

舉例來說：給定一份包含豐富元資料（名稱、描述、等級、標籤、講師等）的課程目錄：

- 我們可以定義一個指令：「總結 2023 年秋季的課程目錄」
- 使用主要內容提供幾個期望輸出的範例
- 使用次要內容標示出最重要的五個「標籤」

這樣模型就能以範例中展示的格式提供摘要；若結果包含多個標籤，則會優先考慮次要內容中標示的五個標籤。

---

<!--
LESSON TEMPLATE:
本單元應涵蓋核心概念 #1。
用範例和參考資料加強該概念。

概念 #3：
提示工程技術。
有哪些基本的提示工程技巧？
用練習來說明。
-->

## Prompting Best Practices

既然我們知道如何 _建構_ 提示，就可以開始思考如何 _設計_ 它們以符合最佳實務。我們可以從兩個面向來看：擁有正確的 _心態_ 和運用合適的 _技巧_。

### Prompt Engineering Mindset

提示工程是一個反覆試驗的過程，請記住三個大方向：

1. **領域理解很重要。** 回應的準確性與相關性取決於應用或使用者所處的 _領域_。運用你的直覺和領域專業來 **進一步客製化技巧**。例如，在系統提示中定義 _領域專屬的角色設定_，或在使用者提示中使用 _領域專屬範本_。提供反映領域上下文的次要內容，或用 _領域專屬的提示與範例_ 引導模型朝熟悉的使用模式。

2. **模型理解很重要。** 我們知道模型本質上是隨機的，但不同模型的訓練資料（預訓練知識）、功能（API 或 SDK 提供的能力）及優化內容類型（程式碼、圖片、文字等）都可能不同。了解你所使用模型的優勢與限制，並利用這些知識來 _優先安排任務_ 或建立 _針對模型能力優化的客製範本_。

3. **反覆與驗證很重要。** 模型和提示工程技術都在快速演進。作為領域專家，你可能有其他特定應用的背景或標準，這些不一定適用於更廣泛的社群。利用提示工程工具與技巧「快速啟動」提示建構，然後用你的直覺和領域專業反覆驗證結果。記錄你的見解並建立一個 **知識庫**（例如提示庫），讓其他人能以此為新基準，加速未來的迭代。

## Best Practices

接下來看看 [OpenAI](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api?WT.mc_id=academic-105485-koreyst) 和 [Azure OpenAI](https://learn.microsoft.com/azure/ai-services/openai/concepts/prompt-engineering#best-practices?WT.mc_id=academic-105485-koreyst) 實務者推薦的常見最佳做法。

| 事項                              | 原因                                                                                                                                                                                                                                               |
| :-------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 評估最新模型                      | 新一代模型通常功能更強、品質更好，但成本可能較高。評估其影響後，再決定是否遷移。                                                                                                                                                |
| 分開指令與上下文                | 確認你的模型或服務提供者是否定義了用來區分指令、主要與次要內容的 _分隔符_，這有助於模型更精確地分配權重給各個詞元。                                                                                                                         |
| 具體且清楚                      | 提供更多關於期望上下文、結果、長度、格式、風格等細節，能提升回應的品質與一致性。將這些做法記錄在可重用的範本中。                                                                                                                          |
| 詳細描述並使用範例              | 模型通常對「示範教學」的方式反應更好。先用「零次學習」（zero-shot）給出指令（無範例），再用「少次學習」（few-shot）提供幾個期望輸出的範例作為精煉。也可使用類比說明。                                                                 |
| 使用提示詞引導完成              | 透過給模型一些開頭詞或片語，幫助它從這些線索開始產生回應，朝向期望結果。                                                                                                               |
| 重複強調                        | 有時需要對模型重複指令。可在主要內容前後都給指令，或同時使用指令與提示詞等。反覆嘗試並驗證什麼方法有效。                                                                                                                         |
| 順序很重要                      | 呈現資訊給模型的順序可能影響輸出結果，尤其在學習範例中，因為模型有近期偏好。嘗試不同順序找出最佳方式。                                                                                                                               |
| 給模型「退路」                  | 提供模型一個 _備用_ 回應，當它無法完成任務時可使用，能降低模型產生錯誤或捏造回應的機率。                                                                                                                         |
|                                   |                                                                                                                                                                                                                                                   |

如同任何最佳實務，請記得根據模型、任務與領域不同，_你的情況可能有所差異_。將這些作為起點，持續迭代找出最適合你的做法。隨著新模型與工具問世，持續重新評估你的提示工程流程，重點放在流程可擴展性與回應品質。

<!--
LESSON TEMPLATE:
本單元若適用，應提供程式碼挑戰。

挑戰：
連結到一個 Jupyter Notebook，指令中只有程式碼註解（程式碼區塊為空）。

解答：
連結到填寫並執行過的 Notebook，展示一個範例解答。
-->

## Assignment

恭喜你完成本課程！現在是時候用實際範例來測試這些概念與技巧了！

這次作業會使用一個 Jupyter Notebook，裡面有你可以互動完成的練習。你也可以自行在 Notebook 裡新增 Markdown 與程式碼區塊，探索更多想法與技巧。

### 開始前，先 fork 這個 repo，然後

- （推薦）啟動 GitHub Codespaces
- （或）將 repo 複製到本地端，並用 Docker Desktop 運行
- （或）用你偏好的 Notebook 執行環境開啟 Notebook

### 接著，設定環境變數

- 將 repo 根目錄的 `.env.copy` 複製為 `.env`，並填入 `AZURE_OPENAI_API_KEY`、`AZURE_OPENAI_ENDPOINT` 和 `AZURE_OPENAI_DEPLOYMENT`。完成後回到[學習沙盒章節](../../../04-prompt-engineering-fundamentals/04-prompt-engineering-fundamentals)了解如何操作。

### 然後，打開 Jupyter Notebook

- 選擇執行核心。如果使用前兩種方式，直接選擇開發容器提供的預設 Python 3.10.x 核心即可。

你已準備好執行練習。請注意，這裡沒有「對錯」答案，重點是透過反覆嘗試探索不同選項，並建立對特定模型與應用領域有效方法的直覺。

_因此本課程沒有程式碼解答區塊。Notebook 中會有標題為「My Solution:」的 Markdown 區塊，展示一個範例輸出供參考。_

 <!--
LESSON TEMPLATE:
用摘要與自學資源結尾本節。
-->

## Knowledge check

以下哪一個提示符合合理的最佳實務？

1. 顯示一張紅色汽車的圖片
2. 顯示一張紅色 Volvo XC90 汽車停在懸崖邊夕陽下的圖片
3. 顯示一張紅色 Volvo XC90 汽車的圖片

答：2 是最佳提示，因為它提供了「什麼」的細節，並具體描述（不只是任何車，而是特定品牌與車型），還描述了整體場景。3 次之，因為也包含不少描述。

## 🚀 Challenge

試試看用提示詞技巧完成句子：「顯示一張紅色 Volvo 汽車的圖片，並且……」。模型會怎麼回應？你會如何改進它？

## Great Work! Continue Your Learning

想了解更多提示工程的概念？請前往[進階學習頁面](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst)，尋找更多優質資源。

接著前往第 5 課，我們將探討[進階提示技巧](../05-advanced-prompts/README.md?WT.mc_id=academic-105485-koreyst)！

**免責聲明**：  
本文件係使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應視為權威來源。對於重要資訊，建議採用專業人工翻譯。我們不對因使用本翻譯而產生的任何誤解或誤譯負責。