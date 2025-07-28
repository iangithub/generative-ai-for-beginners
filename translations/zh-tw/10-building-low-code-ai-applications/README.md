<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f5ff3b6204a695a117d6f452403c95f7",
  "translation_date": "2025-07-09T13:37:40+00:00",
  "source_file": "10-building-low-code-ai-applications/README.md",
  "language_code": "zh-tw"
}
-->
# 建置低程式碼 AI 應用程式

[![建置低程式碼 AI 應用程式](../../../translated_images/10-lesson-banner.a01ac8fe3fd86310c2e4065c0b3c584879f33b8ce797311821a636992f8a5b2f.en.png)](https://aka.ms/gen-ai-lesson10-gh?WT.mc_id=academic-105485-koreyst)

> _（點擊上方圖片觀看本課影片）_

## 簡介

現在我們已經學會了如何建置影像生成應用程式，接下來讓我們談談低程式碼。生成式 AI 可以應用在許多領域，包括低程式碼，但低程式碼到底是什麼？我們又該如何將 AI 整合到其中呢？

由於低程式碼開發平台，傳統開發人員和非開發人員建置應用程式和解決方案變得更加容易。這些平台透過提供視覺化開發環境，讓您可以拖放元件，從而以極少或無需編碼的方式建立應用程式和解決方案。這讓您可以更快、以更少的資源建置應用程式和解決方案。在本課中，我們將探討如何使用低程式碼以及如何使用 Power Platform 透過 AI 增強低程式碼開發。

Power Platform 讓組織有機會透過直觀的低程式碼或無程式碼環境，賦予其團隊建置自己解決方案的能力。這個環境簡化了建置解決方案的過程。透過 Power Platform，解決方案可以在數天或數週內建立，而不是數月或數年。Power Platform 包含五個主要產品：Power Apps、Power Automate、Power BI、Power Pages 和 Copilot Studio。

本課涵蓋：

- Power Platform 中生成式 AI 簡介
- Copilot 簡介及使用方法
- 使用生成式 AI 在 Power Platform 中建置應用程式和流程
- 透過 AI Builder 了解 Power Platform 中的 AI 模型

## 學習目標

在本課結束時，您將能夠：

- 了解 Copilot 在 Power Platform 中的運作方式。
- 為我們的教育新創公司建置一個學生作業追蹤應用程式。
- 建置一個使用 AI 從發票中提取資訊的發票處理流程。
- 在使用「使用 GPT AI 模型建立文字」時應用最佳實務。

您將在本課中使用的工具和技術是：

- **Power Apps**，用於學生作業追蹤應用程式，它提供了一個低程式碼開發環境，用於建置追蹤、管理和與資料互動的應用程式。
- **Dataverse**，用於儲存學生作業追蹤應用程式的資料，它提供了一個低程式碼資料平台，用於儲存應用程式的資料。
- **Power Automate**，用於發票處理流程，它提供了一個低程式碼環境，用於建置自動化發票處理的工作流程。
- **AI Builder**，用於發票處理 AI 模型，您將使用預建的 AI 模型來處理我們新創公司的發票。

## Power Platform 中的生成式 AI

透過生成式 AI 增強低程式碼開發和應用程式是 Power Platform 的一個關鍵重點。目標是讓每個人都能建置由 AI 驅動的應用程式、網站、儀表板，並透過 AI 自動化流程，而「無需任何資料科學專業知識」。這是透過將生成式 AI 整合到 Power Platform 中的低程式碼開發體驗中，透過 Copilot 和 AI Builder 來實現的。

### 這是如何運作的？

Copilot 是一個 AI 助理，可協助您透過一系列使用自然語言的對話步驟來描述您的需求，從而建置 Power Platform 解決方案。例如，您可以告訴您的 AI 助理您的應用程式將使用哪些欄位，它將建立應用程式和底層資料模型。或者您可以指定如何在 Power Automate 中設定流程。

您還可以在應用程式畫面中使用 Copilot 驅動的功能，透過對話式互動協助使用者發現見解。

AI Builder 是 Power Platform 中的低程式碼 AI 功能，可讓您使用 AI 模型來自動化流程和預測結果。透過 AI Builder，您可以將 AI 新增到您的應用程式和流程中，這些應用程式和流程可連接到 Dataverse 或各種雲端資料來源，例如 SharePoint、OneDrive 或 Azure 中的資料。

Copilot 可用於所有 Power Platform 產品：Power Apps、Power Automate、Power BI、Power Pages 和 Power Virtual Agents。AI Builder 可用於 Power Apps 和 Power Automate。在本課中，我們將重點介紹如何在 Power Apps 和 Power Automate 中使用 Copilot 和 AI Builder，為我們的新創公司建置解決方案。

### Power Apps 中的 Copilot

Power Apps 是 Power Platform 的一部分，它提供了一個低程式碼環境，用於建置追蹤、管理和與資料互動的應用程式。它是一套應用程式開發服務，具有可擴展的資料平台，並能夠連接到雲端服務和內部部署資料。Power Apps 讓您可以建置在瀏覽器、平板電腦和手機上執行的應用程式，並可以與同事共享。它透過簡單的介面簡化了應用程式開發，讓任何業務使用者或專業開發人員都可以建立自訂應用程式。透過 Copilot，生成式 AI 進一步增強了應用程式開發體驗。

Power Apps 中的 Copilot AI 助理可讓您描述您需要的應用程式類型以及您希望它追蹤、收集或顯示的資訊。然後 Copilot 會根據您的描述產生一個響應式畫布應用程式。您可以自訂應用程式以符合您的需求。AI Copilot 還會建立並建議一個 Dataverse 表格，其中包含儲存您的資料所需的欄位和一些範例資料。我們將在本課稍後介紹 Dataverse 是什麼以及如何在 Power Apps 中使用它。您可以透過對話式步驟使用 AI Copilot 助理來自訂表格。此功能可直接從 Power Apps 首頁畫面取得。

### Power Automate 中的 Copilot

Power Automate 是 Power Platform 的一部分，它讓使用者可以在應用程式和服務之間建立自動化工作流程。它有助於自動化重複的業務任務，例如通訊、資料收集和核准流程。其簡單的介面讓所有技能水平的使用者——從初學者到經驗豐富的開發人員——都能自動化工作任務。透過 Copilot，工作流程開發體驗也透過生成式 AI 得到了增強。

Power Automate 中的 Copilot AI 助理可讓您描述您需要的流程類型以及您希望它執行的動作。然後 Copilot 會根據您的描述產生一個流程。您可以自訂流程以符合您的需求。AI Copilot 還會建議自動化您的任務所需的動作。我們將在本課稍後介紹流程是什麼以及如何在 Power Automate 中使用它們。您可以透過對話式步驟使用 AI Copilot 助理來自訂動作。此功能可從 Power Automate 首頁畫面取得。

## 作業：使用 Copilot 管理我們新創公司的學生作業和發票

我們的新創公司提供線上課程給學生。它發展迅速，現在正努力跟上需求。新創公司聘請您擔任 Power Platform 開發人員，以建置一個低程式碼解決方案，協助管理學生作業和發票。該解決方案應透過應用程式協助追蹤和管理學生作業，並透過工作流程自動化發票處理。您已被要求使用生成式 AI 來開發此解決方案。

開始使用 Copilot 時，您可以使用 [Power Platform Copilot 提示庫](https://github.com/pnp/powerplatform-prompts?WT.mc_id=academic-109639-somelezediko) 來獲取提示的想法。此程式庫包含您可以用來使用 Copilot 建置應用程式和流程的提示。它也是學習如何向 Copilot 描述您的需求的好資源。

### 為我們的新創公司建置一個學生作業追蹤應用程式

我們新創公司的教育工作者在追蹤學生作業方面遇到了困難。他們一直使用試算表，但隨著學生人數的增加，管理變得困難。他們要求您建置一個應用程式來協助追蹤和管理學生作業。該應用程式應允許他們新增作業、檢視作業、更新作業和刪除作業。它還應讓教育工作者和學生查看哪些作業已評分，哪些尚未評分。

您將透過以下步驟使用 Power Apps 中的 Copilot 建置應用程式：

1. 前往 [Power Apps](https://make.powerapps.com?WT.mc_id=academic-105485-koreyst) 首頁畫面。

2. 使用首頁畫面上的文字方塊來描述您要建置的應用程式。例如，**_我想要建置一個應用程式來追蹤和管理學生作業_**。按一下 **傳送** 按鈕將提示傳送給 AI Copilot。

![描述您要建置的應用程式](../../../translated_images/copilot-chat-prompt-powerapps.84250f341d060830a296b68512e6b3b3aa3a4559f4f1c2d7bafeba8ad3fcd17a.en.png)

3. AI Copilot 將建議一個 Dataverse 表格，其中包含儲存您的資料所需的欄位和一些範例資料。您可以透過對話式步驟使用 AI Copilot 助理來自訂表格以符合您的需求。

   > **重要**：Dataverse 是 Power Platform 的底層資料平台。它是一個低程式碼資料平台，用於儲存應用程式資料。它是一個完全受管理的服務，可將資料安全地儲存在 Microsoft Cloud 中，並在您的 Power Platform 環境中佈建。它包含內建的資料治理功能，例如資料分類、資料沿襲、細粒度存取控制等等。在此處了解更多關於 Dataverse 的資訊：[這裡](https://docs.microsoft.com/powerapps/maker/data-platform/data-platform-intro?WT.mc_id=academic-109639-somelezediko)。

   ![新表格中建議的欄位](../../../translated_images/copilot-dataverse-table-powerapps.f4cc07b5d5f9327bd3783dd288debb2a959ce3320107512e235137aebd8a1a4c.en.png)

4. 教育工作者希望向已提交作業的學生發送電子郵件，以讓他們了解進度。您可以使用 Copilot 向表格新增一個新欄位來儲存學生電子郵件。例如，使用提示：**_我想要新增一個欄位來儲存學生電子郵件_**。按一下 **傳送** 將提示傳送給 AI Copilot。

![新增欄位](../../../translated_images/copilot-new-column.35e15ff21acaf2745965d427b130f2be772f0484835b44fe074d496b1a455f2a.en.png)

5. AI Copilot 將建立新欄位，然後您可以根據需要自訂它。

6. 完成表格後，按一下 **建立應用程式** 以產生應用程式。

7. AI Copilot 將根據您的描述建立一個響應式畫布應用程式。您可以自訂應用程式以符合您的需求。

8. 若要允許教育工作者向學生發送電子郵件，請使用 Copilot 向應用程式新增一個新畫面。例如，使用提示：**_我想要新增一個畫面來向學生發送電子郵件_**。按一下 **傳送** 將提示傳送給 AI Copilot。

![透過提示指令新增畫面](../../../translated_images/copilot-new-screen.2e0bef7132a173928bc621780b39799e03982d315cb5a9ff75a34b08054641d4.en.png)

9. AI Copilot 將產生新畫面，然後您可以根據需要自訂它。

10. 完成應用程式後，按一下 **儲存** 以儲存它。

11. 若要與教育工作者共享應用程式，請按一下 **共享**，然後再次按一下 **共享**。輸入他們的電子郵件地址以共享應用程式。

> **您的作業**：您建置的應用程式是一個很好的開始，但可以改進。目前，教育工作者只能透過手動輸入電子郵件地址來向學生發送電子郵件。您可以使用 Copilot 建置一個自動化，在學生提交作業時自動向他們發送電子郵件嗎？提示：使用正確的提示，您可以在 Power Automate 中使用 Copilot 來建置此功能。

### 為我們的新創公司建置一個發票資訊表

我們新創公司的財務團隊在追蹤發票方面遇到了困難。他們一直使用試算表，但隨著發票數量的增加，管理變得困難。他們要求您建置一個表格來儲存、追蹤和管理發票資訊。此表格將用於建置一個自動化，該自動化將提取所有發票資訊並將其儲存在表格中。該表格還應讓財務團隊查看哪些發票已付款，哪些尚未付款。

Power Platform 包含一個名為 Dataverse 的底層資料平台，可讓您儲存應用程式和解決方案的資料。Dataverse 提供了一個低程式碼資料平台，用於儲存應用程式資料。它是一個完全受管理的服務，可將資料安全地儲存在 Microsoft Cloud 中，並在您的 Power Platform 環境中佈建。它包含內建的資料治理功能，例如資料分類、資料沿襲、細粒度存取控制等等。在此處了解更多關於 Dataverse 的資訊：[這裡](https://docs.microsoft.com/powerapps/maker/data-platform/data-platform-intro?WT.mc_id=academic-109639-somelezediko)。

為什麼要為我們的新創公司使用 Dataverse？Dataverse 中的標準和自訂表格為您的資料提供了安全、基於雲端的儲存選項。表格可讓您儲存不同類型的資料，類似於在單一 Excel 工作簿中使用多個工作表。您可以使用表格來儲存特定於您的組織或業務需求的資料。我們的新創公司將從使用 Dataverse 中獲得的一些好處包括但不限於：
- **易於管理**：中繼資料和資料都儲存在雲端，因此您無需擔心它們的儲存或管理方式。您可以專注於建置您的應用程式和解決方案。

- **安全**：Dataverse 為您的資料提供安全、基於雲端的儲存選項。您可以使用基於角色的安全性來控制誰可以存取您的表格資料以及他們如何存取它。

- **豐富的中繼資料**：資料類型和關係直接在 Power Apps 中使用。

- **邏輯和驗證**：您可以應用業務規則、計算欄位和驗證規則來強制執行業務邏輯並確保資料準確性。

現在您已經了解 Dataverse 是什麼以及為何應該使用它，讓我們看看如何使用 Copilot 在 Dataverse 中建立一個符合我們財務團隊需求的表格。

> **注意**：您將在下一節中使用此表格來建置一個自動化，該自動化將提取所有發票資訊並將其儲存在表格中。

若要使用 Copilot 在 Dataverse 中建立表格，請遵循以下步驟：

1. 前往 [Power Apps](https://make.powerapps.com?WT.mc_id=academic-105485-koreyst) 首頁畫面。

2. 在左側導覽列中，選取 **表格**，然後按一下 **描述新表格**。

![選取新表格](../../../translated_images/describe-new-table.0792373eb757281e3c5f542f84cad3b5208bfe0e5c4a7786dd2bd31aa848a23c.en.png)

3. 在 **描述新表格** 畫面中，使用文字方塊來描述您要建立的表格。例如，**_我想要建立一個表格來儲存發票資訊_**。按一下 **傳送** 將提示提交給 AI Copilot。

![描述表格](../../../translated_images/copilot-chat-prompt-dataverse.feb2f81e5872b9d2b05d45d11bb6830e0f2ef6a2d4742413bc9a1e50a45bbb89.en.png)

4. AI Copilot 將建議一個 Dataverse 表格，其中包含儲存您要追蹤的資料所需的欄位，以及一些範例資料。您可以透過對話式步驟使用 AI Copilot 助理進一步自訂表格。

![建議的 Dataverse 表格](../../../translated_images/copilot-dataverse-table.b3bc936091324d9db1e943d640df1c7a7df598e66d30f5b8a2999048e26a5073.en.png)

5. 財務團隊希望向供應商發送電子郵件，以讓他們了解發票的目前狀態。您可以使用 Copilot 向表格新增一個新欄位來儲存供應商的電子郵件。例如，使用提示：**_我想要新增一個欄位來儲存供應商電子郵件_**。按一下 **傳送** 將提示提交給 AI Copilot。

6. AI Copilot 將產生新欄位，然後您可以根據需要自訂它。

7. 完成表格設定後，按一下 **建立** 以建立它。

## Power Platform 中的 AI 模型與 AI Builder

AI Builder 是 Power Platform 中的低程式碼 AI 功能，可讓您使用 AI 模型來自動化流程和預測結果。透過 AI Builder，您可以將 AI 引入您的應用程式和流程中，這些應用程式和流程可連接到 Dataverse 或各種雲端資料來源，例如 SharePoint、OneDrive 或 Azure 中的資料。

## 預建 AI 模型與自訂 AI 模型

AI Builder 提供兩種 AI 模型：預建 AI 模型和自訂 AI 模型。預建 AI 模型是 Microsoft 訓練並在 Power Platform 中提供的即用型模型。它們可協助您為應用程式和流程新增智慧，而無需收集資料或建置、訓練和發布自己的模型。您可以使用這些模型來自動化流程和預測結果。

Power Platform 中提供的一些預建 AI 模型包括：

- **關鍵詞組提取**：從文字中提取關鍵詞組。
- **語言偵測**：偵測文字的語言。
- **情感分析**：識別文字中的正面、負面、中性或混合情感。
- **名片讀取器**：從名片中提取資訊。
- **文字辨識**：從影像中提取文字。
- **物件偵測**：從影像中偵測和提取物件。
- **文件處理**：從表單中提取資訊。
- **發票處理**：從發票中提取資訊。

透過自訂 AI 模型，您可以將自己的模型引入 AI Builder，使其功能與任何 AI Builder 自訂模型一樣，讓您可以使用自己的資料進行訓練。這些模型可以在 Power Apps 和 Power Automate 中自動化流程和預測結果。使用自己的模型時存在一些限制。在此處了解更多關於這些[限制](https://learn.microsoft.com/ai-builder/byo-model#limitations?WT.mc_id=academic-105485-koreyst)的資訊。

![AI builder 模型](../../../translated_images/ai-builder-models.8069423b84cfc47f6bb989bc3cd0584b5b2471c80fad80bf504d356928a08c9c.en.png)

## 作業 #2 - 為我們的新創公司建置一個發票處理流程

財務團隊一直在努力處理發票。他們一直使用試算表來追蹤發票，但隨著發票數量的增加，管理變得困難。他們要求您建置一個工作流程，協助他們使用 AI 處理發票。該工作流程應從發票中提取資訊並將其儲存在 Dataverse 表格中。它還應向財務團隊發送一封包含提取資訊的電子郵件。

現在您已經了解 AI Builder 是什麼以及為何應該使用它，讓我們看看如何使用 AI Builder 中我們之前介紹的發票處理 AI 模型，來建置一個協助財務團隊處理發票的工作流程。

若要使用 AI Builder 中的發票處理 AI 模型建置一個協助財務團隊處理發票的工作流程，請遵循以下步驟：

1. 前往 [Power Automate](https://make.powerautomate.com?WT.mc_id=academic-105485-koreyst) 首頁畫面。

2. 使用首頁畫面上的文字方塊來描述您要建置的工作流程。例如，**_當發票到達我的信箱時處理它_**。按一下 **傳送** 將提示提交給 AI Copilot。

   ![Copilot power automate](../../../translated_images/copilot-chat-prompt-powerautomate.f377e478cc8412de4394fab09e5b72f97b3fc9312526b516ded426102f51c30d.en.png)

3. AI Copilot 將建議自動化您的任務所需的動作。按一下 **下一步** 以繼續執行步驟。

4. 在下一個畫面中，Power Automate 將要求您設定流程所需的連線。完成後，按一下 **建立流程** 以建立它。

5. AI Copilot 將產生一個流程，您可以自訂它以符合您的需求。

6. 更新流程的觸發器，並將 **資料夾** 設定為儲存發票的位置。例如，將其設定為 **收件匣**。按一下 **顯示進階選項** 並將 **僅限附件** 設定為 **是**。這可確保流程僅在資料夾中收到帶有附件的電子郵件時執行。

7. 從流程中移除這些動作：**HTML 到文字**、**撰寫**、**撰寫 2**、**撰寫 3** 和 **撰寫 4**，因為您不會使用它們。

8. 同時從流程中移除 **條件** 動作。流程應如下所示：

   ![power automate，移除動作](../../../translated_images/powerautomate-remove-actions.7216392fe684ceba4b73c6383edd1cc5e7ded11afd0ca812052a11487d049ef8.en.png)

9. 按一下 **新增動作**，搜尋 **Dataverse**，然後選取 **新增列**。

10. 在 **從發票中提取資訊** 動作中，更新 **發票檔案** 以指向電子郵件中的 **附件內容**。這可確保流程從發票附件中提取資訊。

11. 選取您之前建立的 **表格**，例如 **發票資訊** 表格。使用前一個動作的動態內容來填寫這些欄位：

    - ID
    - 金額
    - 日期
    - 名稱
    - 狀態 – 將 **狀態** 設定為 **待處理**。
    - 供應商電子郵件 – 使用 **當新電子郵件到達時** 觸發器中的 **寄件者** 動態內容。

    ![power automate 新增列](../../../translated_images/powerautomate-add-row.5edce45e5dd3d51e5152688dc140ad43e1423e7a9fef9a206f82a7965ea68d73.en.png)

12. 完成後，按一下 **儲存** 以儲存流程。您可以透過向您在觸發器中指定的資料夾發送帶有發票的電子郵件來測試它。

> **您的作業**：您剛剛建置的流程是一個很好的開始。現在思考一下如何建置一個自動化，讓財務團隊可以向供應商發送電子郵件，以讓他們了解發票的目前狀態。提示：當發票狀態變更時，流程應該執行。

## 在 Power Automate 中使用文字生成 AI 模型

AI Builder 中的「使用 GPT AI 模型建立文字」可讓您根據提示產生文字，並由 Microsoft Azure OpenAI 服務提供支援。此功能可讓您將 GPT (生成式預訓練轉換器) 技術整合到您的應用程式和流程中，以建置各種自動化工作流程和富有洞察力的應用程式。

GPT 模型經過大量資料的訓練，使其能夠在給定提示時產生與人類語言非常相似的文字。當與工作流程自動化結合時，像 GPT 這樣的 AI 模型可以簡化和自動化許多任務。

例如，您可以建置自動產生電子郵件草稿、產品描述等用途的文字的流程。您還可以使用該模型為聊天機器人、客戶服務工具等應用程式產生文字，以協助代理人有效率地回應客戶查詢。

![建立提示](../../../translated_images/create-prompt-gpt.69d429300c2e870a12ec95556cda9bacf6a173e452cdca02973c90df5f705cee.en.png)

若要了解如何在 Power Automate 中使用此 AI 模型，請查看 [使用 AI Builder 和 GPT 新增智慧](https://learn.microsoft.com/training/modules/ai-builder-text-generation/?WT.mc_id=academic-109639-somelezediko) 模組。

## 做得好！繼續學習

完成本課後，請探索我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 技能！

接下來，前往第 11 課，我們將探討如何[將生成式 AI 與函式呼叫整合](../11-integrating-with-function-calling/README.md?WT.mc_id=academic-105485-koreyst)！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。