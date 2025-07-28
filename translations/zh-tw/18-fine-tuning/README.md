<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "68664f7e754a892ae1d8d5e2b7bd2081",
  "translation_date": "2025-07-09T17:33:54+00:00",
  "source_file": "18-fine-tuning/README.md",
  "language_code": "zh-tw"
}
-->
[![開源模型](../../../translated_images/18-lesson-banner.f30176815b1a5074fce9cceba317720586caa99e24001231a92fd04eeb54a121.en.png)](https://aka.ms/gen-ai-lesson18-gh?WT.mc_id=academic-105485-koreyst)

# 微調您的 LLM

使用大型語言模型建置生成式 AI 應用程式帶來了新的挑戰。一個關鍵問題是確保模型針對給定使用者請求所產生回應的品質（準確性和相關性）。在之前的課程中，我們涵蓋了提示工程和檢索增強生成等技術，這些技術試圖透過「修改現有模型的提示輸入」來解決這個問題。

在今天的課程中，我們將探討第三種技術，**微調**，它透過「使用額外資料重新訓練模型本身」來解決這個挑戰。讓我們深入了解細節。

## 學習目標

本課程介紹了預訓練語言模型的微調概念，探討了這種方法的優點和挑戰，並提供了何時以及如何使用微調來提高生成式 AI 模型效能的指導。

在本課結束時，您應該能夠回答：

- 什麼是語言模型的微調？
- 何時以及為何微調有用？
- 我如何微調預訓練模型？
- 微調的限制是什麼？

準備好了嗎？讓我們開始吧。

## 圖解指南

想在深入學習之前了解我們將涵蓋的內容嗎？請查看此圖解指南，其中概述了本課的學習旅程——從了解微調的核心概念和動機，到執行微調的過程和最佳實務。這是一個引人入勝的主題，所以別忘了造訪 [資源](./RESOURCES.md?WT.mc_id=academic-105485-koreyst) 頁面，以獲取更多連結來支援您的自學！

![語言模型微調圖解指南](../../../translated_images/18-fine-tuning-sketchnote.11b21f9ec8a703467a120cb79a28b5ac1effc8d8d9d5b31bbbac6b8640432e14.en.png)

## 什麼是語言模型的微調？

根據定義，大型語言模型是透過來自不同來源（包括網際網路）的大量文字進行「預訓練」的。正如我們在之前的課程中學到的，像「提示工程」和「檢索增強生成」這樣的技術有助於提高模型對使用者提示的回應品質。

一種常見的提示工程方法涉及為模型提供更多關於回應中預期內容的指導，方法是提供「指令」（明確指導）或「少量範例」（隱含指導）。這稱為「少樣本學習」，但它有兩個限制：

- 模型權杖限制限制了您可以提供的範例數量，從而限制了有效性。
- 權杖成本可能會使每個提示新增範例變得昂貴，從而降低彈性。

微調是一種常見的機器學習實踐，其中預訓練模型會使用新資料重新訓練，以提高其在特定任務上的效能。對於語言模型，我們可以「使用針對特定任務或領域的精選範例」來微調預訓練模型，以建立一個更準確且與該使用案例相關的**自訂模型**。微調的一個好處是它可以減少少樣本學習所需的範例數量——降低權杖使用量和相關成本。

## 何時以及為何我們應該微調模型？

這裡的微調指的是**監督式**微調，其中重新訓練是透過**新增不在原始訓練集中的新資料**來完成的。這與非監督式微調不同，後者是在原始資料上重新訓練模型，但使用不同的超參數。

關鍵點是，微調是一種進階技術，需要專業知識才能取得良好結果。如果操作不當，它可能無法提高效能，甚至可能損害模型對目標領域的有效性。

在學習「如何」微調之前，您需要了解「為何」要這樣做以及「何時」開始。問問自己：

- **使用案例**：您的微調「使用案例」是什麼？您想改進目前預訓練模型的哪個部分？
- **替代方案**：您是否嘗試過「其他技術」來實現您的目標？將它們用作基準。
  - 提示工程：嘗試使用相關範例進行少樣本提示。評估回應品質。
  - 檢索增強生成：嘗試使用您的資料中的搜尋結果來增強提示。評估回應品質。
- **成本**：您是否已確定微調的成本？
  - 可調性 – 預訓練模型是否可用於微調？
  - 工作量 – 準備訓練資料、評估和完善模型。
  - 計算 – 執行微調作業和部署微調模型。
  - 資料 – 存取足夠的品質範例以使微調有效。
- **好處**：您是否已確認微調的好處？
  - 品質 – 微調模型是否優於基準？
  - 成本 – 它是否透過簡化提示來減少權杖使用量？
  - 可擴展性 – 您是否可以將基礎模型應用於新領域？

回答這些問題將幫助您決定微調是否適合您的使用案例。理想情況下，好處應該大於成本。一旦您決定繼續，就該考慮「如何」微調預訓練模型了。

想了解更多關於此決策的見解嗎？觀看 [要微調還是不微調](https://www.youtube.com/watch?v=0Jo-z-MFxJs)

## 我們如何微調預訓練模型？

若要微調預訓練模型，您需要：

- 一個要微調的預訓練模型
- 一個用於微調的資料集
- 一個用於執行微調作業的訓練環境
- 一個用於部署微調模型的託管環境

## 微調實作

以下資源提供了使用選定模型和精選資料集的逐步教學課程和實際範例。若要遵循這些教學課程，您需要擁有提供者的帳戶，並存取相關的模型和資料集。

| 提供者 | 教學課程 | 說明 |
| --- | --- | --- |
| OpenAI | [如何微調聊天模型](https://github.com/openai/openai-cookbook/blob/main/examples/How_to_finetune_chat_models.ipynb?WT.mc_id=academic-105485-koreyst) | 了解如何微調 `gpt-35-turbo` 模型以用於特定領域（「食譜助理」），方法是準備訓練資料、執行微調作業，以及使用微調模型進行推論。 |
| Azure OpenAI | [GPT 3.5 Turbo 微調教學課程](https://learn.microsoft.com/azure/ai-services/openai/tutorials/fine-tune?tabs=python-new%2Ccommand-line?WT.mc_id=academic-105485-koreyst) | 了解如何**在 Azure 上**微調 `gpt-35-turbo-0613` 模型，方法是建立和上傳訓練資料、執行微調作業，然後部署和使用新模型。 |
| Hugging Face | [使用 Hugging Face 微調 LLM](https://www.philschmid.de/fine-tune-llms-in-2024-with-trl?WT.mc_id=academic-105485-koreyst) | 這篇部落格文章引導您使用 [transformers](https://huggingface.co/docs/transformers/index?WT.mc_id=academic-105485-koreyst) 程式庫和 [Transformer 強化學習 (TRL)](https://huggingface.co/docs/trl/index?WT.mc_id=academic-105485-koreyst) 在 Hugging Face 上使用開放[資料集](https://huggingface.co/docs/datasets/index?WT.mc_id=academic-105485-koreyst)微調「開放 LLM」（例如 `CodeLlama 7B`）。 |
| | | |
| 🤗 AutoTrain | [使用 AutoTrain 微調 LLM](https://github.com/huggingface/autotrain-advanced/?WT.mc_id=academic-105485-koreyst) | AutoTrain (或 AutoTrain Advanced) 是 Hugging Face 的一個 Python 程式庫，支援許多任務的微調，包括 LLM 微調。AutoTrain 是一個無程式碼解決方案，可以在您的雲端、Hugging Face Spaces 或本機執行。它支援基於 Web 的 GUI、CLI，以及透過 YAML 設定檔進行訓練。 |
| | | |

## 作業

選擇上述其中一個教學課程並完成它。_我們可能會在本儲存庫中複製這些教學課程的版本，僅供參考。請直接使用原始來源以獲取最新版本。_

## 做得好！繼續學習。

完成本課後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 技能！

恭喜！您已完成本課程 v2 系列的最後一課！繼續學習和建置。**請查看 [資源](RESOURCES.md?WT.mc_id=academic-105485-koreyst) 頁面以獲取更多關於此主題的建議。**

我們的 v1 系列也已更新，包含更多作業和概念。花點時間更新您的知識——並請[分享您的問題和回饋](https://github.com/microsoft/generative-ai-for-beginners/issues?WT.mc_id=academic-105485-koreyst)以幫助我們為社群改進這些課程。

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。