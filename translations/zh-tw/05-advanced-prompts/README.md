<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2b4c36be7d66b32e4fac47761718b4a9",
  "translation_date": "2025-07-09T11:22:22+00:00",
  "source_file": "05-advanced-prompts/README.md",
  "language_code": "zh-tw"
}
-->

# 為 Python Web API 產生程式碼

本指南將協助您使用 FastAPI 框架建立一個簡單的 Python Web API。

## 先決條件

- 已安裝 Python 3.7 或更高版本
- Python 程式設計基礎知識
- 熟悉 RESTful API

## 安裝

首先，使用 pip 安裝 FastAPI 和 Uvicorn (一個 ASGI 伺服器)：

```bash
pip install fastapi uvicorn
```

## 建立 API

建立一個名為 `main.py` 的新 Python 檔案，並新增下列程式碼：

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def read_root():
    return {"message": "Hello World"}
```

此程式碼會初始化一個 FastAPI 應用程式，並定義一個根端點，該端點會傳回一個簡單的 JSON 訊息。

## 執行 API

使用 Uvicorn 執行 API 伺服器，指令如下：

```bash
uvicorn main:app --reload
```

`--reload` 旗標會在程式碼變更時啟用自動重新載入，這在開發期間很有用。

## 測試 API

開啟您的瀏覽器並導覽至 `http://127.0.0.1:8000/`。您應該會看到 JSON 回應：

```json
{"message": "Hello World"}
```

## 互動式 API 文件

FastAPI 會自動產生互動式 API 文件。您可以透過以下網址存取：

- Swagger UI：`http://127.0.0.1:8000/docs`
- ReDoc：`http://127.0.0.1:8000/redoc`

## 後續步驟

- 新增更多使用不同 HTTP 方法 (POST、PUT、DELETE) 的端點
- 使用 Pydantic 模型實作請求驗證
- 將您的 API 連接到資料庫以進行永久儲存

[!TIP]  
探索 FastAPI 官方文件以了解更多進階功能和最佳實務。
```python
#import necessary libraries
import flask
from flask import request, jsonify

#create an instance of the Flask class
app = flask.Flask(__name__)

#create an endpoint for the API
@app.route('/api/v1/endpoint', methods=['GET'])
def api_endpoint():
    #get the request data
    data = request.get_json()

    #process the data
    result = process_data(data)

    #return the result
    return jsonify(result)

#function to process the data
def process_data(data):
    #process the data
    result = {'result': 'success'}

    #return the result
    return result

#run the Flask app
if __name__ == '__main__':
    app.run()

```

再次執行提示會得到以下結果：

```python
#import necessary libraries
import flask
from flask import request, jsonify

#create a Flask app
app = flask.Flask(__name__)

#create a route for the API
@app.route('/api', methods=['GET'])
def api_call():
    #get the data from the request
    data = request.get_json()

    #process the data
    result = process_data(data)

    #return the result
    return jsonify(result)

#define the process_data function
def process_data(data):
    #do something with the data
    result = data + 1

    #return the result
    return result

#run the app
if __name__ == '__main__':
    app.run()

```

這兩個輸出之間只有微小的差異。這次讓我們試試相反的做法，將溫度設定為 0.9：

```python
# Import necessary libraries
import flask
from flask import request, jsonify

# Create a Flask app
app = flask.Flask(__name__)

# Create a route for the API
@app.route('/api', methods=['GET'])
def api_call():
    # Get the data from the request
    data = request.args

    # Process the data
    result = process_data(data)

    # Return the result
    return jsonify(result)

# Function to process the data
def process_data(data):
    # Do something with the data
    result = data + 1

    # Return the result
    return result

# Run the app
if __name__ == '__main__':
    app.run()

```

這是第二次嘗試，溫度設定為 0.9：

```python
import flask
from flask import request, jsonify

# create the Flask app
app = flask.Flask(__name__)
app.config['DEBUG'] = True

# create some test data
books = [
    {'id': 0, 'title': 'A Fire Upon The Deep', 'author': 'Vernor Vinge', 'first_sentence': 'The coldsleep itself was dreamless.', 'year_published': '1992'},
    {'id': 1, 'title': 'The Ones Who Walk Away From Omelas', 'author': 'Ursula K. Le Guin', 'first_sentence': 'With a clamor of bells that set the swallows soaring, the Festival of Summer came to the city Omelas, bright-towered by the sea.', 'published': '1973'},
    {'id': 2, 'title': 'Dhalgren', 'author': 'Samuel R. Delany', 'first_sentence': 'to wound the autumnal city.', 'published': '1975'}
]

# create an endpoint
@app.route('/', methods=['GET'])
def home():
    return '''<h1>Welcome to our book API!</h1>'''

@app.route('/api/v1/resources/books

```

如您所見，結果差異很大。

> 請注意，您還可以調整其他參數來變更輸出，例如 top-k、top-p、重複懲罰、長度懲罰和多樣性懲罰，但這些都超出了本課程的範圍。

## 良好實務

您可以使用許多技巧來嘗試獲得想要的結果。隨著您在提示方面獲得更多經驗，您將發展出自己的風格。

除了我們已經介紹過的技巧之外，在提示 LLM 時還需要記住一些良好的實務：

- **指定上下文。** 上下文很重要——您能指定的越多，例如領域、主題等，就越好。
- 限制輸出。如果您想要特定數量的項目或特定長度，請務必指定。
- **同時指定「什麼」和「如何」。** 請記住同時提及您想要的「什麼」和您想要的「如何」，例如，「建立一個 Python Web API，其中包含產品和客戶的路由，並分成 3 個檔案。」
- **使用範本。** 通常，您會希望用公司的資料來豐富您的提示。請使用範本來達成此目的。範本可以包含您用實際資料取代的變數。
- **正確拼寫。** LLM 可能仍然會提供正確的回應，但正確拼寫將有助於您獲得更好的回應。

## 作業

這裡有一些 Python 程式碼，展示如何使用 Flask 建置一個簡單的 API：

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/')
def hello():
    name = request.args.get('name', 'World')
    return f'Hello, {name}!'

if __name__ == '__main__':
    app.run()
```

使用像 GitHub Copilot 或 ChatGPT 這樣的 AI 助理，並應用「自我完善」技巧來改善程式碼。

## 解決方案

嘗試透過在程式碼中加入適當的提示來解決作業。

> [!TIP]
> 提出一個要求改進的提示，最好限制您想要的改進數量。您也可以要求在特定領域進行改進，例如架構、效能、安全性等。

[解決方案](../../../05-advanced-prompts/python/aoai-solution.py)

## 知識測驗

我為什麼要使用思維鏈提示？給我看 1 個正確的回應和 2 個不正確的回應。

1. 教導 LLM 如何解決問題。
2. B，教導 LLM 在程式碼中尋找錯誤。
3. C，指示 LLM 想出不同的解決方案。

A：1，因為思維鏈是關於透過提供一系列步驟，以及類似的問題和它們的解決方法，來向 LLM 展示如何解決問題。

## 🚀 挑戰

您剛剛在作業中使用了自我完善技巧。拿任何您建置的程式，思考您想做哪些改進。現在使用自我完善技巧來應用這些變更。您對結果有何看法——是更好還是更差？

## 做得好！繼續學習

完成本課程後，請查看我們的 [生成式 AI 學習合輯](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) 以繼續增進您的生成式 AI 技能！

前往第 6 課，我們將應用我們的提示工程知識來[建置文字生成應用程式](../06-text-generation-apps/README.md?WT.mc_id=academic-105485-koreyst)

**免責聲明**：
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以其母語的原始文件為權威來源。對於關鍵資訊，建議進行專業的人工翻譯。我們對因使用本翻譯而產生的任何誤解或曲解概不負責。