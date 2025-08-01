<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a45c318dc6ebc2604f35b8b829f93af2",
  "translation_date": "2025-07-09T09:07:44+00:00",
  "source_file": "04-prompt-engineering-fundamentals/README.md",
  "language_code": "zh-tw"
}
-->
# 提示工程基礎

[![提示工程基礎](../../../translated_images/04-lesson-banner.a2c90deba7fedacda69f35b41636a8951ec91c2e33f5420b1254534ac85bc18e.en.png)](https://aka.ms/gen-ai-lesson4-gh?WT.mc_id=academic-105485-koreyst)

## 簡介
本模組涵蓋了在生成式 AI 模型中製作有效提示的關鍵概念和技術。您如何向 LLM 撰寫提示也很重要。一個精心設計的提示可以帶來更高品質的回應。但「提示」和「提示工程」這些術語到底是什麼意思？我該如何改善我傳送給 LLM 的提示「輸入」？這些是我們將在本章和下一章中探討的問題。

「生成式 AI」可以根據使用者要求建立新內容（例如文字、影像、音訊、程式碼等）。它使用像 OpenAI 的 GPT（「生成式預訓練轉換器」）系列這樣的大型語言模型來做到這一點，這些模型經過訓練以理解自然語言和程式碼。

使用者現在可以透過聊天等熟悉的格式與這些模型互動，而無需技術技能或訓練。這些模型是「基於提示的」——使用者傳送文字輸入（提示）並接收 AI 回應（完成）。然後他們可以與 AI 進行多輪「聊天」，完善他們的提示，直到回應滿足他們的需求。

「提示」已成為生成式 AI 應用程式的主要「程式設計介面」，它告訴模型該做什麼，並影響回應的品質。「提示工程」是一個快速發展的領域，專注於提示的「設計和優化」，以大規模地持續提供高品質的回應。

## 學習目標

在本課中，我們將學習什麼是提示工程、它為何重要，以及如何為給定的模型和應用程式目標建立更有效的提示。我們將涵蓋提示工程的核心概念和最佳實務——並探索一個互動式的 Jupyter Notebooks「沙箱」環境，您可以在其中看到這些想法在實際範例中的應用。

在本課結束時，您將能夠：

1. 解釋什麼是提示工程及其重要性。
2. 描述提示的組成部分及其使用方式。
3. 學習提示工程的最佳實務和技術。
4. 使用 OpenAI 端點將這些技術應用於實際範例。

## 關鍵術語

提示工程：設計和完善輸入以引導 AI 模型產生所需輸出的實務。
權杖化：將文字分解為稱為權杖的較小單元，模型可以理解和處理這些單元。
指令調整的 LLM：經過特定指令微調的大型語言模型 (LLM)，以提高回應的準確性和相關性。

## 學習沙箱

提示工程目前更像是一門藝術而非科學。建立直覺的最佳方法是「多加練習」，並採用反覆試驗的方法，將領域專業知識與推薦的技術和特定於模型的調整相結合。

本課程隨附的 Jupyter Notebook 提供了一個「沙箱」環境，您可以在其中嘗試所學的內容——無論是邊學邊做，還是作為最後的程式碼挑戰的一部分。若要執行練習，您需要：

1. **一個 Azure OpenAI API 金鑰**——已部署 LLM 的服務端點。
2. **一個 Python 執行階段**——以執行筆記本。
3. **本機環境變數**——「立即完成 [設定](./../00-course-setup/SETUP.md?WT.mc_id=academic-105485-koreyst) 步驟以做好準備」。

筆記本包含「入門」練習，但鼓勵您新增自己的「Markdown」（說明）和「程式碼」（提示請求）部分，以實驗更多範例或想法——並培養您的提示設計技能。

## 圖解指南

想在深入學習之前了解本課涵蓋的內容嗎？請查看此圖解指南，其中重點介紹了每個主題的主要內容和關鍵要點。課程藍圖將帶您從了解核心概念和挑戰，到使用相關的提示工程技術和最佳實務來解決這些問題。請注意，本指南中的「進階技術」部分指的是本課程「下一章」涵蓋的內容。

![提示工程圖解指南](../../../translated_images/04-prompt-engineering-sketchnote.d5f33336957a1e4f623b826195c2146ef4cc49974b72fa373de6929b474e8b70.en.png)

## 我們的新創公司

現在，讓我們將「這個主題」與我們的新創公司使命連結起來，以[將 AI 創新帶入教育](https://educationblog.microsoft.com/2023/06/collaborating-to-bring-ai-innovation-to-education?WT.mc_id=academic-105485-koreyst)。我們希望為「個人化學習」建立 AI 驅動的應用程式——所以讓我們來思考一下我們應用程式的不同使用者可能會如何「設計」提示：

- **管理員**可能會要求 AI「分析課程資料以找出涵蓋範圍的差距」。AI 可以摘要結果或用程式碼將其視覺化。
- **教育工作者**可能會要求 AI「為目標受眾和主題產生一份課程計畫」。AI 可以以指定的格式建立一份個人化的計畫。
- **學生**可能會要求 AI「在困難的科目上輔導他們」。AI 可以用適合他們程度的課程、提示和範例來引導學生。

這只是個開始。請查看 [教育提示](https://github.com/microsoft/prompts-for-edu/tree/main?WT.mc_id=academic-105485-koreyst)——一個由教育專家策劃的開源提示庫——以探索更多可能性！「嘗試在沙箱或 OpenAI 遊樂場中執行其中一些提示，看看會發生什麼事！」

<!--
課程範本：
本單元應涵蓋核心概念 #1。
用範例和參考資料來強化概念。

概念 #1：
提示工程。
定義它並解釋為何需要它。
-->

## 什麼是提示工程？

我們在本課開始時將**提示工程**定義為「設計和優化」文字輸入（提示）的過程，以便為給定的應用程式目標和模型持續提供高品質的回應（完成）。您可以將此視為一個兩步驟的過程：

- 「設計」特定模型和目標的初始提示
- 反覆「完善」提示以提高回應品質

這本質上是一個反覆試驗的過程，需要使用者的直覺和努力才能獲得最佳結果。那麼它為何重要呢？要回答這個問題，我們首先需要了解三個概念：

- 「權杖化」= 模型如何「看待」提示
- 「基礎 LLM」= 基礎模型如何「處理」提示
- 「指令調整的 LLM」= 模型現在如何理解「任務」

### 權杖化

LLM 將提示視為一個「權杖序列」，而不同的模型（或版本）可能會以不同的方式對同一個提示進行權杖化。由於 LLM 是在權杖（而非原始文字）上進行訓練的，因此提示的權杖化方式會直接影響所產生回應的品質。

若要感受一下權杖化，請嘗試使用像下面顯示的 [OpenAI 權杖化器](https://platform.openai.com/tokenizer?WT.mc_id=academic-105485-koreyst) 等工具。貼上您的提示，看看它是如何被分解成權杖的，並注意空格和標點符號的處理方式。請注意，此範例使用的是較舊的 LLM (GPT-3)，因此較新的模型可能會以不同的方式進行權杖化。

![權杖化](../../../translated_images/04-tokenizer-example.e71f0a0f70356c5c7d80b21e8753a28c18a7f6d4aaa1c4b08e65d17625e85642.en.png)

### 概念：基礎模型

一旦提示被權杖化，["基礎 LLM"](https://blog.gopenai.com/an-introduction-to-base-and-instruction-tuned-large-language-models-8de102c785a6?WT.mc_id=academic-105485-koreyst)（或基礎模型）的主要工作就是預測序列中的下一個權杖。由於 LLM 是在大量的文字資料集上訓練的，它們了解權杖之間的統計關係，並且可以有信心地進行預測。請注意，它們不了解單字的「意義」；它們只是辨識出它們可以用下一個預測來「完成」的模式。它們會繼續預測權杖，直到被使用者或預設條件停止。

想看看基於提示的完成是如何運作的嗎？將上面的提示輸入到 Azure OpenAI Studio 的「聊天遊樂場」中，並使用預設設定。系統會將提示視為資訊請求，因此您應該會看到一個符合此上下文的完成。

但如果使用者想要一個符合特定標準或任務的特定輸出呢？這就是「指令調整」的 LLM 發揮作用的地方。

![基礎 LLM 聊天完成](../../../translated_images/04-playground-chat-base.65b76fcfde0caa6738e41d20f1a6123f9078219e6f91a88ee5ea8014f0469bdf.en.png)

### 概念：指令調整的 LLM

一個[指令調整的 LLM](https://blog.gopenai.com/an-introduction-to-base-and-instruction-tuned-large-language-models-8de102c785a6?WT.mc_id=academic-105485-koreyst) 從基礎模型開始，並使用範例或輸入/輸出對（例如，多輪「訊息」）對其進行微調，這些範例或輸入/輸出對包含明確的指令——而 AI 的回應會嘗試遵循這些指令。

這使用了諸如「人類回饋強化學習」(RLHF) 等技術來訓練模型「遵循指令」和「從回饋中學習」，從而產生更適合實際應用且與使用者目標更相關的回應。

讓我們來試試看——重新檢視上面的提示，但現在更改「系統訊息」以提供此指令作為上下文：

> 「為二年級學生摘要您所獲得的內容。將結果保持在一個段落內，並包含 3-5 個要點。」

注意到回應現在如何與所需的目標和格式保持一致了嗎？教育工作者可以直接在他們的課堂投影片中使用這個。

![指令調整的 LLM 聊天完成](../../../translated_images/04-playground-chat-instructions.b30bbfbdf92f2d051639c9bc23f74a0e2482f8dc7f0dafc6cc6fda81b2b00534.en.png)

## 為何我們需要提示工程？

現在我們了解了 LLM 如何處理提示，讓我們來討論「為何」需要提示工程。答案在於，目前的 LLM 存在一些挑戰，如果沒有仔細的提示設計和優化，就很難實現「可靠且一致的完成」。例如：

1. **模型回應是隨機的。** 「相同的提示」在不同的模型或版本中可能會產生不同的回應。它甚至可能在不同的時間使用「相同的模型」產生不同的結果。「提示工程技術有助於透過提供更好的護欄來減少這些變化」。

2. **模型可能會捏造回應。** 模型是在「龐大但有限」的資料集上預先訓練的，因此它們缺乏超出其訓練資料的知識。因此，它們可能會產生不準確、捏造或與已知事實相矛盾的完成。「提示工程有助於使用者偵測和減少此類捏造，例如透過要求 AI 提供引文或推理」。

3. **模型能力各不相同。** 較新的模型或世代具有更豐富的能力，但在成本和複雜性方面也存在獨特的怪癖和權衡。「提示工程有助於開發最佳實務和工作流程，以抽象化這些差異，並以可擴展、無縫的方式適應特定於模型的需求」。

在 OpenAI 或 Azure OpenAI 遊樂場中親自嘗試一下：

- 使用相同的提示搭配不同的 LLM 部署（例如 OpenAI、Azure OpenAI、Hugging Face）——您是否注意到差異？
- 重複使用相同的提示搭配「相同」的 LLM 部署（例如 Azure OpenAI 遊樂場）——回應有何不同？

### 捏造範例

在本課程中，我們使用「捏造」一詞來描述 LLM 因訓練限制或其他限制而產生事實上不正確的資訊。您可能在熱門文章或研究論文中聽過這個詞被稱為「幻覺」。然而，我們建議使用「捏造」來避免將人類般的特徵歸因於機器產生的輸出來擬人化這種行為。這也符合[負責任的 AI 指南](https://www.microsoft.com/ai/responsible-ai?WT.mc_id=academic-105485-koreyst)，避免使用在某些情況下可能具有冒犯性或非包容性的術語。

想看看捏造是如何發生的嗎？想一個提示，要求 AI 產生關於一個不存在的主題的內容（確保它不在訓練資料中）。例如——我嘗試了這個提示：
# 課程計畫：2076 年的火星戰爭

## 目標
在本課結束時，學生將了解 2076 年火星戰爭的關鍵事件、原因和後果。他們將能夠分析衝突對地球和火星的政治和社會影響。

## 所需材料
- 2076 年火星戰爭的時間軸
- 戰爭期間火星和地球的地圖
- 主要來源的摘錄（信件、演講、官方文件）
- 關於戰爭主要戰役和策略的多媒體簡報

## 課程大綱

### 簡介（10 分鐘）
- 簡要概述 2076 年之前的火星殖民
- 討論地球政府與火星殖民者之間的緊張關係
- 介紹戰爭的主要原因

### 主要活動（30 分鐘）
- 將學生分組分析戰爭的不同階段：
  - 第 1 階段：初期衝突和小規模戰鬥
  - 第 2 階段：主要戰役和轉捩點
  - 第 3 階段：和平談判和後果
- 每組用支持性證據呈現他們的發現

### 討論（15 分鐘）
- 探討戰爭的政治和社會後果
- 辯論殖民和叛亂的倫理意涵
- 將戰爭的結果與當前的火星-地球關係聯繫起來

### 結論（5 分鐘）
- 總結要點
- 指派一篇關於 2076 年火星戰爭如何塑造星際外交的反思性文章

## 評量
- 根據準確性和分析深度評估小組報告
- 根據批判性思維和對主題的理解對反思性文章進行評分

## 額外資源
- 紀錄片：「火星戰爭：歷史的轉捩點」
- 互動式地圖：2076 年火星戰爭的戰役
- 衝突時期的主要文件檔案庫
網路搜尋告訴我，有關於火星戰爭的虛構故事（例如，電視劇或書籍）——但沒有一個設定在 2076 年。常識也告訴我們，2076 年是「未來」，因此不可能與真實事件聯繫起來。

那麼，當我們用不同的 LLM 提供者執行這個提示時會發生什麼事呢？

> **回應 1**：OpenAI 遊樂場 (GPT-35)

![回應 1](../../../translated_images/04-fabrication-oai.5818c4e0b2a2678c40e0793bf873ef4a425350dd0063a183fb8ae02cae63aa0c.en.png)

> **回應 2**：Azure OpenAI 遊樂場 (GPT-35)

![回應 2](../../../translated_images/04-fabrication-aoai.b14268e9ecf25caf613b7d424c16e2a0dc5b578f8f960c0c04d4fb3a68e6cf61.en.png)

> **回應 3**：：Hugging Face 聊天遊樂場 (LLama-2)

![回應 3](../../../translated_images/04-fabrication-huggingchat.faf82a0a512789565e410568bce1ac911075b943dec59b1ef4080b61723b5bf4.en.png)

正如預期的那樣，由於隨機行為和模型能力的差異，每個模型（或模型版本）都會產生略有不同的回應。例如，一個模型針對八年級的受眾，而另一個模型則假設是高中生。但所有三個模型產生的回應都可能讓不知情的使用者相信該事件是真實的。

像「元提示」和「溫度設定」這樣的提示工程技術可以在一定程度上幫助減少模型的捏造。新的提示工程「架構」也將新的工具和技術無縫地整合到提示流程中，以減輕或減少其中一些影響。

## 案例研究：GitHub Copilot

讓我們透過一個案例研究來總結本節：[GitHub Copilot](https://github.com/features/copilot?WT.mc_id=academic-105485-koreyst)，探討提示工程如何在現實世界的解決方案中應用。

GitHub Copilot 是您的「AI 配對程式設計師」——它將文字提示轉換為程式碼完成，並直接整合到您的開發環境（例如 Visual Studio Code）中，以提供流暢的使用者體驗。如下面的部落格系列所記錄，最早的版本是基於 OpenAI Codex 模型——工程師很快就意識到需要微調模型並開發更好的提示工程技術來提高程式碼品質。7 月，他們[推出了一個超越 Codex 的改良 AI 模型](https://github.blog/2023-07-28-smarter-more-efficient-coding-github-copilot-goes-beyond-codex-with-improved-ai-model/?WT.mc_id=academic-105485-koreyst)，以提供更快的建議。

依序閱讀文章以了解他們的學習歷程。

- **2023 年 5 月** | [GitHub Copilot 在理解您的程式碼方面越來越好](https://github.blog/2023-05-17-how-github-copilot-is-getting-better-at-understanding-your-code/?WT.mc_id=academic-105485-koreyst)
- **2023 年 5 月** | [GitHub 內部：與 GitHub Copilot 背後的 LLM 合作](https://github.blog/2023-05-17-inside-github-working-with-the-llms-behind-github-copilot/?WT.mc_id=academic-105485-koreyst)
- **2023 年 6 月** | [如何為 GitHub Copilot 撰寫更好的提示](https://github.blog/2023-06-20-how-to-write-better-prompts-for-github-copilot/?WT.mc_id=academic-105485-koreyst)
- **2023 年 7 月** | [GitHub Copilot 透過改良的 AI 模型超越 Codex](https://github.blog/2023-07-28-smarter-more-efficient-coding-github-copilot-goes-beyond-codex-with-improved-ai-model/?WT.mc_id=academic-105485-koreyst)
- **2023 年 7 月** | [開發人員的提示工程與 LLM 指南](https://github.blog/2023-07-17-prompt-engineering-guide-generative-ai-llms/?WT.mc_id=academic-105485-koreyst)
- **2023 年 9 月** | [如何建置企業級 LLM 應用程式：來自 GitHub Copilot 的經驗](https://github.blog/2023-09-06-how-to-build-an-enterprise-llm-application-lessons-from-github-copilot/?WT.mc_id=academic-105485-koreyst)

您也可以瀏覽他們的[工程部落格](https://github.blog/category/engineering/?WT.mc_id=academic-105485-koreyst)以取得更多像[這篇](https://github.blog/2023-09-27-how-i-used-github-copilot-chat-to-build-a-reactjs-gallery-prototype/?WT.mc_id=academic-105485-koreyst)這樣的文章，其中展示了這些模型和技術如何「應用」於為現實世界的應用程式提供動力。

---

<!--
課程範本：
本單元應涵蓋核心概念 #2。
用範例和參考資料來強化概念。

概念 #2：
提示設計。
用範例說明。
-->

## 提示建構

我們已經了解了提示工程為何重要——現在讓我們來了解提示是如何「建構」的，以便我們可以評估設計更有效提示的不同技術。

### 基本提示

讓我們從基本提示開始：一個傳送給模型的文字輸入，沒有任何額外的上下文。這裡有一個例子——當我們將美國國歌的前幾個字傳送給 OpenAI [完成 API](https://platform.openai.com/docs/api-reference/completions?WT.mc_id=academic-105485-koreyst) 時，它會立即用接下來的幾行「完成」回應，展示了基本的預測行為。

| 提示（輸入） | 完成（輸出） |
| :--- | :--- |
| Oh say can you see | 聽起來您正在開始唱美國國歌「星條旗」的歌詞。完整的歌詞是... |

### 複雜提示

現在讓我們在那個基本提示中加入上下文和指令。 [聊天完成 API](https://learn.microsoft.com/azure/ai-services/openai/how-to/chatgpt?WT.mc_id=academic-105485-koreyst) 讓我們可以將一個複雜的提示建構成一系列的「訊息」，其中包含：

- 反映「使用者」輸入和「助理」回應的輸入/輸出對。
- 設定助理行為或個性的上下文的系統訊息。

請求現在看起來像下面的範例，其中「權杖化」有效地從上下文和對話中擷取相關資訊。更改系統上下文對完成品質的影響可能與提供的使用者輸入一樣大。

```python
response = openai.chat.completions.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "您是一位樂於助人的助理。"},
        {"role": "user", "content": "2020 年世界大賽冠軍是誰？"},
        {"role": "assistant", "content": "洛杉磯道奇隊贏得了 2020 年世界大賽冠軍。"},
        {"role": "user", "content": "比賽在哪裡舉行？"}
    ]
)
```

### 指令提示

在上面的範例中，使用者提示是一個簡單的文字查詢，可以解釋為資訊請求。使用「指令」提示，我們使用該文字更詳細地指定任務，為 AI 提供更清晰的指引。這裡有一個範例：

| 提示（輸入） | 完成（輸出） | 指令類型 |
| :--- | :--- | :--- |
| 撰寫一段關於內戰的描述 | 「傳回一個簡單的段落」 | 簡單 |
| 撰寫一段關於內戰的描述。提供關鍵日期和事件，並描述其意義 | 「傳回一個段落，後面跟著一個包含描述的關鍵事件日期清單」 | 複雜 |
| 用 1 個段落撰寫一段關於內戰的描述。提供 3 個包含關鍵日期及其意義的要點。再提供 3 個包含關鍵歷史人物及其貢獻的要點。以 JSON 檔案格式傳回輸出 | 「在文字方塊中傳回更詳細的資訊，格式化為 JSON，您可以複製貼上到檔案中並視需要進行驗證」 | 複雜。已格式化。 |

## 主要內容

在上面的範例中，提示仍然相當開放，讓 LLM 可以決定其預訓練資料的哪些部分是相關的。使用「主要內容」設計模式，輸入文字被分成兩部分：

- 一個指令（動作）
- 相關內容（影響動作）

這裡有一個例子，指令是「用 2 個句子摘要這個」。

| 提示（輸入） | 完成（輸出） |
| :--- | :--- |
| 木星是距離太陽第五顆行星，也是太陽系中最大的行星。它是一顆氣態巨行星，質量是太陽的千分之一，但卻是太陽系中所有其他行星總和的兩倍半。木星是夜空中肉眼可見的最亮物體之一，自史前有記載以來就為古代文明所知。它以羅馬神朱庇特命名。[19] 從地球上看，木星可以亮到其反射光投下可見的陰影，[20] 平均而言，它是夜空中繼月亮和金星之後第三亮的自然物體。<br/> **用 2 個簡短的句子摘要這個** | 木星是距離太陽第五顆行星，是太陽系中最大的行星，也是夜空中最亮的物體之一。它以羅馬神朱庇特命名，是一顆氣態巨行星，質量是太陽系中所有其他行星總和的兩倍半。 |

主要內容區段可以用各種方式來驅動更有效的指令：

- **範例** – 與其明確地告訴模型該做什麼，不如提供所需輸出的範例，讓它推斷模式。
- **提示** – 在指令後面加上一個「提示」，引導完成，引導模型產生更相關的回應。
- **範本** – 可重複使用的提示「配方」，帶有預留位置（變數），可以用資料客製化以適用於特定使用案例。

讓我們來看看這些的實際應用。

### 使用範例

這種方法使用主要內容來「餵給模型」一些所需輸出的範例，讓它推斷出輸出的模式。根據提供的範例數量，我們有零樣本提示、單樣本提示、少樣本提示等。

提示現在由三個部分組成：

- 任務描述
- 一些所需輸出的範例
- 一個新範例的開頭（作為隱含的任務描述）

| 學習類型 | 提示（輸入） | 完成（輸出） |
| :--- | :--- | :--- |
| 零樣本 | 「太陽正在照耀」。翻譯成西班牙文 | 「El Sol está brillando」。 |
| 單樣本 | 「太陽正在照耀」=>「El Sol está brillando」。<br>「今天又冷又刮風」=> | 「Es un día frío y ventoso」。 |
| 少樣本 | 球員跑壘 => 棒球 <br/> 球員擊出愛司球 => 網球 <br/> 球員擊出六分球 => 板球 <br/> 球員灌籃 => | 籃球 |
| | | |

請注意，在零樣本提示中，我們必須提供明確的指令（「翻譯成西班牙文」），但在單樣本提示中，它是從範例中推斷出來的。少樣本範例顯示，增加更多範例有助於模型在沒有額外指令的情況下做出更準確的推斷。

### 提示線索

另一種使用主要內容的方法是提供「線索」而非範例。在這裡，我們透過「開頭」一個反映所需回應格式的片段來給模型一個正確方向的提示。然後模型「領會線索」並相應地繼續。

| 線索數量 | 提示（輸入） | 完成（輸出） |
| :--- | :--- | :--- |
| 0 | 木星是距離太陽第五顆行星，也是太陽系中最大的行星。它是一顆氣態巨行星，質量是太陽的千分之一，但卻是太陽系中所有其他行星總和的兩倍半。木星是夜空中肉眼可見的最亮物體之一，自史前有記載以來就為古代文明所知。 | **摘要這個** | 木星是我們太陽系中最大的行星，也是距離太陽第五顆行星。它是一顆氣態巨行星，質量是太陽的千分之一，但比所有其他行星的總和還要重。古代文明很早就知道木星，而且在夜空中很容易看到。 |
| 1 | 木星是距離太陽第五顆行星，也是太陽系中最大的行星。它是一顆氣態巨行星，質量是太陽的千分之一，但卻是太陽系中所有其他行星總和的兩倍半。木星是夜空中肉眼可見的最亮物體之一，自史前有記載以來就為古代文明所知。<br/>**摘要這個**<br/>我們學到的是木星 | 是距離太陽第五顆行星，也是太陽系中最大的行星。它是一顆氣態巨行星，質量是太陽的千分之一，但卻是太陽系中所有其他行星總和的兩倍半。肉眼很容易看到，自古以來就為人所知。 |
| 2 | 木星是距離太陽第五顆行星，也是太陽系中最大的行星。它是一顆氣態巨行星，質量是太陽的千分之一，但卻是太陽系中所有其他行星總和的兩倍半。木星是夜空中肉眼可見的最亮物體之一，自史前有記載以來就為古代文明所知。<br/>**摘要這個**<br/>我們學到的前 3 個事實： | 1. 木星是距離太陽第五顆行星，也是太陽系中最大的行星。<br/> 2. 它是一顆氣態巨行星，質量是太陽的千分之一...<br/> 3. 自古以來，木星就肉眼可見... |
| | | |

### 提示範本

提示範本是一個「預先定義的提示配方」，可以根據需要儲存和重複使用，以大規模地建立更一致的使用者體驗。最簡單的形式是，它只是一個提示範例的集合，就像 [OpenAI 的這個範例](https://platform.openai.com/examples?WT.mc_id=academic-105485-koreyst) 一樣，其中包含互動式提示元件（使用者和系統訊息）和 API 請求格式——以支援重複使用。

在更複雜的形式中，就像 [LangChain 的這個範例](https://python.langchain.com/docs/concepts/prompt_templates/?WT.mc_id=academic-105485-koreyst) 一樣，它包含「預留位置」，可以用來自各種來源（使用者輸入、系統上下文、外部資料等）的資料填寫，以動態產生提示。這讓我們可以建立一個可重複使用的提示庫，可以以程式設計方式大規模地提供一致的使用者體驗。

範本的真正價值在於建立和發布針對特定應用程式領域量身打造的「提示庫」——其中提示範本經過「優化」，以反映特定領域的上下文或範例，使回應對目標受眾更具相關性和準確性。[Prompts For Edu](https://github.com/microsoft/prompts-for-edu?WT.mc_id=academic-105485-koreyst) 儲存庫就是一個很好的例子，它為教育策劃了提示，重點關注課程計畫、課程設計、學生輔導等等。

## 輔助內容

如果我們將提示建構視為具有指令（任務）和目標（主要內容），那麼「次要內容」就是我們提供來「影響輸出」的額外上下文。這可能是調整參數、格式化指令、主題分類法等，有助於模型「量身打造」其回應，以更好地滿足使用者的目標或期望。

例如：給定一個包含課程目錄的詳細元資料（名稱、描述、等級、標籤、講師等）的課程目錄：

- 我們可以定義一個指令來「摘要 2023 年秋季的課程目錄」
- 我們可以使用主要內容來提供一些所需輸出的範例
- 我們可以使用次要內容來突顯感興趣的前 5 個「標籤」

現在，模型可以以範例所示的風格產生摘要——但如果一門課程有多個標籤，它可以優先考慮在次要內容中識別的 5 個標籤。

---

<!--
課程範本：
本單元應涵蓋核心概念 #1。
用範例和參考資料來強化概念。

概念 #3：
提示工程技術。
有哪些基本的提示工程技術？
用一些練習來說明它。
-->

## 提示最佳實務

現在我們了解了如何「建構」提示，我們可以開始思考如何遵循最佳實務來「設計」它們。這涉及兩個部分——擁有正確的「心態」和應用正確的「技術」。

### 提示工程心態

提示工程是一個反覆試驗的過程，因此請記住這三個廣泛的指導原則：

1. **領域理解很重要。** 回應的準確性和相關性取決於應用程式或使用者操作的「領域」。利用您的直覺和領域專業知識來相應地「客製化技術」。例如，在系統提示中定義「特定領域的個性」，或在使用者提示中使用「特定領域的範本」。提供反映領域上下文的次要內容，或使用「特定領域的提示和範例」來引導模型走向熟悉的使用模式。

2. **模型理解很重要。** 模型本質上是隨機的，但實作在訓練資料（預訓練知識）、能力（API 或 SDK）和內容重點（程式碼、影像、文字等）方面各不相同。了解您模型的優缺點，並利用這些知識來「排定任務的優先順序」或建立針對模型能力優化的「客製化範本」。

3. **迭代與驗證很重要。** 模型和提示工程技術發展迅速。作為領域專家，您可能對您的應用程式有特定的上下文或標準，而這些上下文或標準並不普遍適用。使用提示工程工具和技術來快速建立提示，然後利用您自己的直覺和專業知識來迭代和驗證結果。記錄您的見解並建立一個「知識庫」（例如，提示庫），其他人可以將其用作未來更快迭代的基準。

## 最佳實務

以下是 [OpenAI](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api?WT.mc_id=academic-105485-koreyst) 和 [Azure OpenAI](https://learn.microsoft.com/azure/ai-services/openai/concepts/prompt-engineering#best-practices?WT.mc_id=academic-105485-koreyst) 從業人員推薦的常見最佳實務。

| 內容 | 原因 |
| :--- | :--- |
| 評估最新的模型。 | 新的模型版本通常具有改進的功能和品質，但成本可能更高。在決定遷移之前，請測試它們的影響。 |
| 分隔指令和上下文 | 檢查您的模型/提供者是否支援「分隔符號」以清楚地分隔指令、主要和次要內容。這有助於模型更準確地為權杖分配重要性。 |
| 具體而清晰 | 提供有關所需上下文、結果、長度、格式、樣式等的詳細資訊。這可以提高回應的品質和一致性。在可重複使用的範本中擷取這些詳細資訊。 |
| 描述性，使用範例 | 模型通常對「展示和說明」的方法反應更好。從「零樣本」提示（僅指令）開始，然後透過新增所需輸出的範例來使用「少樣本」進行完善。在有幫助的地方使用類比。 |
| 使用提示來快速啟動完成 | 透過給予模型一些引導性的單字或片語，引導模型朝向期望的結果，模型可以將其用作回應的起點。 |
| 加倍努力 | 有時重複指令會有幫助。在主要內容之前和之後提供指令，同時使用指令和提示等。迭代並驗證最有效的方法。 |
| 順序很重要 | 由於新近性偏誤，資訊呈現的順序會影響輸出。嘗試不同的順序以找到最有效的方法。 |
| 給模型一個「退路」 | 提供一個「備用」回應，如果模型無法完成任務，可以使用該回應。這可以減少錯誤或捏造答案的機會。 |
| | |

與任何最佳實務一樣，請記住，「您的結果可能會有所不同」，具體取決於模型、任務和領域。將這些作為起點，並進行迭代以找到最適合您的方法。隨著新模型和工具的出現，不斷重新評估您的提示工程流程，重點關注可擴展性和回應品質。

<!--
課程範本：
如果適用，本單元應提供程式碼挑戰

挑戰：
連結到一個 Jupyter Notebook，其中只有指令中的程式碼註解（程式碼部分是空的）。

解決方案：
連結到該筆記本的副本，其中已填入提示並執行，顯示一個範例。
-->

## 作業

恭喜！您已完成本課！現在是時候用實際範例來應用其中一些概念和技術了。

對於此作業，我們將使用一個 Jupyter Notebook，其中包含您可以互動完成的練習。您也可以新增自己的 Markdown 和程式碼儲存格，以自行探索想法和技術。

### 若要開始，請 fork 儲存庫，然後

- （建議）啟動 GitHub Codespaces
- （或者）在本機複製儲存庫並與 Docker Desktop 搭配使用
- （或者）在您偏好的執行階段環境中開啟筆記本

### 接下來，設定您的環境變數

- 將儲存庫根目錄中的 `.env.copy` 檔案複製到 `.env`，並填入 `AZURE_OPENAI_API_KEY`、`AZURE_OPENAI_ENDPOINT` 和 `AZURE_OPENAI_DEPLOYMENT` 的值。然後返回 [學習沙箱部分](../../../04-prompt-engineering-fundamentals/04-prompt-engineering-fundamentals) 以了解如何繼續。

### 接下來，開啟 Jupyter Notebook

- 選取執行階段核心。如果使用選項 1 或 2，只需選取開發容器提供的預設 Python 3.10.x 核心即可。

您已準備好執行練習。請注意，這裡沒有「對或錯」的答案——只是透過反覆試驗來進行實驗，並建立對特定模型和應用程式領域有效的直覺。

「因此，本課中沒有程式碼解決方案部分。相反地，筆記本包含標題為「我的解決方案：」的 Markdown 儲存格，其中顯示一個範例輸出以供參考。」

 <!--
課程範本：
用摘要和自學資源來總結本節。
-->

## 知識測驗

下列何者是遵循合理最佳實務的良好提示？

1. 給我一張紅色汽車的圖片
2. 給我一張紅色汽車的圖片，品牌是 Volvo，型號是 XC90，停在懸崖邊，夕陽西下
3. 給我一張紅色汽車的圖片，品牌是 Volvo，型號是 XC90

A：2 是最好的提示，因為它提供了關於「什麼」的詳細資訊，並包含具體細節（不只是任何汽車，而是特定的品牌和型號），還描述了整體場景。3 是次佳的，因為它也包含很多描述。

## 🚀 挑戰

嘗試使用「提示」技巧搭配提示：完成句子「給我一張紅色汽車的圖片，品牌是 Volvo 和」。它會回應什麼，您會如何改進它？

## 做得好！繼續學習

想了解更多關於不同提示工程概念的資訊嗎？請造訪[持續學習頁面](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst)以取得更多關於此主題的優質資源。

前往第 5 課，我們將探討[進階提示技巧](../05-advanced-prompts/README.md?WT.mc_id=academic-105485-koreyst)！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。