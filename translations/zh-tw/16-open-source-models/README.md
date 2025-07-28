<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0bba96e53ab841d99db731892a51fab8",
  "translation_date": "2025-07-09T17:02:33+00:00",
  "source_file": "16-open-source-models/README.md",
  "language_code": "zh-tw"
}
-->
[![開源模型](../../../translated_images/16-lesson-banner.6b56555e8404fda1716382db4832cecbe616ccd764de381f0af6cfd694d05f74.en.png)](https://aka.ms/gen-ai-lesson16-gh?WT.mc_id=academic-105485-koreyst)

## 簡介

開源 LLM 的世界令人興奮且不斷發展。本課旨在深入探討開源模型。如果您想了解專有模型與開源模型的比較，請查看[「探索和比較不同的 LLM」課程](../02-exploring-and-comparing-different-llms/README.md?WT.mc_id=academic-105485-koreyst)。本課還將觸及微調，但更詳細的解釋請參閱[「微調 LLM」課程](../18-fine-tuning/README.md?WT.mc_id=academic-105485-koreyst)。

## 學習目標

- 了解開源模型
- 學習使用開源模型的好處
- 探索 Hugging Face 和 Azure AI Studio 上可用的開源模型

## 什麼是開源模型？

開源軟體一直是許多領域技術成長的關鍵。開放原始碼促進會 (OSI) 定義了 [10 項軟體標準](https://web.archive.org/web/20241126001143/https://opensource.org/osd?WT.mc_id=academic-105485-koreyst)，以被視為開源。原始碼必須在 OSI 批准的授權下公開共享。

雖然開發 LLM 與軟體開發有相似之處，但過程並不完全相同。這在社群中引發了關於開源在 LLM 背景下意味著什麼的許多爭論。對於一個模型來說，要符合傳統的開源定義，以下內容應該公開可用：

- 用於訓練模型的資料集。
- 訓練後的完整模型權重。
- 評估程式碼。
- 微調程式碼。
- 完整模型權重和訓練指標。

目前，只有少數模型符合這些標準。一個例子是 [Allen Institute for Artificial Intelligence (AllenAI) 建立的 OLMo 模型](https://huggingface.co/allenai/OLMo-7B?WT.mc_id=academic-105485-koreyst)。

在本課中，我們將這些稱為「開放模型」，因為在撰寫本文時，它們可能不完全符合上述標準。

## 開放模型的好處

**高度可客製化** – 因為開放模型附帶詳細的訓練資訊，研究人員和開發人員可以修改模型的內部結構。這允許建立高度專業化的模型，針對特定任務或領域進行微調，例如程式碼生成、數學運算或生物學。

**成本** – 使用和部署這些模型的每個權杖成本通常低於專有模型。在建置生成式 AI 應用程式時，考慮您的特定使用案例的效能與價格之間的關係非常重要。

![模型成本](../../../translated_images/model-price.3f5a3e4d32ae00b465325159e1f4ebe7b5861e95117518c6bfc37fe842950687.en.png)  
來源：Artificial Analysis

**彈性** – 開放模型讓您可以自由使用不同的模型或組合它們。例如，[HuggingChat Assistants](https://huggingface.co/chat?WT.mc_id=academic-105485-koreyst) 讓使用者可以直接在介面中選擇模型：

![選擇模型](../../../translated_images/choose-model.f095d15bbac922141591fd4fac586dc8d25e69b42abf305d441b84c238e293f2.en.png)

## 探索不同的開放模型

### Llama 2

[LLama2](https://huggingface.co/meta-llama?WT.mc_id=academic-105485-koreyst) 由 Meta 開發，是一個針對聊天應用程式優化的開放模型。這歸功於其微調方法，其中包括大量的對話和人類回饋。這種方法有助於模型產生更符合人類期望的回應，從而改善使用者體驗。

Llama 的一些微調版本包括專門用於日語的 [Japanese Llama](https://huggingface.co/elyza/ELYZA-japanese-Llama-2-7b?WT.mc_id=academic-105485-koreyst)，以及基礎模型的增強版本 [Llama Pro](https://huggingface.co/TencentARC/LLaMA-Pro-8B?WT.mc_id=academic-105485-koreyst)。

### Mistral

[Mistral](https://huggingface.co/mistralai?WT.mc_id=academic-105485-koreyst) 是一個專注於高效能和效率的開放模型。它採用了專家混合方法，將一組專業的專家模型組合成一個系統。根據輸入，會選擇特定的模型，透過僅處理它們專門處理的輸入來提高計算效率。

Mistral 的微調版本包括專注於醫療領域的 [BioMistral](https://huggingface.co/BioMistral/BioMistral-7B?text=Mon+nom+est+Thomas+et+mon+principal?WT.mc_id=academic-105485-koreyst)，以及處理數學計算的 [OpenMath Mistral](https://huggingface.co/nvidia/OpenMath-Mistral-7B-v0.1-hf?WT.mc_id=academic-105485-koreyst)。

### Falcon

[Falcon](https://huggingface.co/tiiuae?WT.mc_id=academic-105485-koreyst) 是由技術創新研究所 (TII) 開發的 LLM。Falcon-40B 經過 400 億個參數的訓練，並已證明其效能優於 GPT-3，同時所需的計算量更少。這是由於它使用了 FlashAttention 演算法和多查詢注意力，這減少了推論期間的記憶體需求。由於推論速度更快，Falcon-40B 非常適合聊天應用程式。

Falcon 的微調版本包括 [OpenAssistant](https://huggingface.co/OpenAssistant/falcon-40b-sft-top1-560?WT.mc_id=academic-105485-koreyst)，一個基於開放模型建置的助理，以及 [GPT4ALL](https://huggingface.co/nomic-ai/gpt4all-falcon?WT.mc_id=academic-105485-koreyst)，它提供了比基礎模型更好的效能。

## 如何選擇

對於選擇開放模型，沒有一體適用的答案。一個好的起點是使用 Azure AI Studio 的按任務篩選功能，查看模型已針對哪些任務進行了訓練。Hugging Face 還維護一個 LLM 排行榜，顯示基於各種指標的表現最佳模型。

對於比較不同類型的 LLM，[Artificial Analysis](https://artificialanalysis.ai/?WT.mc_id=academic-105485-koreyst) 是另一個極佳的資源：

![模型品質](../../../translated_images/model-quality.aaae1c22e00f7ee1cd9dc186c611ac6ca6627eabd19e5364dce9e216d25ae8a5.en.png)  
來源：Artificial Analysis

如果您正在處理特定的使用案例，搜尋專注於該領域的微調模型可能會很有效。嘗試多個開放模型，看看它們如何根據您和您的使用者的需求執行，也是一個好方法。

## 後續步驟

開放模型最棒的部分是您可以快速開始使用它們。請查看 [Azure AI Studio 模型目錄](https://ai.azure.com?WT.mc_id=academic-105485-koreyst)，其中包含我們在此處討論的模型專用 Hugging Face 集合。

## 學習永不止步，繼續旅程

完成本課後，請探索我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 技能！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。