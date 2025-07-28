<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "00f2643fec1571acc5d38cc1a3b972d5",
  "translation_date": "2025-07-09T06:57:36+00:00",
  "source_file": "00-course-setup/README.md",
  "language_code": "zh-tw"
}
-->
# 開始本課程

我們很高興您能開始本課程，並期待看到您受生成式 AI 啟發而打造的作品！

為協助您成功，本頁概述了設定步驟、技術要求以及需要時尋求協助的地方。

## 設定步驟

要開始本課程，您需要完成以下步驟。

### 1. Fork 本儲存庫

[Fork 這個完整的儲存庫](https://github.com/microsoft/generative-ai-for-beginners/fork?WT.mc_id=academic-105485-koreyst) 到您自己的 GitHub 帳戶，以便您可以修改程式碼並完成挑戰。您也可以 [star (🌟) 這個儲存庫](https://docs.github.com/en/get-started/exploring-projects-on-github/saving-repositories-with-stars?WT.mc_id=academic-105485-koreyst) 以便更容易找到它和相關的儲存庫。

### 2. 建立一個 codespace

為避免執行程式碼時出現相依性問題，我們建議使用 [GitHub Codespaces](https://github.com/features/codespaces?WT.mc_id=academic-105485-koreyst)。

您可以在您 fork 的儲存庫上選擇 `Code` 按鈕並選擇 **Codespaces** 選項來建立一個。

![顯示建立 codespace 按鈕的對話方塊](../../../00-course-setup/images/who-will-pay.webp)

### 3. 儲存您的 API 金鑰

在建置任何應用程式時，確保您的 API 金鑰安全至關重要。我們建議不要將 API 金鑰直接儲存在您的程式碼中。將它們提交到公開儲存庫可能會導致安全性風險和不當使用時的意外費用。

以下是為 Python 建立 `.env` 檔案並新增您的 `GITHUB_TOKEN` 的逐步指南：

1. **導覽至您的專案目錄**：開啟您的終端機或命令提示字元，並前往您要建立 `.env` 檔案的專案根目錄。

   ```bash
   cd path/to/your/project
   ```

2. **建立 `.env` 檔案**：使用您偏好的文字編輯器建立一個名為 `.env` 的新檔案。在命令列中，您可以使用 `touch` (類 Unix 系統) 或 `echo` (Windows)：

   類 Unix 系統：

   ```bash
   touch .env
   ```

   Windows：

   ```cmd
   echo . > .env
   ```

3. **編輯 `.env` 檔案**：在文字編輯器 (例如 VS Code、Notepad++ 或任何其他編輯器) 中開啟 `.env`。新增以下行，將 `your_github_token_here` 取代為您實際的 GitHub token：

   ```env
   GITHUB_TOKEN=your_github_token_here
   ```

4. **儲存檔案**：儲存並關閉編輯器。

5. **安裝 `python-dotenv`**：如果您尚未安裝，請安裝 `python-dotenv` 套件，以便從 `.env` 檔案將環境變數載入到您的 Python 應用程式中。使用 `pip` 進行安裝：

   ```bash
   pip install python-dotenv
   ```

6. **在您的 Python 指令碼中載入環境變數**：在您的 Python 指令碼中，使用 `python-dotenv` 從 `.env` 檔案載入變數：

   ```python
   from dotenv import load_dotenv
   import os

   # 從 .env 檔案載入環境變數
   load_dotenv()

   # 存取 GITHUB_TOKEN 變數
   github_token = os.getenv("GITHUB_TOKEN")

   print(github_token)
   ```

就是這樣！您已建立 `.env` 檔案、新增您的 GitHub token 並將其載入到您的 Python 應用程式中。

## 如何在您的電腦上本機執行

若要在本機執行程式碼，您需要安裝 [Python](https://www.python.org/downloads/?WT.mc_id=academic-105485-koreyst)。

然後，複製儲存庫：

```shell
git clone https://github.com/microsoft/generative-ai-for-beginners
cd generative-ai-for-beginners
```

一切設定就緒後，您就可以開始了！

## 選用步驟

### 安裝 Miniconda

[Miniconda](https://conda.io/en/latest/miniconda.html?WT.mc_id=academic-105485-koreyst) 是一個輕量級的安裝程式，用於安裝 [Conda](https://docs.conda.io/en/latest?WT.mc_id=academic-105485-koreyst)、Python 和一些套件。

Conda 是一個套件管理器，可以輕鬆建立和切換不同的 Python [**虛擬環境**](https://docs.python.org/3/tutorial/venv.html?WT.mc_id=academic-105485-koreyst) 和套件。在安裝 `pip` 無法提供的套件時，它也很有用。

請遵循 [Miniconda 安裝指南](https://docs.anaconda.com/free/miniconda/#quick-command-line-install?WT.mc_id=academic-105485-koreyst) 進行設定。

安裝 Miniconda 後，如果尚未複製[儲存庫](https://github.com/microsoft/generative-ai-for-beginners/fork?WT.mc_id=academic-105485-koreyst)，請複製它。

接下來，建立一個虛擬環境。使用 Conda，建立一個新的環境檔案 (_environment.yml_)。如果您正在使用 Codespaces，請將此檔案放在 `.devcontainer` 目錄中，作為 `.devcontainer/environment.yml`。

將以下程式碼片段新增至您的環境檔案：

```yml
name: <environment-name>
channels:
  - defaults
  - microsoft
dependencies:
  - python=<python-version>
  - openai
  - python-dotenv
  - pip
  - pip:
      - azure-ai-ml
```

如果您在使用 conda 時遇到錯誤，可以在終端機中使用此指令手動安裝 Microsoft AI 函式庫：

```
conda install -c microsoft azure-ai-ml
```

環境檔案列出了所需的相依性。`<environment-name>` 是您要為 Conda 環境指定的名稱，而 `<python-version>` 是您要使用的 Python 版本 (例如，`3` 代表最新的主要版本)。

準備就緒後，在您的終端機中執行這些指令來建立您的 Conda 環境：

```bash
conda env create --name ai4beg --file .devcontainer/environment.yml # .devcontainer 子路徑僅適用於 Codespace 設定
conda activate ai4beg
```

如果您遇到問題，請參閱 [Conda 環境指南](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html?WT.mc_id=academic-105485-koreyst)。

### 使用 Visual Studio Code 搭配 Python 支援擴充功能

我們建議在本課程中使用 [Visual Studio Code (VS Code)](https://code.visualstudio.com/?WT.mc_id=academic-105485-koreyst) 搭配 [Python 擴充功能](https://marketplace.visualstudio.com/items?itemName=ms-python.python&WT.mc_id=academic-105485-koreyst)。這是一個建議，而非嚴格要求。

> **注意**：在 VS Code 中開啟課程儲存庫可讓您在容器內設定專案，這要歸功於儲存庫中的特殊 [`.devcontainer`](https://code.visualstudio.com/docs/devcontainers/containers?itemName=ms-python.python&WT.mc_id=academic-105485-koreyst) 資料夾。稍後會詳細介紹。

> **注意**：複製並在 VS Code 中開啟儲存庫後，它會提示您安裝 Python 擴充功能。

> **注意**：如果 VS Code 建議在容器中重新開啟儲存庫，如果您想使用本機 Python 安裝，請拒絕。

### 在瀏覽器中使用 Jupyter

您也可以在瀏覽器中使用 [Jupyter](https://jupyter.org?WT.mc_id=academic-105485-koreyst) 來處理專案。傳統的 Jupyter 和 [Jupyter Hub](https://jupyter.org/hub?WT.mc_id=academic-105485-koreyst) 都提供流暢的開發體驗，具有自動完成和語法醒目提示等功能。

若要在本機啟動 Jupyter，請開啟您的終端機，導覽至課程目錄，然後執行：

```bash
jupyter notebook
```

或

```bash
jupyterhub
```

這將啟動一個 Jupyter 執行個體，存取它的 URL 將顯示在終端機中。

一旦您開啟 URL，您將看到課程大綱，並可以開啟任何 `*.ipynb` 檔案，例如 `08-building-search-applications/python/oai-solution.ipynb`。

### 在容器中執行

除了在您的電腦或 Codespace 上設定所有內容之外，您還可以使用[容器](../../../00-course-setup/<https:/en.wikipedia.org/wiki/Containerization_(computing)?WT.mc_id=academic-105485-koreyst>)。儲存庫中的 `.devcontainer` 資料夾允許 VS Code 在容器內設定專案。

在 Codespaces 之外，這需要安裝 Docker 和一些設定，因此我們僅在您有使用容器的經驗時才建議這樣做。

在 GitHub Codespaces 中保護您的 API 金鑰安全的最佳方法之一是使用 Codespace Secrets。請遵循 [Codespaces 密鑰管理](https://docs.github.com/en/codespaces/managing-your-codespaces/managing-secrets-for-your-codespaces?WT.mc_id=academic-105485-koreyst) 指南以了解更多資訊。

## 課程與技術要求

本課程包括 6 堂概念課程和 6 堂程式設計課程。

在程式設計課程中，我們使用 Azure OpenAI 服務。您需要存取 Azure OpenAI 和 API 金鑰才能執行程式碼。您可以透過[填寫此申請表](https://azure.microsoft.com/products/ai-services/openai-service?WT.mc_id=academic-105485-koreyst)來申請存取權限。

在等待您的申請期間，每堂程式設計課程也包含一個 `README.md` 檔案，您可以在其中檢視程式碼和輸出。

## 首次使用 Azure OpenAI 服務

如果您是 Azure OpenAI 的新手，請遵循本指南，了解如何[建立和部署 Azure OpenAI 服務資源](https://learn.microsoft.com/azure/ai-services/openai/how-to/create-resource?pivots=web-portal&WT.mc_id=academic-105485-koreyst)。

## 首次使用 OpenAI API

如果您是 OpenAI API 的新手，請遵循本指南，了解如何[建立和使用介面](https://platform.openai.com/docs/quickstart?context=pythont&WT.mc_id=academic-105485-koreyst)。

## 認識其他學習者

我們在官方的 [AI 社群 Discord 伺服器](https://aka.ms/genai-discord?WT.mc_id=academic-105485-koreyst) 中建立了頻道，以與其他學習者聯繫。這是與企業家、開發人員、學生以及任何希望在生成式 AI 領域取得進步的人建立聯繫的好方法。

[![加入 discord 頻道](https://dcbadge.limes.pink/api/server/ByRwuEEgH4)](https://aka.ms/genai-discord?WT.mc_id=academic-105485-koreyst)

專案團隊也將在此 Discord 上活躍，以支援學習者。

## 貢獻

本課程為開源課程。如果您發現需要改進或問題的地方，請建立 [Pull Request](https://github.com/microsoft/generative-ai-for-beginners/pulls?WT.mc_id=academic-105485-koreyst) 或開啟 [GitHub issue](https://github.com/microsoft/generative-ai-for-beginners/issues?WT.mc_id=academic-105485-koreyst)。

專案團隊會追蹤所有貢獻。為開源做出貢獻是在生成式 AI 領域建立職涯的絕佳方式。

大多數貢獻都要求同意一份貢獻者授權合約 (CLA)，確認您有權授予我們使用您貢獻的權限。如需詳細資訊，請造訪 [CLA，貢獻者授權合約網站](https://cla.microsoft.com?WT.mc_id=academic-105485-koreyst)。

重要提示：在本儲存庫中翻譯文字時，請避免使用機器翻譯。我們透過社群驗證翻譯，因此請僅在您精通的語言中自願進行翻譯。

當您提交提取請求時，CLA-bot 將檢查您是否需要簽署 CLA，並將相應地標記或註解。只需按照機器人的說明操作即可。您只需在所有使用我們 CLA 的儲存庫中執行此操作一次。

本專案遵循 [Microsoft 開源行為準則](https://opensource.microsoft.com/codeofconduct/?WT.mc_id=academic-105485-koreyst)。如需詳細資訊，請閱讀行為準則常見問題集或聯絡 [電子郵件 opencode](opencode@microsoft.com) 提出問題或意見。

## 讓我們開始吧

現在您已完成設定步驟，讓我們開始[介紹生成式 AI 和 LLM](../01-introduction-to-genai/README.md?WT.mc_id=academic-105485-koreyst)。

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。