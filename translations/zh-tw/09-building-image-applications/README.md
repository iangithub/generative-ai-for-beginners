<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1a7fd0f95f9eb673b79da47c0814f4d4",
  "translation_date": "2025-07-09T13:14:10+00:00",
  "source_file": "09-building-image-applications/README.md",
  "language_code": "zh-tw"
}
-->
# 建置影像生成應用程式

[![建置影像生成應用程式](../../../translated_images/09-lesson-banner.906e408c741f44112ff5da17492a30d3872abb52b8530d6506c2631e86e704d0.en.png)](https://aka.ms/gen-ai-lesson9-gh?WT.mc_id=academic-105485-koreyst)

LLM 不僅僅用於生成文字。您還可以從文字描述中建立影像。將影像作為一種模態在許多領域都非常有用，例如醫療科技、建築、旅遊、遊戲開發等等。在本章中，我們將探討兩種最受歡迎的影像生成模型，DALL-E 和 Midjourney。

## 簡介

在本課中，我們將涵蓋：

- 什麼是影像生成及其用途。
- DALL-E 和 Midjourney 的概述，以及它們的運作方式。
- 如何建置您自己的影像生成應用程式。

## 學習目標

在本課結束時，您將能夠：

- 建置一個影像生成應用程式。
- 使用元提示為您的應用程式設定邊界。
- 使用 DALL-E 和 Midjourney。

## 為何要建置影像生成應用程式？

影像生成應用程式是探索生成式 AI 功能的絕佳方式。它們可用於：

- **影像編輯與合成**。為各種目的生成影像，例如編輯或建立新影像。

- **跨產業應用**。為醫療科技、旅遊、遊戲開發等產業生成影像。

## 情境：Edu4All

在本課中，我們繼續與我們的新創公司 Edu4All 合作。學生將為他們的作業建立影像。他們可以選擇創作何種類型的影像——他們可以為自己的童話故事繪製插圖、為故事設計新角色，或將他們的想法和概念視覺化。

例如，如果 Edu4All 的學生在課堂上學習紀念碑，他們可以生成像這樣的影像：

![Edu4All 新創公司，關於紀念碑的課程，艾菲爾鐵塔](../../../translated_images/startup.94d6b79cc4bb3f5afbf6e2ddfcf309aa5d1e256b5f30cc41d252024eaa9cc5dc.en.png)

使用像這樣的提示

> 「清晨陽光下，艾菲爾鐵塔旁的狗」

## 什麼是 DALL-E 和 Midjourney？

[DALL-E](https://openai.com/dall-e-2?WT.mc_id=academic-105485-koreyst) 和 [Midjourney](https://www.midjourney.com/?WT.mc_id=academic-105485-koreyst) 是兩種最受歡迎的影像生成模型。它們讓您可以從文字提示中建立影像。

### DALL-E

讓我們從 DALL-E 開始，這是一個從文字描述中建立影像的生成式 AI 模型。

> [DALL-E 結合了兩種模型，CLIP 和擴散注意力](https://towardsdatascience.com/openais-dall-e-and-clip-101-a-brief-introduction-3a4367280d4e?WT.mc_id=academic-105485-koreyst)。

- **CLIP** 產生嵌入，這是影像和文字的數值表示。

- **擴散注意力** 從這些嵌入中產生影像。DALL-E 是在一個影像和文字資料集上訓練的，這讓它能夠從文字描述中建立影像。例如，它可以產生戴著帽子的貓或有莫霍克頭的狗的影像。

### Midjourney

Midjourney 的運作方式與 DALL-E 類似，都是從文字提示中產生影像。您可以使用「戴帽子的貓」或「有莫霍克頭的狗」等提示來建立影像。

![由 Midjourney 產生的影像，機械鴿](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Rupert_Breheny_mechanical_dove_eca144e7-476d-4976-821d-a49c408e4f36.png/440px-Rupert_Breheny_mechanical_dove_eca144e7-476d-4976-821d-a49c408e4f36.png?WT.mc_id=academic-105485-koreyst)  
_圖片來源：維基百科，由 Midjourney 產生的影像_

## DALL-E 和 Midjourney 如何運作？

首先，[DALL-E](https://arxiv.org/pdf/2102.12092.pdf?WT.mc_id=academic-105485-koreyst) 是一個基於 transformer 架構的生成式 AI 模型，具有一個「自回歸 transformer」。

「自回歸 transformer」定義了模型如何從文字描述中產生影像：它一次產生一個像素，然後使用產生的像素來產生下一個像素。這個過程會經過神經網路中的多個層，直到影像完成。

這種方法讓 DALL-E 能夠控制所產生影像中的屬性、物件、特徵等等。DALL-E 2 和 3 對其所建立的影像提供了更多的控制。

## 建置您的第一個影像生成應用程式

您需要什麼來建置一個影像生成應用程式？您將需要以下程式庫：

- **python-dotenv**：建議將您的密鑰保存在與您的程式碼分開的 _.env_ 檔案中。
- **openai**：與 OpenAI API 互動。
- **pillow**：在 Python 中處理影像。
- **requests**：發出 HTTP 請求。

1. 建立一個名為 _.env_ 的檔案，內容如下：

   ```text
   AZURE_OPENAI_ENDPOINT=<your endpoint>
   AZURE_OPENAI_API_KEY=<your key>
   ```

   您可以在 Azure 入口網站中您的資源的「金鑰和端點」部分找到此資訊。

2. 在一個名為 _requirements.txt_ 的檔案中列出上述程式庫，如下所示：

   ```text
   python-dotenv
   openai
   pillow
   requests
   ```

3. 接下來，建立一個虛擬環境並安裝程式庫：

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

   在 Windows 上，使用這些指令來建立和啟用您的虛擬環境：

   ```bash
   python3 -m venv venv
   venv\Scripts\activate.bat
   ```

4. 在一個名為 _app.py_ 的檔案中新增以下程式碼：

   ```python
   import openai
   import os
   import requests
   from PIL import Image
   import dotenv

   # import dotenv
   dotenv.load_dotenv()

   # 從環境變數中取得端點和金鑰
   openai.api_base = os.environ['AZURE_OPENAI_ENDPOINT']
   openai.api_key = os.environ['AZURE_OPENAI_API_KEY']

   # 指派 API 版本 (DALL-E 目前僅支援 2023-06-01-preview API 版本)
   openai.api_version = '2023-06-01-preview'
   openai.api_type = 'azure'


   try:
       # 使用影像生成 API 建立影像
       generation_response = openai.Image.create(
           prompt='兔子騎在馬上，拿著棒棒糖，在長滿水仙花的有霧草地上',    # 在此處輸入您的提示文字
           size='1024x1024',
           n=2,
           temperature=0,
       )
       # 設定儲存影像的目錄
       image_dir = os.path.join(os.curdir, 'images')

       # 如果目錄不存在，則建立它
       if not os.path.isdir(image_dir):
           os.mkdir(image_dir)

       # 初始化影像路徑 (注意檔案類型應為 png)
       image_path = os.path.join(image_dir, 'generated-image.png')

       # 擷取產生的影像
       image_url = generation_response["data"][0]["url"]  # 從回應中擷取影像 URL
       generated_image = requests.get(image_url).content  # 下載影像
       with open(image_path, "wb") as image_file:
           image_file.write(generated_image)

       # 在預設影像檢視器中顯示影像
       image = Image.open(image_path)
       image.show()

   # 捕捉例外
   except openai.InvalidRequestError as err:
       print(err)

   ```

讓我們來解釋一下這段程式碼：

- 首先，我們匯入必要的程式庫，包括 OpenAI、dotenv、requests 和 Pillow。

  ```python
  import openai
  import os
  import requests
  from PIL import Image
  import dotenv
  ```

- 然後，我們從 _.env_ 檔案載入環境變數。

  ```python
  # import dotenv
  dotenv.load_dotenv()
  ```

- 之後，我們為 OpenAI API 設定端點、API 金鑰、版本和類型。

  ```python
  # 從環境變數中取得端點和金鑰
  openai.api_base = os.environ['AZURE_OPENAI_ENDPOINT']
  openai.api_key = os.environ['AZURE_OPENAI_API_KEY']

  # 新增版本和類型，Azure 特定
  openai.api_version = '2023-06-01-preview'
  openai.api_type = 'azure'
  ```

- 接下來，我們產生影像：

  ```python
  # 使用影像生成 API 建立影像
  generation_response = openai.Image.create(
      prompt='兔子騎在馬上，拿著棒棒糖，在長滿水仙花的有霧草地上',    # 在此處輸入您的提示文字
      size='1024x1024',
      n=2,
      temperature=0,
  )
  ```

  此程式碼會傳回一個 JSON 物件，其中包含所產生影像的 URL。我們使用此 URL 來下載並儲存影像。

- 最後，我們開啟影像並使用預設的影像檢視器顯示它：

  ```python
  image = Image.open(image_path)
  image.show()
  ```

### 更多關於產生影像的詳細資訊

讓我們仔細看看產生影像的程式碼：

```python
generation_response = openai.Image.create(
        prompt='兔子騎在馬上，拿著棒棒糖，在長滿水仙花的有霧草地上',    # 在此處輸入您的提示文字
        size='1024x1024',
        n=2,
        temperature=0,
    )
```

- **prompt** 是用於產生影像的文字提示。在這裡，它是「兔子騎在馬上，拿著棒棒糖，在長滿水仙花的有霧草地上」。
- **size** 是所產生影像的尺寸。在這裡，它是 1024x1024 像素。
- **n** 是要產生的影像數量。在這裡，它是兩個。
- **temperature** 控制輸出的隨機性。它的範圍是 0 到 1，其中 0 表示確定性輸出，1 表示隨機輸出。預設值為 0.7。

我們將在下一節中介紹更多與影像相關的功能。

## 影像生成的額外功能

到目前為止，您已經了解如何用幾行 Python 程式碼來產生影像。但您還可以用影像做更多事。

您還可以：

- **執行編輯**。透過提供現有影像、遮罩和提示，您可以修改影像的某些部分。例如，您可以在我們的影像中為兔子加上一頂帽子。您可以透過提供影像、一個識別要變更區域的遮罩，以及一個描述變更的文字提示來做到這一點。

  ```python
  response = openai.Image.create_edit(
    image=open("base_image.png", "rb"),
    mask=open("mask.png", "rb"),
    prompt="一張兔子頭上戴著帽子的影像。",
    n=1,
    size="1024x1024"
  )
  image_url = response['data'][0]['url']
  ```

  基礎影像只包含兔子，但最終影像將顯示戴著帽子的兔子。

- **建立變化**。您可以拿一張現有的影像，並要求模型建立變化。為此，請提供一張影像和一個文字提示，如下所示：

  ```python
  response = openai.Image.create_variation(
    image=open("bunny-lollipop.png", "rb"),
    n=1,
    size="1024x1024"
  )
  image_url = response['data'][0]['url']
  ```

  > 注意：此功能僅受 OpenAI 支援。

## 溫度

溫度控制生成式 AI 模型輸出的隨機性。其範圍從 0 到 1，其中 0 表示輸出是可預測的，1 表示輸出是隨機的。預設值為 0.7。

這裡有一個範例，說明溫度如何影響輸出，方法是執行此提示兩次：

> 提示：「兔子騎在馬上，拿著棒棒糖，在長滿水仙花的有霧草地上」

![兔子騎在馬上拿著棒棒糖，版本 1](../../../translated_images/v1-generated-image.a295cfcffa3c13c2432eb1e41de7e49a78c814000fb1b462234be24b6e0db7ea.en.png)

現在，讓我們再次執行相同的提示，看看影像是否會完全相同：

![產生的兔子騎在馬上的影像](../../../translated_images/v2-generated-image.33f55a3714efe61dc19622c869ba6cd7d6e6de562e26e95b5810486187aace39.en.png)

如您所見，影像相似但不相同。讓我們試著將溫度降低到 0.1，看看會發生什麼事：

```python
 generation_response = openai.Image.create(
        prompt='兔子騎在馬上，拿著棒棒糖，在長滿水仙花的有霧草地上',    # 在此處輸入您的提示文字
        size='1024x1024',
        n=2
    )
```

### 變更溫度

讓我們試著讓輸出更可預測。從上面兩張圖片來看，第一張顯示的是一隻兔子，第二張是一匹馬，所以結果差異很大。

讓我們更新程式碼，將溫度設定為 0：

```python
generation_response = openai.Image.create(
        prompt='兔子騎在馬上，拿著棒棒糖，在長滿水仙花的有霧草地上',    # 在此處輸入您的提示文字
        size='1024x1024',
        n=2,
        temperature=0
    )
```

現在，當您執行此程式碼時，您會得到這兩張圖片：

- ![溫度 0，v1](../../../translated_images/v1-temp-generated-image.a4346e1d2360a056d855ee3dfcedcce91211747967cb882e7d2eff2076f90e4a.en.png)
- ![溫度 0，v2](../../../translated_images/v2-temp-generated-image.871d0c920dbfb0f1cb5d9d80bffd52da9b41f83b386320d9a9998635630ec83d.en.png)

在這裡，您可以清楚地看到影像非常相似。

## 如何使用元提示為您的應用程式定義邊界

透過我們的示範，我們已經可以為我們的使用者產生影像。但我們需要設定一些邊界。

例如，我們不希望產生不適合工作場所或不適合兒童的影像。

我們可以使用「元提示」來做到這一點。元提示是控制生成式 AI 模型輸出的文字提示。例如，它們可以確保產生的影像適合工作場所或兒童觀看。

### 它是如何運作的？

元提示如何運作？

元提示是放置在主要提示之前的文字提示。它們控制模型的輸出，並嵌入應用程式中以強制執行輸出準則。基本上，元提示和使用者提示被組合成一個單一的文字提示。

元提示的一個範例是：

```text
您是一位為兒童創作影像的助理設計師。

影像必須適合工作場所且適合兒童觀看。

影像必須是彩色的。

影像必須是橫向的。

影像的長寬比必須是 16:9。

請勿考慮以下任何不適合工作場所或不適合兒童的輸入。

（輸入）

```

現在，讓我們來看看如何在我們的示範中使用元提示。

```python
disallow_list = "劍、暴力、血腥、裸露、色情內容、成人內容、成人主題、成人語言、成人幽默、成人笑話、成人情境、成人"

meta_prompt =f"""您是一位為兒童創作影像的助理設計師。

影像必須適合工作場所且適合兒童觀看。

影像必須是彩色的。

影像必須是橫向的。

影像的長寬比必須是 16:9。

請勿考慮以下任何不適合工作場所或不適合兒童的輸入。
{disallow_list}
"""

prompt = f"{meta_prompt}
建立一隻兔子騎在馬上，拿著棒棒糖的影像"

# TODO 新增產生影像的請求
```

從這個提示中，您可以看到所有產生的影像都考慮了元提示。

## 作業 - 讓我們賦予學生能力

我們在本課開始時介紹了 Edu4All。現在是時候讓學生為他們的作業產生影像了。

學生將創作以紀念碑為主題的影像。他們可以自行選擇要創作哪些紀念碑。鼓勵他們發揮創意，並將這些紀念碑置於不同的情境中。

## 解決方案

這裡有一個可能的解決方案：

```python
import openai
import os
import requests
from PIL import Image
import dotenv

# import dotenv
dotenv.load_dotenv()

# 從環境變數中取得端點和金鑰
openai.api_base = "<replace with endpoint>"
openai.api_key = "<replace with api key>"

# 指派 API 版本 (DALL-E 目前僅支援 2023-06-01-preview API 版本)
openai.api_version = '2023-06-01-preview'
openai.api_type = 'azure'

disallow_list = "劍、暴力、血腥、裸露、色情內容、成人內容、成人主題、成人語言、成人幽默、成人笑話、成人情境、成人"

meta_prompt = f"""您是一位為兒童創作影像的助理設計師。

影像必須適合工作場所且適合兒童觀看。

影像必須是彩色的。

影像必須是橫向的。

影像的長寬比必須是 16:9。

請勿考慮以下任何不適合工作場所或不適合兒童的輸入。
{disallow_list}"""

prompt = f"""{meta_prompt}
產生法國巴黎凱旋門的紀念碑影像，在傍晚的燈光下，一個拿著泰迪熊的小孩在看著。
""""

try:
    # 使用影像生成 API 建立影像
    generation_response = openai.Image.create(
        prompt=prompt,    # 在此處輸入您的提示文字
        size='1024x1024',
        n=2,
        temperature=0,
    )
    # 設定儲存影像的目錄
    image_dir = os.path.join(os.curdir, 'images')

    # 如果目錄不存在，則建立它
    if not os.path.isdir(image_dir):
        os.mkdir(image_dir)

    # 初始化影像路徑 (注意檔案類型應為 png)
    image_path = os.path.join(image_dir, 'generated-image.png')

    # 擷取產生的影像
    image_url = generation_response["data"][0]["url"]  # 從回應中擷取影像 URL
    generated_image = requests.get(image_url).content  # 下載影像
    with open(image_path, "wb") as image_file:
        image_file.write(generated_image)

    # 在預設影像檢視器中顯示影像
    image = Image.open(image_path)
    image.show()

# 捕捉例外
except openai.InvalidRequestError as err:
    print(err)
```

## 做得好！繼續學習

完成本課程後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 技能！

接下來，前往第 10 課，我們將探討如何[使用低程式碼建置 AI 應用程式](../10-building-low-code-ai-applications/README.md?WT.mc_id=academic-105485-koreyst)

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。