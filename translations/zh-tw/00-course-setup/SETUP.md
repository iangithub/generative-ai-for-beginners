<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f12faf55ab620aef9f6761679b7ac68b",
  "translation_date": "2025-07-09T07:20:16+00:00",
  "source_file": "00-course-setup/SETUP.md",
  "language_code": "zh-tw"
}
-->
# 設定您的開發環境

我們使用[開發容器](https://containers.dev?WT.mc_id=academic-105485-koreyst)設定此儲存庫和課程，其中包含支援 Python3、.NET、Node.js 和 Java 開發的通用執行階段。相關設定定義在此儲存庫根目錄的 `.devcontainer/` 資料夾中的 `devcontainer.json` 檔案中。

若要啟用開發容器，請在 [GitHub Codespaces](https://docs.github.com/en/codespaces/overview?WT.mc_id=academic-105485-koreyst) (用於雲端託管的執行階段) 或 [Docker Desktop](https://docs.docker.com/desktop/?WT.mc_id=academic-105485-koreyst) (用於本機裝置託管的執行階段) 中啟動它。請閱讀[此文件](https://code.visualstudio.com/docs/devcontainers/containers?WT.mc_id=academic-105485-koreyst)以取得有關開發容器如何在 VS Code 中運作的更多詳細資料。

> [!TIP]
> 我們建議使用 GitHub Codespaces 以最少的力氣快速入門。它為個人帳戶提供慷慨的[免費使用配額](https://docs.github.com/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces#monthly-included-storage-and-core-hours-for-personal-accounts?WT.mc_id=academic-105485-koreyst)。設定[逾時](https://docs.github.com/codespaces/setting-your-user-preferences/setting-your-timeout-period-for-github-codespaces?WT.mc_id=academic-105485-koreyst)以停止或刪除閒置的 codespace，以充分利用您的配額。

## 1. 執行作業

每堂課可能包含一或多種程式語言 (例如 Python、.NET/C#、Java 和 JavaScript/TypeScript) 的_選修_作業。本節提供有關如何執行這些作業的一般指引。

### 1.1 Python 作業

Python 作業以應用程式 (`.py` 檔案) 或 Jupyter 筆記本 (`.ipynb` 檔案) 的形式提供。
- 若要執行筆記本，請在 Visual Studio Code 中開啟它，然後按一下_選取核心_ (右上角) 並選擇預設的 Python 3 選項。然後您可以_全部執行_以執行筆記本。
- 若要從命令列執行 Python 應用程式，請遵循特定作業的指示以選取正確的檔案並提供任何必要的引數。

## 2. 設定提供者

作業**可能**也會設定為可與一或多個大型語言模型 (LLM) 部署搭配使用，這些部署是透過支援的服務提供者 (例如 OpenAI、Azure 或 Hugging Face) 提供的。這些提供者提供可透過適當的憑證 (API 金鑰或權杖) 以程式設計方式存取的_託管端點_ (API)。在本課程中，我們將介紹這些提供者：

- [OpenAI](https://platform.openai.com/docs/models?WT.mc_id=academic-105485-koreyst)，提供各種模型，包括核心的 GPT 系列。
- [Azure OpenAI](https://learn.microsoft.com/azure/ai-services/openai/?WT.mc_id=academic-105485-koreyst)，提供具有企業級功能的 OpenAI 模型。
- [Hugging Face](https://huggingface.co/docs/hub/index?WT.mc_id=academic-105485-koreyst)，提供開源模型和推論伺服器。

**您需要使用自己的帳戶來進行這些練習**。作業是選修的，因此您可以根據自己的興趣選擇設定一個、全部或不設定任何提供者。以下是一些註冊指引：

| 註冊 | 費用 | API 金鑰 | 遊樂場 | 備註 |
|:---|:---|:---|:---|:---|
| [OpenAI](https://platform.openai.com/signup?WT.mc_id=academic-105485-koreyst) | [定價](https://openai.com/pricing#language-models?WT.mc_id=academic-105485-koreyst) | [專案式](https://platform.openai.com/api-keys?WT.mc_id=academic-105485-koreyst) | [無程式碼，網頁版](https://platform.openai.com/playground?WT.mc_id=academic-105485-koreyst) | 提供多種模型 |
| [Azure](https://aka.ms/azure/free?WT.mc_id=academic-105485-koreyst) | [定價](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/?WT.mc_id=academic-105485-koreyst) | [SDK 快速入門](https://learn.microsoft.com/azure/ai-services/openai/quickstart?WT.mc_id=academic-105485-koreyst) | [Studio 快速入門](https://learn.microsoft.com/azure/ai-services/openai/quickstart?WT.mc_id=academic-105485-koreyst) | [必須預先申請存取權限](https://learn.microsoft.com/azure/ai-services/openai/?WT.mc_id=academic-105485-koreyst) |
| [Hugging Face](https://huggingface.co/join?WT.mc_id=academic-105485-koreyst) | [定價](https://huggingface.co/pricing) | [存取權杖](https://huggingface.co/docs/hub/security-tokens?WT.mc_id=academic-105485-koreyst) | [Hugging Chat](https://huggingface.co/chat/?WT.mc_id=academic-105485-koreyst) | [Hugging Chat 的模型有限](https://huggingface.co/chat/models?WT.mc_id=academic-105485-koreyst) |
| | | | | |

請遵循以下指示來_設定_此儲存庫以與不同的提供者搭配使用。需要特定提供者的作業，其檔名中將包含下列其中一個標籤：
- `aoai` - 需要 Azure OpenAI 端點和金鑰
- `oai` - 需要 OpenAI 端點和金鑰
- `hf` - 需要 Hugging Face 權杖

您可以設定一個、不設定或全部設定提供者。如果缺少必要的憑證，作業將會失敗。

### 2.1. 建立 `.env` 檔案

我們假設您已經閱讀了上述指引、向相關提供者註冊，並取得了必要的驗證憑證 (API_KEY 或權杖)。對於 Azure OpenAI，我們也假設您已擁有一個有效的 Azure OpenAI 服務部署 (端點)，且至少部署了一個用於聊天完成的 GPT 模型。

下一步是如下設定您的**本機環境變數**：

1. 在根資料夾中尋找一個 `.env.copy` 檔案，其內容應如下所示：

   ```bash
   # OpenAI 提供者
   OPENAI_API_KEY='<在此處新增您的 OpenAI API 金鑰>'

   ## Azure OpenAI
   AZURE_OPENAI_API_VERSION='2024-02-01' # 已設定預設值！
   AZURE_OPENAI_API_KEY='<在此處新增您的 AOAI 金鑰>'
   AZURE_OPENAI_ENDPOINT='<在此處新增您的 AOIA 服務端點>'
   AZURE_OPENAI_DEPLOYMENT='<在此處新增您的聊天完成模型名稱>' 
   AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT='<在此處新增您的嵌入模型名稱>'

   ## Hugging Face
   HUGGING_FACE_API_KEY='<在此處新增您的 HuggingFace API 或權杖>'
   ```

2. 使用以下指令將該檔案複製到 `.env`。此檔案已加入 `gitignore`，以確保您的密鑰安全。

   ```bash
   cp .env.copy .env
   ```

3. 如下一節所述填寫值 (取代 `=` 右側的預留位置)。

3. (選用) 如果您使用 GitHub Codespaces，您可以將環境變數儲存為連結至此儲存庫的 _Codespaces 密鑰_。在這種情況下，您不需要設定本機 `.env` 檔案。**但是，請注意，此選項僅在您使用 GitHub Codespaces 時才有效。** 如果您改用 Docker Desktop，您仍然需要設定 `.env` 檔案。

### 2.2. 填寫 `.env` 檔案

以下是變數名稱及其代表意義的快速總覽：

| 變數 | 說明 |
| :--- | :--- |
| HUGGING_FACE_API_KEY | 這是您在個人資料中設定的使用者存取權杖 |
| OPENAI_API_KEY | 這是用於非 Azure OpenAI 端點服務的授權金鑰 |
| AZURE_OPENAI_API_KEY | 這是用於 Azure OpenAI 服務的授權金鑰 |
| AZURE_OPENAI_ENDPOINT | 這是 Azure OpenAI 資源的已部署端點 |
| AZURE_OPENAI_DEPLOYMENT | 這是_文字產生_模型部署端點 |
| AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT | 這是_文字嵌入_模型部署端點 |
| | |

注意：最後兩個 Azure OpenAI 變數分別對應於聊天完成 (文字產生) 和向量搜尋 (嵌入) 的預設模型。設定這些變數的說明將在相關作業中提供。

### 2.3 設定 Azure：從入口網站

您可以在 [Azure 入口網站](https://portal.azure.com?WT.mc_id=academic-105485-koreyst) 中找到 Azure OpenAI 端點和金鑰值。讓我們從那裡開始。

1. 前往 [Azure 入口網站](https://portal.azure.com?WT.mc_id=academic-105485-koreyst)
2. 按一下側邊欄 (左側選單) 中的 **金鑰和端點** 選項。
3. 按一下 **顯示金鑰** — 您應該會看到 KEY 1、KEY 2 和端點。
4. 將 KEY 1 的值用於 `AZURE_OPENAI_API_KEY`
5. 將端點的值用於 `AZURE_OPENAI_ENDPOINT`

接下來，我們需要您已部署的特定模型的端點。

1. 按一下您 Azure OpenAI 資源的側邊欄 (左側選單) 中的 **模型部署** 選項。
2. 在目標頁面中，按一下 **管理部署**

這將帶您前往 Azure OpenAI Studio 網站，您將在其中找到如下所述的其他值。

### 2.4 設定 Azure：從 Studio

1. 如上所述，**從您的資源** 導覽至 [Azure OpenAI Studio](https://oai.azure.com?WT.mc_id=academic-105485-koreyst)。
2. 按一下 **部署** 索引標籤 (側邊欄，左側) 以檢視目前已部署的模型。
3. 如果您想要的模型尚未部署，請使用 **建立新部署** 來部署它。
4. 您將需要一個_文字產生_模型 — 我們建議：**gpt-35-turbo**
5. 您將需要一個_文字嵌入_模型 — 我們建議 **text-embedding-ada-002**

現在更新環境變數以反映所使用的_部署名稱_。除非您明確變更它，否則這通常會與模型名稱相同。例如，您可能會這樣設定：

```bash
AZURE_OPENAI_DEPLOYMENT='gpt-35-turbo'
AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT='text-embedding-ada-002'
```

**完成後別忘了儲存 `.env` 檔案**。然後您可以關閉檔案並返回執行筆記本的說明。

### 2.5 設定 OpenAI：從個人資料

您的 OpenAI API 金鑰可以在您的 [OpenAI 帳戶](https://platform.openai.com/api-keys?WT.mc_id=academic-105485-koreyst) 中找到。如果您沒有帳戶，可以註冊並建立一個 API 金鑰。取得金鑰後，請使用它來填寫 `.env` 檔案中的 `OPENAI_API_KEY` 變數。

### 2.6 設定 Hugging Face：從個人資料

您的 Hugging Face 權杖可以在您的個人資料中的 [存取權杖](https://huggingface.co/settings/tokens?WT.mc_id=academic-105485-koreyst) 下找到。請勿公開分享這些權杖。相反地，請為此專案特別建立一個新權杖，並將其複製到 `.env` 檔案的 `HUGGING_FACE_API_KEY` 變數下。_注意：_ 這在技術上不是 API 金鑰，但用於驗證，因此我們保持命名一致。

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。