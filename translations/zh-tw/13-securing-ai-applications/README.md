<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f3cac698e9eea47dd563633bd82daf8c",
  "translation_date": "2025-07-09T15:08:25+00:00",
  "source_file": "13-securing-ai-applications/README.md",
  "language_code": "zh-tw"
}
-->
# 保護您的生成式 AI 應用程式

[![保護您的生成式 AI 應用程式](../../../translated_images/13-lesson-banner.14103e36b4bbf17398b64ed2b0531f6f2c6549e7f7342f797c40bcae5a11862e.en.png)](https://aka.ms/gen-ai-lesson13-gh?WT.mc_id=academic-105485-koreyst)

## 簡介

本課將涵蓋：

- AI 系統中的安全性。
- AI 系統的常見風險和威脅。
- 保護 AI 系統的方法和考量因素。

## 學習目標

完成本課後，您將了解：

- AI 系統面臨的威脅和風險。
- 保護 AI 系統的常見方法和最佳實務。
- 安全性測試如何幫助防止意外結果並維護使用者信任。

## 在生成式 AI 的背景下，安全性意味著什麼？

隨著人工智慧 (AI) 和機器學習 (ML) 技術日益影響我們的生活，保護客戶資料和 AI 系統本身都至關重要。AI/ML 越來越多地用於支援高風險決策，在這些決策中，錯誤的決策可能會產生嚴重後果。

需要考慮的關鍵點：

- **AI/ML 的影響**：AI/ML 顯著影響日常生活，使其保護至關重要。
- **安全挑戰**：AI/ML 的影響需要集中精力保護基於 AI 的產品免受複雜攻擊，無論是來自惡意使用者還是有組織的團體。
- **策略問題**：科技產業必須主動應對策略挑戰，以確保長期客戶安全和資料安全。

此外，機器學習模型通常無法區分惡意輸入和無害異常。許多訓練資料來自未經策劃、未經審核的公共資料集，這些資料集對第三方貢獻開放。攻擊者不需要駭入資料集，他們只需貢獻即可。隨著時間的推移，如果資料格式保持一致，低信賴度的惡意資料可能會變成受信任的高信賴度資料。

這就是為什麼確保模型所依賴的資料儲存的完整性和保護至關重要。

## 了解 AI 的威脅和風險

在 AI 和相關系統中，資料中毒是目前最嚴重的安全威脅。資料中毒發生在有人故意更改訓練資料以導致 AI 犯錯時。由於缺乏標準化的偵測和緩解方法，以及我們對用於訓練的不可信或未經策劃的公共資料集的依賴，這種威脅更加嚴重。為了維護資料完整性並避免有缺陷的訓練，追蹤資料的來源和沿襲至關重要。否則，老話說「垃圾進，垃圾出」適用，導致模型效能受損。

資料中毒如何影響您的模型的範例：

1. **標籤翻轉**：在二元分類任務中，攻擊者翻轉一小部分訓練資料的標籤。例如，良性樣本被標記為惡意，導致模型學習不正確的關聯。
   **範例**：垃圾郵件過濾器由於被操縱的標籤而錯誤地將合法電子郵件標記為垃圾郵件。
2. **特徵中毒**：攻擊者巧妙地更改訓練資料中的特徵，以引入偏差或誤導模型。
   **範例**：向產品描述添加不相關的關鍵字以操縱推薦系統。
3. **資料注入**：惡意資料被注入訓練集以影響模型的行為。
   **範例**：引入虛假使用者評論以扭曲情感分析。
4. **後門攻擊**：攻擊者將隱藏模式（後門）插入訓練資料中。模型學習識別此模式，並在觸發時惡意行為。
   **範例**：一個經過後門影像訓練的人臉辨識系統錯誤地識別特定人員。

MITRE 公司建立了 [ATLAS (人工智慧系統的對抗性威脅情勢)](https://atlas.mitre.org/?WT.mc_id=academic-105485-koreyst)，這是一個關於攻擊者在真實世界 AI 攻擊中使用的戰術和技術的知識庫。

> AI 啟用系統中的漏洞數量不斷增加，因為 AI 的整合擴大了攻擊面，超越了傳統的網路攻擊。我們開發了 ATLAS，以提高對這些獨特且不斷演變的漏洞的認識，因為 AI 越來越廣泛地整合到各種系統中。ATLAS 模仿 MITRE ATT&CK® 框架，其戰術、技術和程序 (TTP) 補充了 ATT&CK 中的那些。

與 MITRE ATT&CK® 框架類似，ATLAS 在傳統網路安全中廣泛用於規劃進階威脅模擬，ATLAS 提供了一組可搜尋的 TTP，以更好地了解和準備防禦新興的 AI 攻擊。

此外，開放式 Web 應用程式安全專案 (OWASP) 建立了一個「[十大清單](https://llmtop10.com/?WT.mc_id=academic-105485-koreyst)」，列出了使用 LLM 的應用程式中最關鍵的漏洞。此清單突出了資料中毒等風險，以及其他風險，例如：

- **提示注入**：一種技術，攻擊者透過精心設計的輸入來操縱大型語言模型 (LLM)，使其行為超出其預期參數。
- **供應鏈漏洞**：LLM 使用的元件和軟體，例如 Python 模組或外部資料集，可能會受到損害，導致底層基礎設施中出現意外結果、偏差或漏洞。
- **過度依賴**：LLM 容易出錯且容易產生幻覺，產生不準確或不安全的輸出。在有記錄的案例中，使用者輕信這些輸出，導致現實世界中意想不到的傷害。

Microsoft Cloud Advocate Rod Trent 撰寫了一本免費電子書 [Must Learn AI Security](https://github.com/rod-trent/OpenAISecurity/tree/main/Must_Learn/Book_Version?WT.mc_id=academic-105485-koreyst)，深入探討了這些和其他新興的 AI 威脅，並提供了廣泛的解決方案指南。

## AI 系統和 LLM 的安全性測試

人工智慧 (AI) 正在改變許多領域和產業，提供新的機會和好處。然而，AI 也帶來了重大的挑戰和風險，包括資料隱私、偏見、缺乏可解釋性以及潛在的濫用。因此，確保 AI 系統安全且負責任至關重要——這意味著它們符合道德和法律標準，並且可以受到使用者和利害關係人的信任。

安全性測試涉及透過識別和利用漏洞來評估 AI 系統或 LLM 的安全性。這可以由開發人員、使用者或第三方稽核員完成，具體取決於測試的目的和範圍。AI 系統和 LLM 的常見安全性測試方法包括：

- **資料清理**：從訓練資料或 AI 輸入中移除或匿名化敏感或私人資訊。這有助於透過減少機密或個人資料的暴露來防止資料洩露和惡意操縱。
- **對抗性測試**：建立和應用對抗性範例到 AI 輸入或輸出，以評估對攻擊的穩健性。這有助於識別和緩解攻擊者可能利用的漏洞。
- **模型驗證**：檢查模型參數或架構的正確性和完整性。這有助於透過確保模型受到保護和驗證來偵測和防止模型竊取。
- **輸出驗證**：驗證 AI 輸出的品質和可靠性。這有助於透過確保輸出一致且準確來偵測和糾正惡意操縱。

OpenAI 作為 AI 系統的領導者，已建立一系列「安全評估」作為其紅隊網路計畫的一部分，旨在測試 AI 輸出以促進 AI 安全。

> 評估範圍從簡單的問答測試到複雜的模擬。以下是 OpenAI 開發的範例評估，用於從不同角度評估 AI 行為：

#### 說服

- [MakeMeSay](https://github.com/openai/evals/tree/main/evals/elsuite/make_me_say/readme.md?WT.mc_id=academic-105485-koreyst)：AI 系統能多好地欺騙另一個 AI 系統說出一個秘密單字？
- [MakeMePay](https://github.com/openai/evals/tree/main/evals/elsuite/make_me_pay/readme.md?WT.mc_id=academic-105485-koreyst)：AI 系統能多好地說服另一個 AI 系統捐款？
- [Ballot Proposal](https://github.com/openai/evals/tree/main/evals/elsuite/ballots/readme.md?WT.mc_id=academic-105485-koreyst)：AI 系統能多好地影響另一個 AI 系統對政治提案的支持？

#### 隱寫術（隱藏訊息）

- [隱寫術](https://github.com/openai/evals/tree/main/evals/elsuite/steganography/readme.md?WT.mc_id=academic-105485-koreyst)：AI 系統能多好地傳遞秘密訊息而不被另一個 AI 系統偵測到？
- [文字壓縮](https://github.com/openai/evals/tree/main/evals/elsuite/text_compression/readme.md?WT.mc_id=academic-105485-koreyst)：AI 系統能多好地壓縮和解壓縮訊息以隱藏秘密訊息？
- [謝林點](https://github.com/openai/evals/blob/main/evals/elsuite/schelling_point/README.md?WT.mc_id=academic-105485-koreyst)：AI 系統能在沒有直接通訊的情況下多好地與另一個 AI 系統協調？

### AI 安全

保護 AI 系統免受惡意攻擊、濫用或意外後果至關重要。這涉及透過以下方式確保 AI 系統的安全、可靠性和可信度：

- 保護用於訓練和操作 AI 模型的資料和演算法
- 防止未經授權的存取、操縱或破壞 AI 系統
- 偵測和緩解 AI 系統中的偏見、歧視或道德問題
- 確保 AI 決策和行動的問責制、透明度和可解釋性
- 使 AI 系統的目標和價值觀與人類和社會的目標和價值觀保持一致

AI 安全對於維護 AI 系統和資料的完整性、可用性和機密性至關重要。一些挑戰和機會包括：

- 機會：在網路安全策略中使用 AI，因為它可以幫助識別威脅並縮短回應時間。AI 可以自動化並增強對網路攻擊（如網路釣魚、惡意軟體或勒索軟體）的偵測和緩解。
- 挑戰：攻擊者也可以使用 AI 發動複雜的攻擊，例如產生虛假或誤導性內容、冒充使用者或利用 AI 系統漏洞。AI 開發人員有獨特的責任來設計對濫用具有穩健性和彈性的系統。

### 資料保護

LLM 可能對其使用的資料的隱私和安全構成風險。例如，LLM 可能會記住並洩露其訓練資料中的敏感資訊，例如個人姓名、地址、密碼或信用卡號碼。它們也可能被惡意行為者操縱或攻擊，這些行為者試圖利用漏洞或偏見。因此，了解這些風險並採取適當措施保護與 LLM 一起使用的資料非常重要。您可以採取的步驟包括：

- **限制與 LLM 共享的資料量和類型**：僅共享必要且與預期目的相關的資料，避免敏感、機密或個人資訊。使用者應透過移除或遮罩識別詳細資訊或使用安全通訊通道來匿名化或加密與 LLM 共享的資料。
- **驗證 LLM 產生的資料**：始終檢查 LLM 輸出的準確性和品質，以確保它們不包含不需要或不適當的資訊。
- **報告和警示資料外洩或事件**：警惕可疑或異常的 LLM 行為，例如產生不相關、不準確、冒犯性或有害的文字。這可能表示資料外洩或安全事件。

資料安全、治理和合規性對於在多雲端環境中利用資料和 AI 的組織至關重要。保護和治理所有資料是複雜且多方面的。您必須保護和管理多種雲端中的不同類型資料（結構化、非結構化和 AI 產生），同時遵守當前和未來的資料安全、治理和 AI 法規。最佳實務包括：

- 使用提供資料保護和隱私功能的雲端服務或平台。
- 採用資料品質和驗證工具來偵測錯誤、不一致或異常。
- 應用資料治理和道德框架，以確保負責任和透明的資料使用。

### 模擬真實世界威脅 - AI 紅隊

模擬真實世界威脅現在是建置彈性 AI 系統的標準做法。它涉及使用類似的工具、戰術和程序來識別系統風險並測試防禦者的回應。
> AI 紅隊的實踐已經發展出更廣泛的意義：它不僅涉及尋找安全漏洞，還包括測試其他系統故障，例如產生潛在有害內容。AI 系統帶來新的風險，而紅隊對於了解這些新穎的風險至關重要，例如提示注入和產生未經證實的內容。- [Microsoft AI 紅隊正在建置更安全的 AI 的未來](https://www.microsoft.com/security/blog/2023/08/07/microsoft-ai-red-team-building-future-of-safer-ai/?WT.mc_id=academic-105485-koreyst)
[![紅隊的指導和資源](../../../translated_images/13-AI-red-team.642ed54689d7e8a4d83bdf0635768c4fd8aa41ea539d8e3ffe17514aec4b4824.en.png)]()

以下是塑造 Microsoft AI 紅隊計畫的關鍵見解。

1. **AI 紅隊的廣泛範圍：**
   AI 紅隊現在涵蓋安全和負責任 AI (RAI) 結果。傳統上，紅隊專注於安全方面，將模型視為目標（例如，竊取底層模型）。然而，AI 系統引入了新的安全漏洞（例如，提示注入、中毒），需要特別注意。除了安全之外，AI 紅隊還檢查公平性問題（例如，刻板印象）和有害內容（例如，美化暴力）。及早識別這些問題有助於優先處理防禦工作。

2. **惡意和良性故障：**
   AI 紅隊考慮來自惡意和良性角度的故障。例如，在對新的 Bing 進行紅隊測試時，我們不僅探討惡意行為者如何利用系統，還探討普通使用者如何遇到有問題或有害的內容。與主要關注惡意行為者的傳統安全紅隊不同，AI 紅隊處理更廣泛的使用者和潛在故障。

3. **AI 系統的動態性質：**
   AI 應用程式不斷發展。在大型語言模型應用程式中，開發人員適應不斷變化的需求。持續的紅隊測試可確保對新興風險的持續警惕和適應。

AI 紅隊並非包羅萬象，應視為與其他控制措施（例如[基於角色的存取控制 (RBAC)](https://learn.microsoft.com/azure/ai-services/openai/how-to/role-based-access-control?WT.mc_id=academic-105485-koreyst)）和全面的資料管理解決方案相輔相成的補充方法。它旨在支援以部署安全且負責任的 AI 解決方案為重點的安全策略，這些解決方案尊重隱私和安全，同時旨在減少可能破壞使用者信任的偏見、有害內容和錯誤資訊。

以下是額外閱讀清單，可幫助您更好地了解紅隊如何識別和緩解 AI 系統中的風險：

- [規劃大型語言模型 (LLM) 及其應用程式的紅隊測試](https://learn.microsoft.com/azure/ai-services/openai/concepts/red-teaming?WT.mc_id=academic-105485-koreyst)
- [什麼是 OpenAI 紅隊網路？](https://openai.com/blog/red-teaming-network?WT.mc_id=academic-105485-koreyst)
- [AI 紅隊 - 建置更安全、更負責任的 AI 解決方案的關鍵實踐](https://rodtrent.substack.com/p/ai-red-teaming?WT.mc_id=academic-105485-koreyst)
- MITRE [ATLAS (人工智慧系統的對抗性威脅情勢)](https://atlas.mitre.org/?WT.mc_id=academic-105485-koreyst)，一個關於攻擊者在真實世界 AI 系統攻擊中使用的戰術和技術的知識庫。

## 知識測驗

維護資料完整性並防止濫用的好方法是什麼？

1. 對資料存取和資料管理有強大的基於角色的控制
2. 實施和稽核資料標籤以防止資料誤報或濫用
3. 確保您的 AI 基礎設施支援內容過濾

A:1，雖然這三者都是極好的建議，但確保您為使用者指派正確的資料存取權限是防止 LLM 使用的資料被操縱和誤報的關鍵。

## 🚀 挑戰

了解更多關於如何在 AI 時代[治理和保護敏感資訊](https://learn.microsoft.com/training/paths/purview-protect-govern-ai/?WT.mc_id=academic-105485-koreyst)的資訊。

## 做得好，繼續學習

完成本課後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 知識！

接下來，前往第 14 課，我們將探討[生成式 AI 應用程式生命週期](../14-the-generative-ai-application-lifecycle/README.md?WT.mc_id=academic-105485-koreyst)！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。