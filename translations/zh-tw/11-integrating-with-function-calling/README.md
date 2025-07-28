<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "77a48a201447be19aa7560706d6f93a0",
  "translation_date": "2025-07-09T14:21:05+00:00",
  "source_file": "11-integrating-with-function-calling/README.md",
  "language_code": "zh-tw"
}
-->
# 整合函式呼叫

[![整合函式呼叫](../../../translated_images/11-lesson-banner.d78860d3e1f041e2c3426b1c052e1590738d2978db584a08efe1efbca299ed82.en.png)](https://aka.ms/gen-ai-lesson11-gh?WT.mc_id=academic-105485-koreyst)

您在前面的課程中學到了不少東西。然而，仍有改進的空間。我們可以專注的一些領域包括如何獲得更一致的回應格式，以便更容易地處理下游回應。此外，我們可能希望從其他來源新增資料，以進一步豐富我們的應用程式。

這些是本章旨在解決的挑戰。

## 簡介

本課將涵蓋：

- 什麼是函式呼叫及其使用案例。
- 如何使用 Azure OpenAI 建立函式呼叫。
- 如何將函式呼叫整合到應用程式中。

## 學習目標

在本課結束時，您將能夠：

- 解釋函式呼叫為何有用。
- 使用 Azure OpenAI 服務設定函式呼叫。
- 設計符合應用程式需求的有效函式呼叫。

## 情境：使用函式改進我們的聊天機器人

在本課中，我們希望為我們的教育新創公司建置一個功能，讓使用者可以使用聊天機器人來尋找技術課程。我們將推薦符合他們技能水平、目前角色和技術興趣的課程。

為了完成此情境，我們將結合使用：

- `Azure OpenAI` 以為使用者建立聊天體驗。
- `Microsoft Learn Catalog API` 以協助使用者根據其請求尋找課程。
- `函式呼叫` 以接收使用者的查詢並將其傳送至發出 API 請求的函式。

首先，讓我們了解為何要使用函式呼叫：

## 為何要函式呼叫

在函式呼叫之前，LLM 的回應是非結構化且不一致的。開發人員必須編寫複雜的驗證程式碼來處理回應的每個變體。使用者無法獲得諸如「斯德哥爾摩目前天氣如何？」之類問題的答案，因為模型僅限於其訓練資料。

函式呼叫是 Azure OpenAI 服務的一項功能，旨在克服這些限制：

- **一致的回應格式**。透過控制回應格式，我們可以更輕鬆地將回應整合到下游的其他系統中。
- **外部資料**。它允許在聊天上下文中使用來自應用程式其他部分的資料。

## 透過情境說明問題

> 如果您想執行以下情境，我們建議使用[隨附的筆記本](../../../11-integrating-with-function-calling/python/aoai-assignment.ipynb)。您也可以只閱讀我們說明函式可以幫助解決的問題。

讓我們看一個突顯回應格式問題的範例：

假設我們想建立一個學生資料庫，以便我們可以建議正確的課程。以下是兩個學生描述，它們在所包含的資料方面非常相似。

1. 建立與我們的 Azure OpenAI 資源的連線：

   ```python
   import os
   import json
   from openai import AzureOpenAI
   from dotenv import load_dotenv
   load_dotenv()

   client = AzureOpenAI(
   api_key=os.environ['AZURE_OPENAI_API_KEY'],  # 這也是預設值，可以省略
   api_version = "2023-07-01-preview"
   )

   deployment=os.environ['AZURE_OPENAI_DEPLOYMENT']
   ```

   以下是一些設定我們與 Azure OpenAI 連線的 Python 程式碼，其中我們設定了 `api_type`、`api_base`、`api_version` 和 `api_key`。

2. 使用變數 `student_1_description` 和 `student_2_description` 建立兩個學生描述。

   ```python
   student_1_description="Emily Johnson 是杜克大學電腦科學系二年級學生。她的 GPA 為 3.7。Emily 是大學西洋棋社和辯論隊的活躍成員。她希望畢業後從事軟體工程師的職業。"

   student_2_description = "Michael Lee 是史丹佛大學電腦科學系二年級學生。他的 GPA 為 3.8。Michael 以其程式設計技能而聞名，並且是大學機器人社的活躍成員。他希望在完成學業後從事人工智慧的職業。"
   ```

   我們希望將這些學生描述傳送給 LLM 以解析資料。這些資料稍後可以用於我們的應用程式、傳送給 API 或儲存在資料庫中。

3. 讓我們建立兩個相同的提示，指示 LLM 我們想要什麼資訊：

   ```python
prompt1 = f'''
請從給定的文字中提取以下資訊並以 JSON 物件形式傳回：

姓名
主修
學校
成績
社團

這是要提取資訊的文字主體：
{student_1_description}
'''

prompt2 = f'''
請從給定的文字中提取以下資訊並以 JSON 物件形式傳回：

姓名
主修
學校
成績
社團

這是要提取資訊的文字主體：
{student_2_description}
'''
   ```

   這些提示會告訴 LLM 提取資訊並以 JSON 格式傳回回應。

4. 設定提示並連接到 Azure OpenAI 後，我們使用 `openai.ChatCompletion` 將提示傳送給 LLM。我們將提示儲存在 `messages` 變數中，並將 `user` 角色指派給它，以模擬傳送給聊天機器人的使用者訊息。

   ```python
   # 來自提示一的回應
   openai_response1 = client.chat.completions.create(
   model=deployment,
   messages = [{'role': 'user', 'content': prompt1}]
   )
   openai_response1.choices[0].message.content

   # 來自提示二的回應
   openai_response2 = client.chat.completions.create(
   model=deployment,
   messages = [{'role': 'user', 'content': prompt2}]
   )
   openai_response2.choices[0].message.content
   ```

現在我們可以將兩個請求都傳送給 LLM，並透過存取 `openai_response1['choices'][0]['message']['content']` 來檢查回應。

5. 最後，我們透過呼叫 `json.loads` 將回應轉換為 JSON 格式：

   ```python
   # 將回應載入為 JSON 物件
   json_response1 = json.loads(openai_response1.choices[0].message.content)
   json_response1
   ```

   回應 1：

   ```json
   {
     "name": "Emily Johnson",
     "major": "computer science",
     "school": "Duke University",
     "grades": "3.7",
     "club": "Chess Club"
   }
   ```

   回應 2：

   ```json
   {
     "name": "Michael Lee",
     "major": "computer science",
     "school": "Stanford University",
     "grades": "3.8 GPA",
     "club": "Robotics Club"
   }
   ```

   即使提示相同且描述相似，`Grades` 屬性的格式也不同——有時是 `3.7`，有時是 `3.7 GPA`。

   發生這種情況是因為 LLM 從提示中獲取非結構化資料並傳回非結構化資料。我們需要結構化格式，以便在儲存或使用此資料時知道預期會得到什麼。

那麼我們如何解決格式問題呢？透過使用函式呼叫，我們可以確保我們收到結構化資料。當使用函式呼叫時，LLM 實際上不會呼叫或執行任何函式。相反，我們為 LLM 建立一個結構，讓它在回應中遵循。然後我們使用這些結構化回應來決定在我們的應用程式中執行哪個函式。

![函式流程](../../../translated_images/Function-Flow.083875364af4f4bb69bd6f6ed94096a836453183a71cf22388f50310ad6404de.en.png)

然後我們可以從函式中取得輸出並將其傳送回 LLM。LLM 將以自然語言回應以回答使用者的查詢。

## 使用函式呼叫的使用案例

函式呼叫可以透過多種方式改進您的應用程式，例如：

- **呼叫外部工具**。聊天機器人擅長回答使用者問題。透過函式呼叫，聊天機器人可以使用使用者訊息來執行任務。例如，學生可能會要求聊天機器人「向我的老師發送電子郵件，說我需要更多關於這個主題的幫助。」這可能會觸發一個函式呼叫，例如 `send_email(to: string, body: string)`。

- **建立 API 或資料庫查詢**。使用者可以用自然語言提問，這些問題會被轉換為格式化的查詢或 API 請求。例如，老師可能會問「哪些學生完成了上次作業？」，這可能會呼叫一個函式，例如 `get_completed(student_name: string, assignment: int, current_status: string)`。

- **建立結構化資料**。使用者可以輸入一段文字或 CSV，並使用 LLM 提取關鍵資訊。例如，學生可以使用一個函式，例如 `get_important_facts(agreement_name: string, date_signed: string, parties_involved: list)`，將維基百科上關於和平協議的文章轉換為 AI 抽認卡。

## 建立您的第一個函式呼叫

建立函式呼叫涉及三個主要步驟：

1. 使用您的函式清單和使用者訊息**呼叫**聊天完成 API。
2. **讀取**模型的響應以決定要採取什麼動作，例如執行函式或 API 呼叫。
3. **再次呼叫**聊天完成 API，並帶上函式的響應，以產生對使用者的回覆。

![LLM 流程](../../../translated_images/LLM-Flow.3285ed8caf4796d7343c02927f52c9d32df59e790f6e440568e2e951f6ffa5fd.en.png)

### 步驟 1 - 建立訊息

第一步是建立使用者訊息。這可以透過取得文字輸入的值來動態指派，或者您可以在此處指派一個值。如果您是第一次使用聊天完成 API，您需要定義訊息的 `role` 和 `content`。

`role` 可以是 `system`（設定規則）、`assistant`（模型）或 `user`（終端使用者）。對於函式呼叫，我們指派 `user` 並提供一個範例問題。

```python
messages= [ {"role": "user", "content": "為初學者學生尋找一個學習 Azure 的好課程。"} ]
```

指派不同的角色可以向 LLM 闡明訊息是來自系統還是使用者，幫助它建立對話歷史記錄。

### 步驟 2 - 建立函式

接下來，我們定義一個函式及其參數。在這裡，我們使用一個名為 `search_courses` 的函式，但您可以建立多個函式。

> **重要**：函式包含在傳送給 LLM 的系統訊息中，並計入您可用的權杖。

下面，我們將函式建立為一個陣列。每個項目都是一個具有 `name`、`description` 和 `parameters` 屬性的函式：

```python
functions = [
   {
      "name":"search_courses",
      "description":"根據提供的參數從搜尋索引中擷取課程",
      "parameters":{
         "type":"object",
         "properties":{
            "role":{
               "type":"string",
               "description":"學習者的角色（即開發人員、資料科學家、學生等）"
            },
            "product":{
               "type":"string",
               "description":"課程涵蓋的產品（即 Azure、Power BI 等）"
            },
            "level":{
               "type":"string",
               "description":"學習者在修讀課程之前的經驗水平（即初級、中級、進階）"
            }
         },
         "required":[
            "role"
         ]
      }
   }
]
```

以下是每個函式屬性的詳細說明：

- `name` - 要呼叫的函式名稱。
- `description` - 函式功能的清晰具體說明。
- `parameters` - 您希望模型在其回應中產生的值及其格式清單。參數陣列包含具有這些屬性的項目：
  1. `type` - 屬性的資料類型。
  2. `properties` - 模型將在其格式化回應中使用的特定值：
      1. `name` - 模型將在其格式化回應中使用的鍵名，例如 `product`。
      2. `type` - 此屬性的資料類型，例如 `string`。
      3. `description` - 屬性的描述。

還有一個可選的 `required` 屬性，它指定了函式呼叫有效必須包含哪些參數。

### 步驟 3 - 進行函式呼叫

定義函式後，我們透過將 `functions` 新增到請求中，例如 `functions=functions`，將其包含在對聊天完成 API 的呼叫中。

您還可以將 `function_call` 設定為 `auto`，這讓 LLM 根據使用者訊息決定要呼叫哪個函式，而不是您自己指定。

以下是一些呼叫 `ChatCompletion.create` 的程式碼，展示了我們如何設定 `functions=functions` 和 `function_call="auto"`，讓 LLM 選擇何時呼叫函式：

```python
response = client.chat.completions.create(model=deployment,
                                        messages=messages,
                                        functions=functions,
                                        function_call="auto")

print(response.choices[0].message)
```

回應現在看起來像這樣：

```json
{
  "role": "assistant",
  "function_call": {
    "name": "search_courses",
    "arguments": "{\n  \"role\": \"student\",\n  \"product\": \"Azure\",\n  \"level\": \"beginner\"\n}"
  }
}
```

在這裡，我們看到函式 `search_courses` 被呼叫，以及其引數，列在 JSON 回應的 `arguments` 屬性中。

LLM 提取了資料以符合函式的引數，這些資料來自聊天完成呼叫的 `messages` 參數中提供的值。以下是 `messages` 值的提醒：

```python
messages= [ {"role": "user", "content": "為初學者學生尋找一個學習 Azure 的好課程。"} ]
```

如您所見，`student`、`Azure` 和 `beginner` 是從 `messages` 中提取出來並用作函式的輸入。以這種方式使用函式是從提示中提取資訊、為 LLM 提供結構並啟用可重複使用功能的好方法。

接下來，讓我們看看如何在我們的應用程式中使用它。

## 將函式呼叫整合到應用程式中

測試 LLM 的格式化回應後，我們可以將其整合到應用程式中。

### 管理流程

若要將此整合到我們的應用程式中，請遵循以下步驟：

1. 首先，呼叫 OpenAI 服務並將訊息儲存在名為 `response_message` 的變數中。

   ```python
   response_message = response.choices[0].message
   ```

2. 現在定義將呼叫 Microsoft Learn API 以取得課程清單的函式：

   ```python
   import requests

   def search_courses(role, product, level):
     url = "https://learn.microsoft.com/api/catalog/"
     params = {
        "role": role,
        "product": product,
        "level": level
     }
     response = requests.get(url, params=params)
     modules = response.json()["modules"]
     results = []
     for module in modules[:5]:
        title = module["title"]
        url = module["url"]
        results.append({"title": title, "url": url})
     return str(results)
   ```

   請注意我們如何建立一個實際的 Python 函式，它對應於 `functions` 變數中定義的函式名稱。我們還進行了實際的外部 API 呼叫以獲取我們需要的資料。在這種情況下，我們查詢 Microsoft Learn API 以搜尋訓練模組。

那麼，我們建立了 `functions` 變數和一個對應的 Python 函式。我們如何告訴 LLM 將它們對應起來，以便呼叫我們的 Python 函式？

1. 若要檢查我們是否需要呼叫 Python 函式，請查看 LLM 回應以查看是否存在 `function_call`，並呼叫指定的函式。以下是執行此檢查的方法：

   ```python
   # 檢查模型是否要呼叫函式
   if response_message.function_call.name:
    print("建議的函式呼叫：")
    print(response_message.function_call.name)
    print()

    # 呼叫函式。
    function_name = response_message.function_call.name

    available_functions = {
            "search_courses": search_courses,
    }
    function_to_call = available_functions[function_name]

    function_args = json.loads(response_message.function_call.arguments)
    function_response = function_to_call(**function_args)

    print("函式呼叫的輸出：")
    print(function_response)
    print(type(function_response))


    # 將助理回應和函式回應新增到訊息中
    messages.append( # 將助理回應新增到訊息中
        {
            "role": response_message.role,
            "function_call": {
                "name": function_name,
                "arguments": response_message.function_call.arguments,
            },
            "content": None
        }
    )
    messages.append( # 將函式回應新增到訊息中
        {
            "role": "function",
            "name": function_name,
            "content":function_response,
        }
    )
   ```

   這三行提取函式名稱、引數並進行呼叫：

   ```python
   function_to_call = available_functions[function_name]

   function_args = json.loads(response_message.function_call.arguments)
   function_response = function_to_call(**function_args)
   ```

   以下是執行程式碼的輸出：

   **輸出**

   ```建議的函式呼叫：
   {
     "name": "search_courses",
     "arguments": "{\n  \"role\": \"student\",\n  \"product\": \"Azure\",\n  \"level\": \"beginner\"\n}"
   }

   函式呼叫的輸出：
   [{'title': '描述密碼學概念', 'url': 'https://learn.microsoft.com/training/modules/describe-concepts-of-cryptography/?
   WT.mc_id=api_CatalogApi'}, {'title': 'TensorFlow 音訊分類簡介', 'url': 'https://learn.microsoft.com/en-
   us/training/modules/intro-audio-classification-tensorflow/?WT.mc_id=api_CatalogApi'}, {'title': '使用 Azure Data Studio 在 Azure SQL
   資料庫中設計高效能資料模型', 'url': 'https://learn.microsoft.com/training/modules/design-a-data-model-with-ads/?
   WT.mc_id=api_CatalogApi'}, {'title': 'Azure Microsoft Cloud Adoption Framework 入門', 'url':
   'https://learn.microsoft.com/training/modules/cloud-adoption-framework-getting-started/?WT.mc_id=api_CatalogApi'}, {'title': '設定
   Rust 開發環境', 'url': 'https://learn.microsoft.com/training/modules/rust-set-up-environment/?WT.mc_id=api_CatalogApi'}]
   <class 'str'>
   ```

2. 現在將更新後的訊息 `messages` 傳送回 LLM，這樣我們就可以收到自然語言回應，而不是 JSON 格式的 API 回應。

   ```python
   print("下一個請求中的訊息：")
   print(messages)
   print()

   second_response = client.chat.completions.create(
      messages=messages,
      model=deployment,
      function_call="auto",
      functions=functions,
      temperature=0
         )  # 從 GPT 取得新的回應，其中它可以看到函式回應


   print(second_response.choices[0].message)
   ```

   **輸出**

   ```python
   {
     "role": "assistant",
     "content": "我為初學者學生找到了一些學習 Azure 的好課程：\n\n1. [描述密碼學概念] (https://learn.microsoft.com/training/modules/describe-concepts-of-cryptography/?WT.mc_id=api_CatalogApi)\n2. [TensorFlow 音訊分類簡介](https://learn.microsoft.com/training/modules/intro-audio-classification-tensorflow/?WT.mc_id=api_CatalogApi)\n3. [使用 Azure Data Studio 在 Azure SQL 資料庫中設計高效能資料模型](https://learn.microsoft.com/training/modules/design-a-data-model-with-ads/?WT.mc_id=api_CatalogApi)\n4. [Azure Microsoft Cloud Adoption Framework 入門](https://learn.microsoft.com/training/modules/cloud-adoption-framework-getting-started/?WT.mc_id=api_CatalogApi)\n5. [設定 Rust 開發環境](https://learn.microsoft.com/training/modules/rust-set-up-environment/?WT.mc_id=api_CatalogApi)\n\n您可以點擊連結以存取課程。"
   }

   ```

## 作業

若要繼續學習 Azure OpenAI 函式呼叫，您可以建置：

- 函式的更多參數，以幫助學習者找到更多課程。
- 另一個函式呼叫，從學習者那裡收集額外資訊，例如他們的母語。
- 函式呼叫和/或 API 呼叫未傳回任何合適課程時的錯誤處理。
## 做得好！繼續旅程

完成本課後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 技能！

前往第 12 課，我們將探討如何[為 AI 應用程式設計 UX](../12-designing-ux-for-ai-applications/README.md?WT.mc_id=academic-105485-koreyst)！

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。
