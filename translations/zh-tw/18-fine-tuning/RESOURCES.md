<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c2f423d1402f71ca3869ec135bb77d16",
  "translation_date": "2025-07-09T17:52:42+00:00",
  "source_file": "18-fine-tuning/RESOURCES.md",
  "language_code": "zh-tw"
}
-->
# 自學資源

本課程是使用 OpenAI 和 Azure OpenAI 的幾個關鍵資源作為術語和教學課程的參考而建立的。以下是您自學旅程的非詳盡清單。

## 1. 主要資源

| 標題/連結 | 說明 |
| :--- | :--- |
| [使用 OpenAI 模型進行微調](https://platform.openai.com/docs/guides/fine-tuning?WT.mc_id=academic-105485-koreyst) | 微調透過訓練比提示中能容納的更多範例來增強少樣本學習，從而節省成本、提高回應品質並實現更低的延遲請求。**從 OpenAI 獲取微調概述。** |
| [什麼是 Azure OpenAI 的微調？](https://learn.microsoft.com/azure/ai-services/openai/concepts/fine-tuning-considerations#what-is-fine-tuning-with-azure-openai?WT.mc_id=academic-105485-koreyst) | 了解**什麼是微調（概念）**、為何值得考慮（動機問題）、使用什麼資料（訓練）以及如何衡量品質。 |
| [使用微調自訂模型](https://learn.microsoft.com/azure/ai-services/openai/how-to/fine-tuning?tabs=turbo%2Cpython&pivots=programming-language-studio#continuous-fine-tuning?WT.mc_id=academic-105485-koreyst) | Azure OpenAI 服務可讓您使用微調將模型調整為您自己的資料集。了解**如何微調（過程）**選定的模型，使用 Azure AI Studio、Python SDK 或 REST API。 |
| [LLM 微調建議](https://learn.microsoft.com/ai/playbook/technology-guidance/generative-ai/working-with-llms/fine-tuning-recommend?WT.mc_id=academic-105485-koreyst) | LLM 可能在特定領域、任務或資料集方面遇到困難，或產生不準確或誤導性的輸出。**何時應考慮微調**作為解決方案？ |
| [持續微調](https://learn.microsoft.com/azure/ai-services/openai/how-to/fine-tuning?tabs=turbo%2Cpython&pivots=programming-language-studio#continuous-fine-tuning?WT.mc_id=academic-105485-koreyst) | 持續微調是將已微調的模型作為基礎，並在新的訓練範例上**進一步微調**的迭代過程。 |
| [微調和函式呼叫](https://learn.microsoft.com/azure/ai-services/openai/how-to/fine-tuning-functions?WT.mc_id=academic-105485-koreyst) | 使用函式呼叫範例微調您的模型可以透過產生更準確、更一致的回應並具有相似的格式來改善輸出，同時也節省成本。 |
| [微調模型：Azure OpenAI 指南](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#fine-tuning-models?WT.mc_id=academic-105485-koreyst) | 檢查此表格以查看 Azure OpenAI 中**哪些模型可以微調**，其可用區域、權杖限制以及訓練資料到期日期（如果需要）。 |
| [要微調還是不微調？這是個問題](https://learn.microsoft.com/shows/ai-show/to-fine-tune-or-not-fine-tune-that-is-the-question?WT.mc_id=academic-105485-koreyst) | 這部 2023 年 10 月的 30 分鐘 AI Show 影片涵蓋了優點、缺點和實用見解，可幫助您決定是否進行微調。 |
| [LLM 微調入門](https://learn.microsoft.com/ai/playbook/technology-guidance/generative-ai/working-with-llms/fine-tuning-recommend?WT.mc_id=academic-105485-koreyst) | 這份 **AI 劇本**資源引導您了解資料要求、格式化、超參數調整以及需要注意的挑戰/限制。 |
| **教學課程**：[Azure OpenAI GPT3.5 Turbo 微調](https://learn.microsoft.com/azure/ai-services/openai/tutorials/fine-tune?tabs=python%2Ccommand-line?WT.mc_id=academic-105485-koreyst) | 了解如何建立範例微調資料集、準備微調、建立微調作業，以及在 Azure 上部署微調模型。 |
| **教學課程**：[在 Azure AI Studio 中微調 Llama 2 模型](https://learn.microsoft.com/azure/ai-studio/how-to/fine-tune-model-llama?WT.mc_id=academic-105485-koreyst) | Azure AI Studio 可讓您使用「適合低程式碼開發人員的 UI 型工作流程」將大型語言模型自訂為您自己的資料集。請參閱此範例。 |
| **教學課程**：[在 Azure 上為單一 GPU 微調 Hugging Face 模型](https://learn.microsoft.com/azure/databricks/machine-learning/train-model/huggingface/fine-tune-model?WT.mc_id=academic-105485-koreyst) | 本文說明如何使用 Azure Databricks 和 Hugging Face Trainer 程式庫，在單一 GPU 上使用 transformers 程式庫微調 Hugging Face 模型。 |
| **訓練**：[使用 Azure Machine Learning 微調基礎模型](https://learn.microsoft.com/training/modules/finetune-foundation-model-with-azure-machine-learning/?WT.mc_id=academic-105485-koreyst) | Azure Machine Learning 的模型目錄提供了許多開源模型，您可以針對您的特定任務進行微調。請嘗試來自 [AzureML 生成式 AI 學習路徑](https://learn.microsoft.com/training/paths/work-with-generative-models-azure-machine-learning/?WT.mc_id=academic-105485-koreyst) 的此模組。 |
| **教學課程**：[Azure OpenAI 微調](https://docs.wandb.ai/guides/integrations/azure-openai-fine-tuning?WT.mc_id=academic-105485-koreyst) | 使用 W&B 在 Microsoft Azure 上微調 GPT-3.5 或 GPT-4 模型，可實現模型效能的詳細追蹤和分析。本指南以 OpenAI 微調指南為基礎，並包含 Azure OpenAI 的特定步驟和功能。 |
| | | |

## 2. 次要資源

本節列出了值得探索的其他資源，儘管我們在本課中沒有時間涵蓋它們。它們可能會包含在未來的課程中，或稍後作為選修作業提供。目前，請使用它們來加深您對此主題的專業知識和知識。

| 標題/連結 | 說明 |
| :--- | :--- |
| **OpenAI Cookbook**：[聊天模型微調的資料準備和分析](https://cookbook.openai.com/examples/chat_finetuning_data_prep?WT.mc_id=academic-105485-koreyst) | 本筆記本有助於預處理和分析用於微調聊天模型的聊天資料集。它檢查格式錯誤，提供基本統計資料，並估計權杖計數以幫助計算微調成本。請參閱：[gpt-3.5-turbo 的微調方法](https://platform.openai.com/docs/guides/fine-tuning?WT.mc_id=academic-105485-koreyst)。 |
| **OpenAI Cookbook**：[使用 Qdrant 進行檢索增強生成 (RAG) 的微調](https://cookbook.openai.com/examples/fine-tuned_qa/ft_retrieval_augmented_generation_qdrant?WT.mc_id=academic-105485-koreyst) | 本筆記本透過詳細範例說明了如何微調 OpenAI 模型以進行檢索增強生成 (RAG)。它還整合了 Qdrant 和少樣本學習，以提高模型效能並減少幻覺。 |
| **OpenAI Cookbook**：[使用 Weights & Biases 微調 GPT](https://cookbook.openai.com/examples/third_party/gpt_finetuning_with_wandb?WT.mc_id=academic-105485-koreyst) | Weights & Biases (W&B) 是一個 AI 開發者平台，提供用於訓練、微調和利用基礎模型的工具。請先閱讀他們的 [OpenAI 微調](https://docs.wandb.ai/guides/integrations/openai-fine-tuning/?WT.mc_id=academic-105485-koreyst) 指南，然後嘗試 Cookbook 練習。 |
| **社群教學課程** [Phinetuning 2.0](https://huggingface.co/blog/g-ronimo/phinetuning?WT.mc_id=academic-105485-koreyst) - 小型語言模型的微調 | 認識 [Phi-2](https://www.microsoft.com/research/blog/phi-2-the-surprising-power-of-small-language-models/?WT.mc_id=academic-105485-koreyst)，微軟新的小而強大的模型。本教學課程引導您微調 Phi-2，展示如何建置自訂資料集並使用 QLoRA 微調模型。 |
| **Hugging Face 教學課程** [如何使用 Hugging Face 在 2024 年微調 LLM](https://www.philschmid.de/fine-tune-llms-in-2024-with-trl?WT.mc_id=academic-105485-koreyst) | 這篇部落格文章引導您使用 Hugging Face TRL、Transformers 和 2024 年的資料集微調開放 LLM。您定義一個使用案例，設定開發環境，準備資料集，微調模型，評估它，並將其部署到生產環境。 |
| **Hugging Face**：[AutoTrain Advanced](https://github.com/huggingface/autotrain-advanced?WT.mc_id=academic-105485-koreyst) | 提供更快、更輕鬆的[最先進機器學習模型](https://twitter.com/abhi1thakur/status/1755167674894557291?WT.mc_id=academic-105485-koreyst)的訓練和部署。該儲存庫包含與 Colab 相容的教學課程，並附有 YouTube 影片指南，用於微調。**反映最近的[本地優先](https://twitter.com/abhi1thakur/status/1750828141805777057?WT.mc_id=academic-105485-koreyst)更新**。請參閱 [AutoTrain 文件](https://huggingface.co/autotrain?WT.mc_id=academic-105485-koreyst)。 |
| | | |

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。