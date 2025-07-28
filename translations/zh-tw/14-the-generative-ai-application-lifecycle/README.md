<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "27a5347a5022d5ef0a72ab029b03526a",
  "translation_date": "2025-07-09T15:46:09+00:00",
  "source_file": "14-the-generative-ai-application-lifecycle/README.md",
  "language_code": "zh-tw"
}
-->
[![整合函式呼叫](../../../translated_images/14-lesson-banner.066d74a31727ac121eeac06376a068a397d8e335281e63ce94130d11f516e46b.en.png)](https://aka.ms/gen-ai-lesson14-gh?WT.mc_id=academic-105485-koreyst)

# 生成式 AI 應用程式生命週期

所有 AI 應用程式的一個關鍵問題是其 AI 功能的相關性如何保持，因為 AI 是一個快速發展的領域。為了讓您的應用程式保持相關性、可靠性和穩健性，您需要持續監控、評估和改進它。這就是生成式 AI 生命週期發揮作用的地方。

生成式 AI 生命週期是一個框架，可引導您完成開發、部署和維護生成式 AI 應用程式的各個階段。它幫助您定義目標、衡量效能、識別挑戰並實施解決方案。它還確保您的應用程式符合您領域和利害關係人的道德和法律標準。透過遵循此生命週期，您可以確保您的應用程式持續提供價值並滿足使用者期望。

## 簡介

在本章中，您將：

- 了解從 MLOps 到 LLMOps 的典範轉移
- 了解 LLM 生命週期
- 探索生命週期工具
- 深入了解生命週期指標和評估

## 了解從 MLOps 到 LLMOps 的典範轉移

LLM 是 AI 工具包中的新工具，為應用程式中的分析和生成任務提供了強大的功能。然而，這種力量改變了我們處理 AI 和傳統機器學習工作流程的方式。

因此，我們需要一個新的典範來動態地適應這個工具，並提供正確的激勵。我們可以將舊的 AI 應用程式歸類為「ML 應用程式」，新的應用程式歸類為「生成式 AI 應用程式」或簡稱「AI 應用程式」，以反映當時主流的技術和技術。這種轉變從幾個方面改變了我們的觀點——請參閱下面的比較。

![LLMOps 與 MLOps 比較](../../../translated_images/01-llmops-shift.29bc933cb3bb0080a562e1655c0c719b71a72c3be6252d5c564b7f598987e602.en.png)

請注意，在 LLMOps 中，重點更多地轉向應用程式開發人員，強調整合、使用「模型即服務」，並考慮以下指標：

- 品質：回應品質
- 危害：負責任的 AI
- 誠實：回應的基礎性（是否有意義？是否正確？）
- 成本：解決方案預算
- 延遲：每個權杖回應的平均時間

## LLM 生命週期

若要了解生命週期及其差異，請查看下面的資訊圖表。

![LLMOps 資訊圖表](../../../translated_images/02-llmops.70a942ead05a7645db740f68727d90160cb438ab71f0fb20548bc7fe5cad83ff.en.png)

如您所見，這與傳統的 MLOps 生命週期不同。LLM 引入了新的要求，例如提示、各種提高品質的技術（微調、RAG、元提示）、圍繞負責任 AI 的新責任，以及新的評估指標（品質、危害、誠實、成本和延遲）。

例如，考慮我們如何構思：使用提示工程來實驗不同的 LLM，以探索可能性並測試我們的假設是否成立。

請記住，這個過程並非線性，而是由一個總體循環中整合的、迭代的循環組成。

我們如何探索這些步驟？讓我們深入了解建置生命週期的細節。

![LLMOps 工作流程](../../../translated_images/03-llm-stage-flows.3a1e1c401235a6cfa886ed6ba04aa52a096a545e1bc44fa54d7d5983a7201892.en.png)

這可能看起來很複雜，所以讓我們首先關注三個主要步驟：

1. 構思/探索：基於業務需求的探索。原型設計、建立 [PromptFlow](https://microsoft.github.io/promptflow/index.html?WT.mc_id=academic-105485-koreyst)，並測試它是否足以驗證我們的假設。
2. 建置/增強：實作。在這裡，我們評估更大的資料集並應用微調和 RAG 等技術來檢查我們解決方案的穩健性。如果它不符合預期，重新實作、新增步驟或重組資料可能會有所幫助。經過測試和擴展後，如果指標看起來不錯，就可以進入下一步了。
3. 操作化：整合。新增監控和警報系統、部署，並將應用程式整合到您的環境中。

涵蓋所有這些的是管理週期，重點關注安全性、合規性和治理。

恭喜，您的 AI 應用程式現在已準備就緒並可運作！如需實際體驗，請查看 [Contoso 聊天示範。](https://nitya.github.io/contoso-chat/?WT.mc_id=academic-105485-koreys)

我們可以使用哪些工具？

## 生命週期工具

對於工具，Microsoft 提供了 [Azure AI 平台](https://azure.microsoft.com/solutions/ai/?WT.mc_id=academic-105485-koreyst) 和 [PromptFlow](https://microsoft.github.io/promptflow/index.html?WT.mc_id=academic-105485-koreyst)，這使得實施和管理您的生命週期變得簡單。

[Azure AI 平台](https://azure.microsoft.com/solutions/ai/?WT.mc_id=academic-105485-koreyst) 包含 [AI Studio](https://ai.azure.com/?WT.mc_id=academic-105485-koreyst)，這是一個網路入口網站，您可以在其中探索模型、範例和工具。它讓您可以管理資源、開發 UI 流程，並使用 SDK/CLI 選項進行程式碼優先開發。

![Azure AI 的可能性](../../../translated_images/04-azure-ai-platform.80203baf03a12fa8b166e194928f057074843d1955177baf0f5b53d50d7b6153.en.png)

Azure AI 提供多種資源來管理您的操作、服務、專案、向量搜尋和資料庫需求。

![LLMOps 與 Azure AI](../../../translated_images/05-llm-azure-ai-prompt.a5ce85cdbb494bdf95420668e3464aae70d8b22275a744254e941dd5e73ae0d2.en.png)

使用 PromptFlow 從概念驗證 (POC) 建置到大規模應用程式：

- 使用視覺化和功能工具從 VS Code 設計和建置應用程式
- 輕鬆測試和微調您的應用程式以獲得高品質 AI
- 使用 Azure AI Studio 在雲端整合和迭代，然後推送和部署以實現快速整合

![LLMOps 與 PromptFlow](../../../translated_images/06-llm-promptflow.a183eba07a3a7fdf4aa74db92a318b8cbbf4a608671f6b166216358d3203d8d4.en.png)

## 太棒了！繼續學習！

太棒了！現在透過 [Contoso 聊天應用程式](https://nitya.github.io/contoso-chat/?WT.mc_id=academic-105485-koreyst) 了解如何使用這些概念來建構應用程式，該應用程式展示了 Cloud Advocacy 如何在示範中融入這些想法。如需更多內容，請查看我們的 [Ignite 分組討論會！](https://www.youtube.com/watch?v=DdOylyrTOWg)

接下來，繼續學習第 15 課，了解[檢索增強生成和向量資料庫](../15-rag-and-vector-databases/README.md?WT.mc_id=academic-105485-koreyst)如何影響生成式 AI 並幫助建立更具吸引力的應用程式！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。