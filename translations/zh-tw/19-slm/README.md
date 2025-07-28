<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "124ad36cfe96f74038811b6e2bb93e9d",
  "translation_date": "2025-07-09T18:11:30+00:00",
  "source_file": "19-slm/README.md",
  "language_code": "zh-tw"
}
-->
# 生成式 AI 初學者小型語言模型簡介
生成式 AI 是一個令人興奮的人工智慧領域，專注於建置可以創造新內容的系統。這些內容可以包括文字、影像、音樂，甚至整個虛擬世界。生成式 AI 最令人興奮的用途之一是在語言模型中。

## 什麼是小型語言模型？

小型語言模型 (SLM) 是大型語言模型 (LLM) 的縮小版，使用許多相同的架構原則和技術，但計算足跡小得多。

SLM 是一種旨在產生類似人類文字的語言模型。與 GPT-4 等較大型模型不同，SLM 更緊湊且效率更高，使其非常適合計算資源有限的情況，例如行動裝置或邊緣運算平台。儘管它們的尺寸較小，但它們仍然可以處理各種任務。通常，SLM 是透過壓縮或提煉 LLM 來建立的，旨在保留原始模型的大部分功能和語言技能。這種較小的尺寸降低了複雜性，使 SLM 在記憶體和計算方面更有效率。即使有這些優化，SLM 仍然可以執行許多自然語言處理 (NLP) 任務：

- 文字生成：產生連貫且與上下文相關的句子或段落。
- 文字完成：根據提示預測並完成句子。
- 翻譯：將文字從一種語言轉換為另一種語言。
- 摘要：將長文本濃縮成更短、更容易理解的摘要。

儘管與較大型模型相比，在效能或理解深度方面存在一些權衡。

## 小型語言模型如何運作？
SLM 透過大量文字資料進行訓練。在訓練期間，它們學習語言模式和結構，使其能夠產生語法正確且符合上下文的文字。訓練過程包括：

- 資料收集：從各種來源收集大量文字資料集。
- 預處理：清理和組織資料以進行訓練。
- 訓練：使用機器學習演算法教導模型如何理解和產生文字。
- 微調：調整模型以提高特定任務的效能。

SLM 的開發是為了滿足在資源有限的環境中（例如行動裝置或邊緣運算平台）執行模型的日益增長的需求，在這些環境中，全尺寸的 LLM 通常要求過高。透過專注於效率，SLM 在效能和可存取性之間取得了平衡，從而實現了在不同領域的更廣泛使用。

![slm](../../../translated_images/slm.4058842744d0444a021548a3e8253efd20e93a6ef59ec1525ded361bfc9e6c22.en.png)

## 學習目標

在本課中，我們旨在介紹 SLM 的概念，並將其與 Microsoft Phi-3 結合，以探索文字內容、視覺和 MoE 中的各種情境。

在本課結束時，您應該能夠回答：

- 什麼是 SLM？
- SLM 與 LLM 有何不同？
- 什麼是 Microsoft Phi-3/3.5 系列？
- 如何使用 Microsoft Phi-3/3.5 系列執行推論？

準備好了嗎？讓我們開始吧。

## 大型語言模型 (LLM) 與小型語言模型 (SLM) 之間的差異

LLM 和 SLM 都基於機率機器學習原則，並共享相似的架構設計、訓練方法、資料生成和評估技術。然而，有幾個關鍵因素使它們與眾不同。

## 小型語言模型的應用

SLM 用於許多領域，包括：

- 聊天機器人：提供客戶支援並以對話方式與使用者互動。
- 內容創作：協助作家產生想法或起草文章。
- 教育：協助學生寫作或語言學習。
- 無障礙性：為身心障礙人士建置工具，例如文字轉語音系統。

**尺寸**

LLM 和 SLM 之間的一個主要區別是它們的規模。像 ChatGPT (GPT-4) 這樣的 LLM 可以擁有約 1.76 兆個參數，而像 Mistral 7B 這樣的開源 SLM 則少得多——約 70 億個參數。這種差異源於模型架構和訓練的變化。例如，ChatGPT 在編碼器-解碼器框架內使用自注意力機制，而 Mistral 7B 在僅解碼器模型中採用滑動視窗注意力，從而實現更有效的訓練。這些架構差異極大地影響了模型的複雜性和效能。

**理解力**

SLM 通常針對特定領域進行優化，使其高度專業化，但在許多知識領域的廣泛上下文理解方面有時會受到限制。另一方面，LLM 旨在更全面地模仿人類般的智慧。LLM 在龐大且多樣化的資料集上進行訓練，在許多領域表現出色，提供更大的多功能性和適應性。因此，LLM 更適合廣泛的任務，包括自然語言處理和程式設計。

**計算**

訓練和執行 LLM 需要大量的計算資源，通常涉及大型 GPU 叢集。例如，從頭開始訓練像 ChatGPT 這樣的模型可能需要數千個 GPU 長時間運作。SLM 由於參數較少，在計算上更容易存取。像 Mistral 7B 這樣的模型可以在具有中等 GPU 效能的本機機器上進行訓練和執行，儘管訓練仍然需要多個 GPU 數小時。

**偏見**

偏見是 LLM 中一個已知的挑戰，主要是由於其訓練資料的性質。這些模型通常使用原始的、公開可用的網路資料，這些資料可能代表性不足或錯誤地代表某些群體，包含標籤錯誤，或反映來自方言、地區和語法規則的語言偏見。LLM 架構的複雜性也可能無意中放大偏見，如果沒有仔細微調，這可能不會被注意到。SLM 在更專注、特定領域的資料集上進行訓練，因此較不容易出現此類偏見，儘管它們並非完全免疫。

**推論**

SLM 較小的尺寸使其在推論速度方面具有巨大優勢，允許它們在本地硬體上高效地產生輸出，而無需大量的平行處理。LLM 由於其尺寸和複雜性，通常需要大量的平行計算資源才能達到合理的推論時間。當許多使用者同時存取 LLM 時，回應時間可能會變慢，尤其是在大規模情況下。

總之，雖然 LLM 和 SLM 共享機器學習基礎，但它們在模型大小、資源需求、上下文理解、偏見敏感性和推論速度方面存在顯著差異。這些差異決定了它們對各種使用案例的適用性：LLM 提供多功能性但資源密集，而 SLM 則以較低的計算需求提供特定領域的效率。

***注意：在本章中，我們將以 Microsoft Phi-3 / 3.5 為例介紹 SLM。***

## 介紹 Phi-3 / Phi-3.5 系列

Phi-3 / 3.5 系列主要針對文字、視覺和代理 (MoE) 應用情境：

### Phi-3 / 3.5 Instruct

主要用於文字生成、聊天完成和內容資訊提取。

**Phi-3-mini**

3.8B 參數語言模型可在 Microsoft Azure AI Studio、Hugging Face 和 Ollama 上使用。Phi-3 模型在關鍵基準測試中顯著優於相同或更大尺寸的語言模型（請參閱下面的基準分數；越高越好）。Phi-3-mini 的效能優於其兩倍大小的模型，而 Phi-3-small 和 Phi-3-medium 的效能優於包括 GPT-3.5 在內的更大模型。

**Phi-3-small & medium**

Phi-3-small 僅有 7B 參數，但在各種語言、推理、編碼和數學基準測試中擊敗了 GPT-3.5T。

Phi-3-medium 擁有 14B 參數，延續了這一趨勢，並超越了 Gemini 1.0 Pro。

**Phi-3.5-mini**

將其視為 Phi-3-mini 的升級版。雖然參數數量保持不變，但它改進了多語言支援（支援 20 多種語言：阿拉伯語、中文、捷克語、丹麥語、荷蘭語、英語、芬蘭語、法語、德語、希伯來語、匈牙利語、義大利語、日語、韓語、挪威語、波蘭語、葡萄牙語、俄語、西班牙語、瑞典語、泰語、土耳其語、烏克蘭語），並增加了對長上下文的更強支援。

Phi-3.5-mini 擁有 3.8B 參數，其效能優於相同大小的語言模型，並與其兩倍大小的模型相匹配。

### Phi-3 / 3.5 Vision

您可以將 Phi-3/3.5 Instruct 模型視為 Phi 理解語言的能力，而 Vision 則賦予 Phi「眼睛」來理解世界。

**Phi-3-Vision**

Phi-3-Vision 僅有 4.2B 參數，延續了這一趨勢，在一般視覺推理、OCR 以及表格和圖表理解任務方面，其效能優於 Claude-3 Haiku 和 Gemini 1.0 Pro V 等較大型模型。

**Phi-3.5-Vision**

Phi-3.5-Vision 是 Phi-3-Vision 的升級版，增加了對多個影像的支援。將其視為視覺方面的改進：它不僅能看圖片，還能看影片。

Phi-3.5-Vision 在 OCR、表格和圖表理解任務方面優於 Claude-3.5 Sonnet 和 Gemini 1.5 Flash 等較大型模型，並在一般視覺知識推理方面與它們相匹配。它支援多幀輸入，這意味著它可以同時對多個影像進行推理。

### Phi-3.5-MoE

***專家混合 (MoE)*** 允許模型以更少的計算進行預訓練，從而以與密集模型相同的計算預算實現模型或資料集大小的顯著擴展。具體來說，MoE 模型可以在預訓練期間比其密集對應模型更快地達到相同的品質。

Phi-3.5-MoE 由 16 個專家模組組成，每個模組有 3.8B 參數。Phi-3.5-MoE 僅有 6.6B 活躍參數，其推理、語言理解和數學能力可與更大的模型相媲美。

我們可以在不同的情境中使用 Phi-3/3.5 系列模型。與 LLM 不同，您可以在邊緣裝置上部署 Phi-3/3.5-mini 或 Phi-3/3.5-Vision。

## 如何使用 Phi-3/3.5 系列模型

我們旨在在各種情境中使用 Phi-3/3.5。接下來，我們將根據不同的使用案例探索使用 Phi-3/3.5。

![phi3](../../../translated_images/phi3.655208c3186ae38168d66032ed529d1d0d9c881ac531c95a2a5a32dbe11c38b4.en.png)

### 推論差異：雲端 API

**GitHub 模型**

GitHub 模型是最直接的方法。您可以透過 GitHub 模型快速存取 Phi-3/3.5-Instruct 模型。結合 Azure AI 推論 SDK 或 OpenAI SDK，您可以透過程式碼呼叫 API 以使用 Phi-3/3.5-Instruct。您也可以透過 Playground 測試不同的結果。

- 示範：Phi-3-mini 和 Phi-3.5-mini 在中文情境下的效能比較

![phi3](../../../translated_images/gh1.126c6139713b622b2564ef280de7d2a4c7f4c4a5e60cf577b94b47feec4342dd.en.png)

![phi35](../../../translated_images/gh2.07d7985af66f178df0c80d0331f39f763c5b5ec2859931d86ed7f2b43e6fa644.en.png)

**Azure AI Studio**

如果您想使用視覺和 MoE 模型，您可以使用 Azure AI Studio 進行呼叫。如果您有興趣，可以閱讀 Phi-3 Cookbook，了解如何透過 Azure AI Studio 呼叫 Phi-3/3.5 Instruct、Vision 和 MoE [點擊此連結](https://github.com/microsoft/Phi-3CookBook/blob/main/md/02.QuickStart/AzureAIStudio_QuickStart.md?WT.mc_id=academic-105485-koreyst)

**NVIDIA NIM**

除了 Azure 和 GitHub 的雲端模型目錄解決方案外，您還可以使用 [NVIDIA NIM](https://developer.nvidia.com/nim?WT.mc_id=academic-105485-koreyst) 進行相關呼叫。NVIDIA NIM (NVIDIA 推論微服務) 是一組加速推論微服務，旨在協助開發人員在各種環境中（包括雲端、資料中心和工作站）高效部署 AI 模型。

NVIDIA NIM 的主要功能包括：

- **易於部署：** NIM 允許 AI 模型以單一指令部署，使整合到現有工作流程中變得簡單。
- **優化效能：** 它使用 NVIDIA 預先優化的推論引擎，例如 TensorRT 和 TensorRT-LLM，以確保低延遲和高吞吐量。
- **可擴展性：** NIM 支援 Kubernetes 上的自動擴展，使其能夠有效地處理不同的工作負載。
- **安全性和控制：** 組織可以透過在其自己的受管理基礎設施上自行託管 NIM 微服務，來完全控制其資料和應用程式。
- **標準 API：** NIM 提供業界標準 API，使建置和整合 AI 應用程式（例如聊天機器人、AI 助理等）變得容易。

NIM 是 NVIDIA AI Enterprise 的一部分，旨在簡化 AI 模型的部署和操作，確保它們在 NVIDIA GPU 上高效運行。

- 示範：使用 Nvidia NIM 呼叫 Phi-3.5-Vision-API [[點擊此連結](../../../19-slm/python/Phi-3-Vision-Nividia-NIM.ipynb)]


### 在本機環境中推論 Phi-3/3.5
推論相關的 Phi-3 或任何語言模型（如 GPT-3），是指根據其接收到的輸入產生回應或預測的過程。當您向 Phi-3 提供提示或問題時，它會使用其訓練過的神經網路，透過分析其訓練資料中的模式和關係，來推斷最可能且相關的回應。

**Hugging Face Transformer**
Hugging Face Transformers 是一個功能強大的程式庫，專為自然語言處理 (NLP) 和其他機器學習任務而設計。以下是它的一些主要特點：

1. **預訓練模型：** 它提供數千個預訓練模型，用於各種任務，例如文字分類、命名實體辨識、問答、摘要、翻譯和文字生成。

2. **框架互通性：** 該程式庫支援多個深度學習框架，包括 PyTorch、TensorFlow 和 JAX。這允許您在一個框架中訓練模型，並在另一個框架中使用它。

3. **多模態功能：** 除了 NLP，Hugging Face Transformers 還支援電腦視覺（例如，影像分類、物件偵測）和音訊處理（例如，語音辨識、音訊分類）中的任務。

4. **易於使用：** 該程式庫提供 API 和工具，可輕鬆下載和微調模型，使其對初學者和專家都易於使用。

5. **社群和資源：** Hugging Face 擁有一個充滿活力的社群，以及豐富的文件、教學課程和指南，可幫助使用者入門並充分利用該程式庫。
[官方文件](https://huggingface.co/docs/transformers/index?WT.mc_id=academic-105485-koreyst) 或他們的 [GitHub 儲存庫](https://github.com/huggingface/transformers?WT.mc_id=academic-105485-koreyst)。

這是最常用的方法，但它也需要 GPU 加速。畢竟，像 Vision 和 MoE 這樣的情境涉及大量的計算，除非量化，否則在 CPU 上非常有限。


- 示範：使用 Transformer 呼叫 Phi-3.5-Instruct [點擊此連結](../../../19-slm/python/phi35-instruct-demo.ipynb)

- 示範：使用 Transformer 呼叫 Phi-3.5-Vision [點擊此連結](../../../19-slm/python/phi35-vision-demo.ipynb)

- 示範：使用 Transformer 呼叫 Phi-3.5-MoE [點擊此連結](../../../19-slm/python/phi35_moe_demo.ipynb)

**Ollama**
[Ollama](https://ollama.com/?WT.mc_id=academic-105485-koreyst) 是一個旨在讓您更輕鬆地在本機機器上執行大型語言模型 (LLM) 的平台。它支援各種模型，例如 Llama 3.1、Phi 3、Mistral 和 Gemma 2 等。該平台透過將模型權重、組態和資料捆綁到一個單一封裝中來簡化流程，使使用者更容易自訂和建立自己的模型。Ollama 可用於 macOS、Linux 和 Windows。如果您想在不依賴雲端服務的情況下實驗或部署 LLM，它是一個很棒的工具。Ollama 是最直接的方法——您只需要執行以下命令。


```bash

ollama run phi3.5

```


**ONNX Runtime for GenAI**

[ONNX Runtime](https://github.com/microsoft/onnxruntime-genai?WT.mc_id=academic-105485-koreyst) 是一個跨平台推論和訓練機器學習加速器。ONNX Runtime for Generative AI (GENAI) 是一個功能強大的工具，可協助您在各種平台上高效執行生成式 AI 模型。

## 什麼是 ONNX Runtime？
ONNX Runtime 是一個開源專案，可實現機器學習模型的高效能推論。它支援 Open Neural Network Exchange (ONNX) 格式的模型，該格式是表示機器學習模型的標準。ONNX Runtime 推論可以提供更快的客戶體驗並降低成本，支援來自深度學習框架（例如 PyTorch 和 TensorFlow/Keras）以及傳統機器學習程式庫（例如 scikit-learn、LightGBM、XGBoost 等）的模型。ONNX Runtime 與不同的硬體、驅動程式和作業系統相容，透過利用可用的硬體加速器，以及圖形優化和轉換，提供最佳效能。

## 什麼是生成式 AI？
生成式 AI 是指可以根據其訓練資料建立新內容（例如文字、影像或音樂）的 AI 系統。範例包括像 GPT-3 這樣的語言模型和像 Stable Diffusion 這樣的影像生成模型。ONNX Runtime for GenAI 程式庫為 ONNX 模型提供生成式 AI 工作流程，包括使用 ONNX Runtime 進行推論、logits 處理、搜尋和取樣，以及 KV 快取管理。

## ONNX Runtime for GENAI
ONNX Runtime for GENAI 擴展了 ONNX Runtime 的功能，以支援生成式 AI 模型。主要功能包括：

- **廣泛的平台支援：** 適用於各種平台，包括 Windows、Linux、macOS、Android 和 iOS。
- **模型支援：** 支援許多流行的生成式 AI 模型，例如 LLaMA、GPT-Neo、BLOOM 等。
- **效能優化：** 包含針對不同硬體加速器（例如 NVIDIA GPU、AMD GPU 等）的優化。
- **易於使用：** 提供 API 以便輕鬆整合到應用程式中，讓您可以用最少的程式碼產生文字、影像和其他內容。
- 使用者可以呼叫高階的 generate() 方法，或在迴圈中執行模型的每次迭代，一次產生一個權杖，並可選擇在迴圈中更新生成參數。
- ONNX Runtime 還支援貪婪/束搜尋和 TopP、TopK 取樣以產生權杖序列，以及內建的 logits 處理，例如重複懲罰。您還可以輕鬆新增自訂評分。

## 入門
若要開始使用 ONNX Runtime for GENAI，請遵循以下步驟：

### 安裝 ONNX Runtime：
```Python
pip install onnxruntime
```
### 安裝生成式 AI 擴充功能：
```Python
pip install onnxruntime-genai
```

### 執行模型：以下是一個簡單的 Python 範例：
```Python
import onnxruntime_genai as og

model = og.Model('path_to_your_model.onnx')

tokenizer = og.Tokenizer(model)

input_text = "Hello, how are you?"

input_tokens = tokenizer.encode(input_text)

output_tokens = model.generate(input_tokens)

output_text = tokenizer.decode(output_tokens)

print(output_text)
```
### 示範：使用 ONNX Runtime GenAI 呼叫 Phi-3.5-Vision


```python

import onnxruntime_genai as og

model_path = './您的 Phi-3.5-vision-instruct ONNX 路徑'

img_path = './您的影像路徑'

model = og.Model(model_path)

processor = model.create_multimodal_processor()

tokenizer_stream = processor.create_stream()

text = "您的提示"

prompt = "<|user|>\n"

prompt += "<|image_1|>\n"

prompt += f"{text}<|end|>\n"

prompt += "<|assistant|>\n"

image = og.Images.open(img_path)

inputs = processor(prompt, images=image)

params = og.GeneratorParams(model)

params.set_inputs(inputs)

params.set_search_options(max_length=3072)

generator = og.Generator(model, params)

while not generator.is_done():

    generator.compute_logits()
    
    generator.generate_next_token()

    new_token = generator.get_next_tokens()[0]
    
    code += tokenizer_stream.decode(new_token)
    
    print(tokenizer_stream.decode(new_token), end='', flush=True)

```


**其他**

除了 ONNX Runtime 和 Ollama 參考方法之外，您還可以根據不同製造商提供的模型參考方法來完成量化模型的參考。範例包括 Apple Metal 的 Apple MLX 框架、NPU 的 Qualcomm QNN、CPU/GPU 的 Intel OpenVINO 等。您可以在 [Phi-3 Cookbook](https://github.com/microsoft/phi-3cookbook?WT.mc_id=academic-105485-koreyst) 中找到其他資源。


## 更多

我們已經涵蓋了 Phi-3/3.5 系列的基礎知識，但要了解更多關於 SLM 的資訊，還需要進一步的知識。您可以在 Phi-3 Cookbook 中找到答案。如需更多資訊，請造訪 [Phi-3 Cookbook](https://github.com/microsoft/phi-3cookbook?WT.mc_id=academic-105485-koreyst)。

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。
