<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e2f686f2eb794941761252ac5e8e090b",
  "translation_date": "2025-07-09T08:06:44+00:00",
  "source_file": "02-exploring-and-comparing-different-llms/README.md",
  "language_code": "zh-tw"
}
-->
# 探索與比較不同的 LLM

[![探索與比較不同的 LLM](../../../translated_images/02-lesson-banner.ef94c84979f97f60f07e27d905e708cbcbdf78707120553ccab27d91c947805b.en.png)](https://aka.ms/gen-ai-lesson2-gh?WT.mc_id=academic-105485-koreyst)

> _點擊上方圖片觀看本課影片_

在上一課中，我們看到了生成式 AI 如何改變技術格局、大型語言模型 (LLM) 如何運作，以及像我們的新創公司這樣的企業如何將其應用於其使用案例並成長！在本章中，我們將比較和對比不同類型的大型語言模型 (LLM)，以了解其優缺點。

我們新創公司旅程的下一步是探索目前的 LLM 格局，並確定哪些模型最適合我們的使用案例。

## 簡介

本課將涵蓋：

- 現今可用的不同類型的 LLM。
- 如何在 Azure 中測試、迭代和比較不同模型以適用於您的使用案例。
- 如何部署 LLM。

## 學習目標

在本課結束時，您將能夠：

- 為您的使用案例選擇正確的模型。
- 了解如何測試、迭代和改善模型的效能。
- 了解企業如何部署模型。

## 了解不同類型的 LLM

LLM 可以根據其架構、訓練資料和預期用途以各種方式進行分類。了解這些差異將有助於我們的新創公司為情境選擇正確的模型，並知道如何測試、迭代和增強效能。

LLM 有許多類型，您的選擇取決於您的預期用途、資料、預算等等。

根據您是否要將模型用於文字、音訊、視訊、影像生成等，您可能會選擇不同類型的模型。

- **音訊和語音辨識**。Whisper 型模型在這裡是絕佳的選擇，因為它們是通用型的，專為語音辨識而設計。它們在多樣化的音訊上進行訓練，可以執行多語言語音辨識。在此處深入了解 [Whisper 型模型](https://platform.openai.com/docs/models/whisper?WT.mc_id=academic-105485-koreyst)。

- **影像生成**。對於影像生成，DALL-E 和 Midjourney 是兩個知名的選項。DALL-E 可透過 Azure OpenAI 取得。[在此處閱讀更多關於 DALL-E 的資訊](https://platform.openai.com/docs/models/dall-e?WT.mc_id=academic-105485-koreyst)，以及本課程的第 9 章。

- **文字生成**。大多數模型都是為文字生成而訓練的，您有從 GPT-3.5 到 GPT-4 的廣泛選擇。它們的價格不同，GPT-4 是最昂貴的。值得探索 [Azure OpenAI 遊樂場](https://oai.azure.com/portal/playground?WT.mc_id=academic-105485-koreyst) 以評估哪些模型在能力和成本方面最符合您的需求。

- **多模態**。如果您想處理多種類型的輸入和輸出資料，請考慮像 [帶有視覺的 gpt-4 turbo 或 gpt-4o](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#gpt-4-and-gpt-4-turbo-models?WT.mc_id=academic-105485-koreyst) 這樣的模型——這是 OpenAI 的最新版本——它們將自然語言處理與視覺理解相結合，從而能夠透過多模態介面進行互動。

選擇模型可以讓您具備基本能力，但這可能還不夠。通常，您有公司特定的資料需要納入 LLM。有幾種方法可以解決這個問題，我們將在接下來的章節中介紹。

### 基礎模型與 LLM

「基礎模型」一詞由 [史丹佛大學研究人員創造](https://arxiv.org/abs/2108.07258?WT.mc_id=academic-105485-koreyst)，並定義為符合特定標準的 AI 模型，例如：

- **它們是使用無監督或自監督學習進行訓練的**，這意味著它們從未標記的多模態資料中學習，並且在訓練期間不需要人工註釋或標記。
- **它們是非常大的模型**，基於在數十億個參數上訓練的深度神經網路。
- **它們通常旨在作為其他模型的「基礎」**，這意味著它們可以作為透過微調建置其他模型的起點。

![基礎模型與 LLM](../../../translated_images/FoundationModel.e4859dbb7a825c94b284f17eae1c186aabc21d4d8644331f5b007d809cf8d0f2.en.png)

圖片來源：[基礎模型與大型語言模型基本指南 | Babar M Bhatti | Medium](https://thebabar.medium.com/essential-guide-to-foundation-models-and-large-language-models-27dab58f7404)

為了釐清這個區別，讓我們以 ChatGPT 為例。ChatGPT 的第一個版本是建立在一個名為 GPT-3.5 的基礎模型之上。OpenAI 使用特定於聊天室的資料來微調 GPT-3.5，從而建立了一個專門用於聊天機器人等對話情境的版本。

![基礎模型](../../../translated_images/Multimodal.2c389c6439e0fc51b0b7b226d95d7d900d372ae66902d71b8ce5ec4951b8efbe.en.png)

圖片來源：[2108.07258.pdf (arxiv.org)](https://arxiv.org/pdf/2108.07258.pdf?WT.mc_id=academic-105485-koreyst)

### 開源模型與專有模型

另一種對 LLM 進行分類的方法是它們是開源的還是專有的。

開源模型是公開可用的，任何人都可以使用。它們通常由創建它們的公司或研究社群發布。這些模型可以被檢查、修改和客製化，以適用於各種 LLM 使用案例。然而，它們並不總是針對生產進行優化，並且可能不如專有模型表現得好。開源模型的資金可能有限，因此它們可能無法長期維護或更新最新的研究成果。流行的開源模型包括 [Alpaca](https://crfm.stanford.edu/2023/03/13/alpaca.html?WT.mc_id=academic-105485-koreyst)、[Bloom](https://huggingface.co/bigscience/bloom) 和 [LLaMA](https://llama.meta.com)。

專有模型由公司擁有，不公開。這些模型通常針對生產用途進行了優化，但無法針對不同的使用案例進行檢查、修改或客製化。它們通常不是免費的，可能需要訂閱或付費。使用者也無法控制用於訓練模型的資料，因此他們必須信任模型所有者以確保資料隱私和負責任的 AI 使用。流行的專有模型範例包括 [OpenAI 模型](https://platform.openai.com/docs/models/overview?WT.mc_id=academic-105485-koreyst)、[Google Bard](https://sapling.ai/llm/bard?WT.mc_id=academic-105485-koreyst) 和 [Claude 2](https://www.anthropic.com/index/claude-2?WT.mc_id=academic-105485-koreyst)。

### 嵌入與影像生成與文字與程式碼生成

LLM 也可以根據其產生的輸出類型進行分類。

嵌入是將文字轉換為稱為嵌入的數值向量的模型，這些向量以數值方式表示輸入文字。嵌入有助於機器理解單字或句子之間的關係，並可用作其他模型的輸入，例如在處理數值資料時表現更好的分類器或叢集演算法。嵌入模型通常用於遷移學習，其中模型在具有豐富資料的代理任務上進行訓練，並且學習到的嵌入會重複用於其他下游任務。一個例子是 [OpenAI 嵌入](https://platform.openai.com/docs/models/embeddings?WT.mc_id=academic-105485-koreyst)。

![嵌入](../../../translated_images/Embedding.c3708fe988ccf76073d348483dbb7569f622211104f073e22e43106075c04800.en.png)

影像生成模型會建立影像。它們用於影像編輯、合成和翻譯。這些模型是在大型影像資料集（如 [LAION-5B](https://laion.ai/blog/laion-5b/?WT.mc_id=academic-105485-koreyst)）上訓練的，可以使用修補、超解析度和著色等技術生成新影像或編輯現有影像。範例包括 [DALL-E-3](https://openai.com/dall-e-3?WT.mc_id=academic-105485-koreyst) 和 [Stable Diffusion 模型](https://github.com/Stability-AI/StableDiffusion?WT.mc_id=academic-105485-koreyst)。

![影像生成](../../../translated_images/Image.349c080266a763fd255b840a921cd8fc526ed78dc58708fa569ff1873d302345.en.png)

文字和程式碼生成模型會產生文字或程式碼。它們用於摘要、翻譯和問答等任務。文字生成模型是在大型文字資料集（例如 [BookCorpus](https://www.cv-foundation.org/openaccess/content_iccv_2015/html/Zhu_Aligning_Books_and_ICCV_2015_paper.html?WT.mc_id=academic-105485-koreyst)）上訓練的，可以生成新文字或回答問題。程式碼生成模型（例如 [CodeParrot](https://huggingface.co/codeparrot?WT.mc_id=academic-105485-koreyst)）是在大型程式碼資料集（例如 GitHub）上訓練的，可以生成新程式碼或修復錯誤。

![文字和程式碼生成](../../../translated_images/Text.a8c0cf139e5cc2a0cd3edaba8d675103774e6ddcb3c9fc5a98bb17c9a450e31d.en.png)

### 編碼器-解碼器與僅解碼器

為了說明不同的 LLM 架構，讓我們用一個比喻。

想像一下，您的經理要求您為學生製作一份測驗。您有兩位同事：一位負責建立內容，另一位負責審核。

內容建立者就像一個僅解碼器模型。他們查看主題和您已經寫好的內容，然後撰寫課程內容。他們擅長產生引人入勝且資訊豐富的文字，但不太擅長理解主題或學習目標。解碼器模型的範例包括 GPT 系列，例如 GPT-3。

審核員就像一個僅編碼器模型。他們檢查已撰寫的課程和答案，了解關係和上下文，但不太擅長產生內容。僅編碼器模型的範例是 BERT。

現在想像一下，有人既能建立又能審核測驗——這就是一個編碼器-解碼器模型。範例包括 BART 和 T5。

### 服務與模型

讓我們來討論服務和模型之間的差異。服務是雲端服務提供者提供的產品，通常結合了模型、資料和其他元件。模型是服務的核心部分，通常是像 LLM 這樣的基礎模型。

服務通常針對生產進行了優化，並且比模型更容易使用，通常是透過圖形介面。然而，服務並非總是免費的，可能需要訂閱或付費，這涵蓋了提供者的基礎設施、優化成本並允許輕鬆擴展。一個例子是 [Azure OpenAI 服務](https://learn.microsoft.com/azure/ai-services/openai/overview?WT.mc_id=academic-105485-koreyst)，它提供按需付費的定價，根據使用量向使用者收費。Azure OpenAI 服務還在模型之上提供企業級安全性和負責任的 AI 框架。

模型只是具有參數和權重的神經網路。公司可以在本地運行它們，但需要投資硬體、建立基礎設施以進行擴展，並取得授權或使用開源模型。例如，LLaMA 可供使用，但需要計算資源才能運行。

## 如何在 Azure 上測試和迭代不同模型以了解效能

在探索了目前的 LLM 格局並為其情境確定了有前途的候選模型之後，我們團隊的下一步是在其資料和工作負載上測試這些模型。這是一個涉及實驗和測量的迭代過程。
我們在前面章節中提到的大多數模型（OpenAI 模型、像 Llama2 這樣的開源模型，以及 Hugging Face transformer）都可以在 [Azure AI Studio](https://ai.azure.com/?WT.mc_id=academic-105485-koreyst) 的 [模型目錄](https://learn.microsoft.com/azure/ai-studio/how-to/model-catalog-overview?WT.mc_id=academic-105485-koreyst) 中找到。

[Azure AI Studio](https://learn.microsoft.com/azure/ai-studio/what-is-ai-studio?WT.mc_id=academic-105485-koreyst) 是一個雲端平台，專為開發人員建置生成式 AI 應用程式和管理整個開發生命週期而設計——從實驗到評估——透過將所有 Azure AI 服務整合到一個具有使用者友好 GUI 的單一中樞。Azure AI Studio 中的模型目錄允許使用者：

- 在目錄中尋找感興趣的基礎模型——無論是專有的還是開源的——透過按任務、授權或名稱進行篩選。為了提高可搜尋性，模型被組織成集合，例如 Azure OpenAI 集合、Hugging Face 集合等等。

![模型目錄](../../../translated_images/AzureAIStudioModelCatalog.3cf8a499aa8ba0314f2c73d4048b3225d324165f547525f5b7cfa5f6c9c68941.en.png)

- 檢閱模型卡，其中包含預期用途和訓練資料的詳細說明、程式碼範例，以及來自內部評估庫的評估結果。

![模型卡](../../../translated_images/ModelCard.598051692c6e400d681a713ba7717e8b6e5e65f08d12131556fcec0f1789459b.en.png)

- 透過 [模型基準](https://learn.microsoft.com/azure/ai-studio/how-to/model-benchmarks?WT.mc_id=academic-105485-koreyst) 窗格，比較業界可用的模型和資料集的基準，以確定哪一個最適合業務情境。

![模型基準](../../../translated_images/ModelBenchmarks.254cb20fbd06c03a4ca53994585c5ea4300a88bcec8eff0450f2866ee2ac5ff3.en.png)

- 在自訂訓練資料上微調模型，以提高特定工作負載的效能，並利用 Azure AI Studio 的實驗和追蹤功能。

![模型微調](../../../translated_images/FineTuning.aac48f07142e36fddc6571b1f43ea2e003325c9c6d8e3fc9d8834b771e308dbf.en.png)

- 將原始預訓練模型或微調版本部署到遠端即時推論受控運算或無伺服器 API 端點——[按需付費](https://learn.microsoft.com/azure/ai-studio/how-to/model-catalog-overview#model-deployment-managed-compute-and-serverless-api-pay-as-you-go?WT.mc_id=academic-105485-koreyst)——以使應用程式能夠使用它。

![模型部署](../../../translated_images/ModelDeploy.890da48cbd0bccdb4abfc9257f3d884831e5d41b723e7d1ceeac9d60c3c4f984.en.png)


> [!NOTE]
> 並非目錄中的所有模型目前都可用於微調和/或按需付費部署。請查看模型卡以取得有關模型功能和限制的詳細資訊。

## 改善 LLM 結果

我們的新創團隊已經探索了各種類型的 LLM 和一個雲端平台 (Azure Machine Learning)，讓我們能夠比較不同的模型、在測試資料上評估它們、改善效能，並將它們部署在推論端點上。

但是，您應該何時考慮微調模型，而不是使用預訓練模型？還有其他方法可以改善模型在特定任務上的效能嗎？

企業可以使用幾種策略來從 LLM 中獲得所需的結果。在生產中部署 LLM 時，您可以選擇不同類型的模型，其訓練程度各不相同，每種模型的複雜性、成本和品質也不同。以下是一些方法：

- **帶有上下文的提示工程**。這個想法是在您的提示中提供足夠的上下文，以確保您獲得想要的響應。

- **檢索增強生成 (RAG)**。您的資料可能儲存在資料庫或 Web 端點中。若要在提示時包含此資料或其子集，您可以擷取相關資訊並將其新增至使用者的提示中。

- **微調模型**。在這裡，您可以在自己的資料上進一步訓練模型，使其更精確、更能滿足您的需求，儘管這可能成本高昂。

![LLM 部署](../../../translated_images/Deploy.18b2d27412ec8c02871386cbe91097c7f2190a8c6e2be88f66392b411609a48c.en.png)

圖片來源：[企業部署 LLM 的四種方式 | Fiddler AI 部落格](https://www.fiddler.ai/blog/four-ways-that-enterprises-deploy-llms?WT.mc_id=academic-105485-koreyst)

### 帶有上下文的提示工程

預訓練的 LLM 在一般自然語言任務上表現非常出色，即使只給予一個簡短的提示，例如一個要完成的句子或一個問題——這被稱為「零樣本」學習。

然而，使用者越能用詳細的請求和範例來建構他們的查詢——也就是上下文——答案就會越準確，也越符合使用者的期望。在這種情況下，如果提示只包含一個範例，就稱為「單樣本」學習；如果包含多個範例，就稱為「少樣本學習」。帶有上下文的提示工程是開始的最具成本效益的方式。

### 檢索增強生成 (RAG)

LLM 僅限於使用其訓練資料來產生答案。這意味著它們不知道訓練後發生的事件，也無法存取私人資訊（例如公司資料）。

RAG 透過以文件區塊的形式擴增提示與外部資料來克服這個問題，同時遵守提示長度限制。這由向量資料庫工具（例如 [Azure 向量搜尋](https://learn.microsoft.com/azure/search/vector-search-overview?WT.mc_id=academic-105485-koreyst)）支援，這些工具會從各種預定義的資料來源中擷取相關區塊，並將其新增至提示上下文中。

當企業缺乏足夠的資料、時間或資源來微調 LLM，但仍希望提高特定任務的效能並降低幻覺（即捏造或有害內容）的風險時，此技術特別有用。

### 微調模型

微調使用遷移學習來使模型適應特定的下游任務或問題。與少樣本學習和 RAG 不同，它會產生一個具有更新權重和偏差的新模型。它需要一組訓練範例，其中包含輸入（提示）及其對應的輸出（完成）。

如果出現以下情況，則首選此方法：

- **使用微調模型**。企業希望使用微調、功能較弱的模型（如嵌入模型）而不是高效能模型，從而獲得更具成本效益和更快的解決方案。

- **考慮延遲**。延遲對於使用案例至關重要，因此由於提示長度限制，非常長的提示或許多範例是不可行的。

- **保持最新**。企業擁有大量高品質的資料和真實標籤，以及隨著時間的推移保持此資料最新的資源。

### 訓練模型

從頭開始訓練 LLM 是迄今為止最困難、最複雜的方法，需要大量的資料、技術熟練的人員和大量的計算能力。只有當企業具有特定領域的使用案例和大量的以領域為中心的資料時，才應考慮此選項。

## 知識測驗

改善 LLM 完成結果的好方法是什麼？

1. 帶有上下文的提示工程
2. RAG
3. 微調模型

A：3. 如果您有時間、資源和高品質的資料，微調是保持最新狀態的最佳選擇。但是，如果您想改善結果但時間有限，則值得先考慮 RAG。

## 🚀 挑戰

深入了解如何為您的企業[使用 RAG](https://learn.microsoft.com/azure/search/retrieval-augmented-generation-overview?WT.mc_id=academic-105485-koreyst)。

## 做得好，繼續學習

完成本課程後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 知識！

前往第 3 課，我們將探討如何[負責任地建置生成式 AI](../03-using-generative-ai-responsibly/README.md?WT.mc_id=academic-105485-koreyst)！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。