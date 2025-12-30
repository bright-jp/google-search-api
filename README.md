# Google Search API

[![Promo](https://media.brightdata.com/2025/08/SERP-API-50-off-GitHub-banner_1389_166.png)](https://brightdata.jp/products/serp-api/google-search) 

> ⚠️ 2025年1月時点で、検索結果をレンダリングするために[GoogleはJavaScriptを必須としています](https://techcrunch.com/2025/01/17/google-begins-requiring-javascript-for-google-search/)。この更新は、JavaScript非対応の手法に依存する従来型のボット、スクレイパー、SEOツールをブロックすることを目的としています。その結果、市場調査やランキング分析のためにGoogle Searchを利用する企業は、JavaScriptレンダリングに対応したツールを採用する必要があります。


このリポジトリでは、Google SERPデータを収集するための2つのアプローチを提供しています。

1. 基本的なデータ収集に適した、無料の小規模スクレイパー
2. 大量かつ堅牢なデータニーズ向けに構築された、エンタープライズグレードのAPIソリューション


## Table of Contents
- [Free Scraper](#free-scraper)
  - [Input Parameters](#input-parameters)
  - [Implementation](#implementation)
  - [Sample Output](#sample-output)
  - [Limitations](#limitations)
- [Bright Data Google Search API](#bright-data-google-search-api)
  - [Key Features](#key-features)
  - [Getting Started](#getting-started)
  - [Direct API Access](#direct-api-access)
  - [Native Proxy-Based Access](#native-proxy-based-access)
- [Advanced Features](#advanced-features)
  - [Localization](#localization)
  - [Search Type](#search-type)
  - [Pagination](#pagination)
  - [Geo-Location](#geo-location)
  - [Device Type](#device-type)
  - [Browser Type](#browser-type)
  - [Parsing Results](#parsing-results)
  - [Hotel Search](#hotel-search)
  - [Parallel Searches](#parallel-searches)
  - [AI Overview](#ai-overview)
- [Support & Resources](#support--resources)


## Free Scraper
基本的なデータ収集ニーズ向けの、軽量なGoogleスクレイパーです。

<img width="700" alt="google-search-result" src="https://github.com/bright-jp/google-search-api/blob/main/images/416310595-58573147-5ac2-4cb3-bb5e-295d76f6972c.png" />

### Input Parameters

- **File:** Googleでクエリする検索語のリスト（必須）
- **Pages:** データをスクレイピングするGoogleページ数

### Implementation
これらのパラメータを、[Python file](https://github.com/bright-jp/Google-Search-API/blob/main/free_google_scraper/google_serp.py)で変更してください。

```python
HEADLESS = False        
MAX_RETRIES = 2         
REQUEST_DELAY = (1, 4) 

SEARCH_TERMS = [
    "nike shoes",
    "macbook pro"
]
PAGES_PER_TERM = 3      
```

💡 **Tip:** `HEADLESS = False` に設定すると、Googleの検知メカニズムを回避しやすくなります。

### Sample Output
<img width="700" alt="google-serp-data" src="https://github.com/bright-jp/google-search-api/blob/main/images/416109839-c7048fc9-44c3-4553-8117-2b238d354f70.png" />


### Limitations

Googleは、複数のアンチスクレイピング対策を実装しています。

1. **CAPTCHAs:** 人間とボットを区別するために使用されます
2. **IP Blocks:** 不審なアクティビティに対する一時的または恒久的なBANです
3. **Rate Limiting:** 急速なリクエストはブロックを引き起こす可能性があります
4. **Geotargeting:** 結果は場所、言語、デバイスによって変化します
5. **Honeypot Traps:** 自動アクセスを検出するための隠し要素です

複数回リクエストすると、おそらくGoogleのCAPTCHAチャレンジに遭遇します。

<img width="700" alt="google-captcha" src="https://github.com/bright-jp/google-search-api/blob/main/images/414117571-21ab3e9f-1162-4aef-9e22-fb08491dd928.png" />

## Bright Data Google Search API
[Bright Data's Google Search API](https://brightdata.jp/products/serp-api/google-search) は、カスタマイズ可能な検索パラメータを使用して、Googleから実ユーザーの検索結果を提供します。[SERP API](https://brightdata.jp/products/serp-api)と同じ先進技術に基づいて構築されており、公開データを大規模にスクレイピングする際に、高い成功率と堅牢なパフォーマンスを提供します。


### Key Features

- 大量でも高い成功率
- 成功したリクエストに対してのみ課金
- 高速なレスポンスタイム（5秒未満）
- ジオロケーションターゲティング – 任意の国・都市・デバイスからデータを抽出
- 出力形式 – JSONまたは生HTMLでデータを取得
- 複数の検索タイプ – News、images、shopping、jobsなど
- 非同期リクエスト – 結果をバッチで取得
- スケール向けに設計 – 高トラフィックとピーク負荷に対応

📌 [SERP Playground](https://brightdata.jp/products/serp-api/google-search)で無料でお試しください。

<img width="700" alt="bright-data-serp-api-playground" src="https://github.com/bright-jp/google-search-api/blob/main/images/416966701-8d516e08-37a1-4723-bf12-9a9da6a13b1a.png" />


### Getting Started

1. **Prerequisites:**
    - [Bright Data account](https://brightdata.jp/)を作成してください（新規ユーザーには$5クレジットが付与されます）
    - [API key](https://docs.brightdata.com/general/account/api-token)を取得してください
2. **Setup:** [step-by-step guide](https://github.com/bright-jp/Google-Search-API/blob/main/setup_serp_api.md)に従って、Bright DataアカウントにSERP APIを統合してください
3. **Implementation Methods:**
    - Direct API Access
    - Native Proxy-Based Access


### Direct API Access
最も簡単な方法は、APIに直接リクエストすることです。

**cURL Example**
```bash
curl https://api.brightdata.com/request \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer API_TOKEN" \
  -d '{
        "zone": "ZONE_NAME",
        "url": "https://www.google.com/search?q=ollama&brd_json=1",
        "format": "raw"
      }'
```

**Python Example**
```python
import requests
import json

url = "https://api.brightdata.com/request"

headers = {"Content-Type": "application/json", "Authorization": "Bearer API_TOKEN"}

payload = {
    "zone": "ZONE_NAME",
    "url": "https://www.google.com/search?q=ollama&brd_json=1",
    "format": "raw",
}

response = requests.post(url, headers=headers, json=payload)

with open("serp_direct_api.json", "w") as file:
    json.dump(response.json(), file, indent=4)

print("Response saved to 'serp_direct_api.json'.")
```

👉 [full JSON output](https://github.com/bright-jp/Google-Search-API/blob/main/google_search_api_outputs/serp_direct_api.json)をご覧ください。

> **Note**: パース済みJSONには `brd_json=1` を使用し、パース済みJSON + 完全にネストされたHTMLには `brd_json=html` を使用してください。

検索結果のパースについて詳しくは、[SERP API Parsing Guide](https://docs.brightdata.com/scraping-automation/serp-api/parsing-search-results)をご覧ください。

### Native Proxy-Based Access
代わりに、プロキシルーティング方式を使用することもできます。

**cURL Example**
```bash
curl -i \
  --proxy brd.superproxy.io:33335 \
  --proxy-user "brd-customer-<CUSTOMER_ID>-zone-<ZONE_NAME>:<ZONE_PASSWORD>" \
  -k \
  "https://www.google.com/search?q=ollama"
```

**Python Example**
```python
import requests
import urllib3

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

host = "brd.superproxy.io"
port = 33335
username = "brd-customer-<customer_id>-zone-<zone_name>"
password = "<zone_password>"
proxy_url = f"http://{username}:{password}@{host}:{port}"

proxies = {"http": proxy_url, "https": proxy_url}

url = "https://www.google.com/search?q=ollama"
response = requests.get(url, proxies=proxies, verify=False)

with open("serp_native_proxy.html", "w", encoding="utf-8") as file:
    file.write(response.text)

print("Response saved to 'serp_native_proxy.html'.")
```

👉 [full HTML output](https://github.com/bright-jp/Google-Search-API/blob/main/google_search_api_outputs/serp_native_proxy.html)をご覧ください。

本番環境では、Bright DataのSSL証明書を読み込んでください（[SSL Certificate Guide](https://docs.brightdata.com/general/account/ssl-certificate)を参照してください）。

## Advanced Features

### Localization
<img width="700" alt="bright-data-google-search-api-screenshot-localization" src="https://github.com/bright-jp/google-search-api/blob/main/images/416281053-eb050c00-3c35-451b-a2d2-e98e16f91aee.png" />


1. `gl` (Country Code)
    - 検索結果の国を決定する2文字の国コードです
    - 特定の国から行われた検索をシミュレートします
    
    Example: フランスでレストランを検索する
    
    ```bash
    curl --proxy brd.superproxy.io:33335 \
     --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
     "https://www.google.com/search?q=best+restaurants+in+paris&gl=fr"
    ```
    
2. `hl` (Language Code)
    - ページコンテンツの言語を設定する2文字の言語コードです
    - インターフェースおよび検索結果の言語に影響します
    
    Example: 日本で寿司店を検索する（結果は日本語）
    
    ```bash
    curl --proxy brd.superproxy.io:33335 \
     --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
     "https://www.google.com/search?q=best+sushi+restaurants+in+tokyo&hl=ja"
    ```
    
    より適切なローカライズのために、両方のパラメータを併用できます。
    
    ```bash
    curl --proxy brd.superproxy.io:33335 \
     --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
     "https://www.google.com/search?q=best+hotels+in+berlin&gl=de&hl=de"
    ```

### Search Type
<img width="700" alt="bright-data-google-search-api-screenshot-search-type" src="https://github.com/bright-jp/google-search-api/blob/main/images/416280410-49853108-5e3d-4062-831b-8d55711d5f54.png" />

1. `tbm` (Search Category)
    - 特定の検索タイプ（画像、ニュースなど）を指定します
    - **Options**:
        - `tbm=isch` → **Images**
        - `tbm=shop` → **Shopping**
        - `tbm=nws` → **News**
        - `tbm=vid` → **Videos**
    
    **Example**（Shopping検索）:
    
    ```bash
    curl --proxy brd.superproxy.io:33335 \
         --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
         "https://www.google.com/search?q=macbook+pro&tbm=shop"
    ```
    
2. `ibp` (Jobs Search Parameter)
    - 求人関連の検索に特化して使用します
    - 例: `ibp=htl;jobs` は求人リストを返します
    
    **Example**:
    
    ```bash
    curl --proxy brd.superproxy.io:33335 \
         --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
         "https://www.google.com/search?q=technical+copywriter&ibp=htl;jobs"
    ```

### Pagination

結果ページ間を移動したり、表示される結果数を調整したりします。

1. `start`
    - 検索結果の開始位置を定義します
    - Examples:
        - `start=0`（default）- 1ページ目
        - `start=10` - 2ページ目（結果11-20）
        - `start=20` - 3ページ目（結果21-30）
    
    **Example**（11番目の結果から開始）:
    
    ```bash
    curl --proxy brd.superproxy.io:33335 \
         --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
         "https://www.google.com/search?q=best+coding+laptops+2025&start=10"
    ```
    
2. `num`
    - 1ページあたりに返す結果数を定義します
    - Examples:
        - `num=10`（default）- 10件の結果を返します
        - `num=50` - 50件の結果を返します
    
    **Example**（40件の結果を返す）:
    
    ```bash
    curl --proxy brd.superproxy.io:33335 \
         --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
         "https://www.google.com/search?q=best+coding+laptops+2025&num=40"
    ```


### Geo-Location
<img width="700" alt="bright-data-google-search-api-screenshot-geolocation" src="https://github.com/bright-jp/google-search-api/blob/main/images/416279186-af64c770-0c8a-4007-9415-304d2e0c0fe8.png" />

`uule` パラメータは、特定の場所に基づいて検索結果をカスタマイズします。

- プレーンテキストではなく、エンコードされた文字列が必要です。
- [Google's geotargeting CSV](https://developers.google.com/adwords/api/docs/appendix/geotargeting)のCanonical Name列で、生のロケーション文字列を見つけてください。
- サードパーティのコンバーターまたは組み込みライブラリを使用して、生の文字列をエンコード形式に変換してください。
- APIリクエストで、`uule` の値としてエンコード文字列を含めてください。

```bash
curl --proxy brd.superproxy.io:33335 \
     --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
     "https://www.google.com/search?q=best+hotels+in+paris&uule=w+CAIQICIGUGFyaXM"
```

### Device Type

<img width="700" alt="bright-data-google-search-api-screenshot-device-type" src="https://github.com/bright-jp/google-search-api/blob/main/images/416278511-cf0f203f-5d62-4eb9-9d28-7a50d75c7a00.png" />


`brd_mobile` パラメータを使用して、特定デバイスからのリクエストをシミュレートします。

| Value | Device | User-Agent Type |
| --- | --- | --- |
| `0` or omit | Desktop | Desktop |
| `1` | Mobile | Mobile |
| `ios` or `iphone` | iPhone | iOS |
| `ipad` or `ios_tablet` | iPad | iOS Tablet |
| `android` | Android | Android |
| `android_tablet` | Android Tablet | Android Tablet |

**Example: Mobile Search**

```bash
curl --proxy brd.superproxy.io:33335 \
     --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
     "https://www.google.com/search?q=best+laptops&brd_mobile=1"
```

### Browser Type
<img width="700" alt="bright-data-google-search-api-screenshot-browser-type" src="https://github.com/bright-jp/google-search-api/blob/main/images/416277969-df382cb0-0eb2-4fb1-982c-2fa3401cc83a.png" />

`brd_browser` パラメータを使用して、特定ブラウザからのリクエストをシミュレートします。

- `brd_browser=chrome` — Google Chrome
- `brd_browser=safari` — Safari
- `brd_browser=firefox` — Mozilla Firefox（`brd_mobile=1` と互換性がありません）

指定しない場合、APIはランダムなブラウザを使用します。

**Example**:

```bash
curl --proxy brd.superproxy.io:33335 \
     --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
     "https://www.google.com/search?q=best+gaming+laptops&brd_browser=chrome"
```

**Example**（ブラウザとデバイスタイプの組み合わせ）:

```bash
curl --proxy brd.superproxy.io:33335 \
     --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
     "https://www.google.com/search?q=best+smartphones&brd_browser=safari&brd_mobile=ios"
```

### Parsing Results

`brd_json` パラメータを使用して、検索結果を構造化形式で受け取ります。

- **Options**:
    - `brd_json=1` - パース済みJSON形式で結果を返します
    - `brd_json=html` - 生HTMLを含む追加の `"html"` フィールドを持つJSONを返します

Example（JSON output）:

```bash
curl --proxy brd.superproxy.io:33335 \
     --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
     "https://www.google.com/search?q=best+hotels+in+new+york&brd_json=1"
```

Example（生HTML付きJSON）:

```bash
curl --proxy brd.superproxy.io:33335 \
     --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
     "https://www.google.com/search?q=top+restaurants+in+paris&brd_json=html"
```

詳細は[ SERP API Parsing Guide](https://docs.brightdata.com/scraping-automation/serp-api/parsing-search-results)をご覧ください。


### Hotel Search

<img width="700" alt="bright-data-google-search-api-screenshot-google-hotels-search" src="https://github.com/bright-jp/google-search-api/blob/main/images/416277071-0859191a-47c0-4373-b3af-a1bc04ea54b1.png" />


以下のパラメータでホテル検索を絞り込めます。

1. `hotel_occupancy` (Number of Guests)
    - 宿泊人数を設定します（最大4）
    - Examples:
        - `hotel_occupancy=1` → 1名
        - `hotel_occupancy=2` → 2名（default）
        - `hotel_occupancy=4` → 4名
    
    **Example**（ニューヨークのホテルを4名で検索）:
    
    ```bash
    curl --proxy brd.superproxy.io:33335 \
         --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
         "https://www.google.com/search?q=hotels+in+new+york&hotel_occupancy=4"
    ```
    
2. `hotel_dates` (Check-in & Check-out Dates)
    - 特定の日付範囲で結果をフィルタリングします
    - Format: YYYY-MM-DD, YYYY-MM-DD
    
    **Example**（2025年5月1日から5月3日までのパリのホテルを検索）:
    
    ```bash
    curl --proxy brd.superproxy.io:33335 \
         --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
         "https://www.google.com/search?q=hotels+in+paris&hotel_dates=2025-05-01%2C2025-05-03"
    ```
    
    **Combined Example**:
    
    ```bash
    curl --proxy brd.superproxy.io:33335 \
         --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
         "https://www.google.com/search?q=hotels+in+tokyo&hotel_occupancy=2&hotel_dates=2025-05-01%2C2025-05-03"
    ```

### Parallel Searches

同一のpeerおよびセッション内で、複数の検索リクエストを同時に送信します。結果の比較に最適です。

1. 検索バリエーションを含む `multi` 配列でPOSTリクエストを送信します
2. 後で結果を取得するための `response_id` を取得します
3. 処理完了後、`response_id` を使用して結果を取得します

**Step 1: Send Parallel Requests**

```bash
RESPONSE_ID=$(curl -i --silent --compressed \
  "https://api.brightdata.com/serp/req?customer=<customer-id>&zone=<zone-name>" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer API_TOKEN" \
  -d $'{
    "country": "us",
    "multi": [
      {"query": {"q": "top+macbook+for+developers", "num": 20}},
      {"query": {"q": "top+macbook+for+developers", "num": 100}}
    ]
  }' | sed -En 's/^x-response-id: (.*)/\1/p' | tr -d '\r')

echo "Response ID: $RESPONSE_ID"
```

**Step 2: Fetch Results**

```bash
curl -v --compressed \
     "https://api.brightdata.com/serp/get_result?customer=<customer-id>&zone=<zone-name>&response_id=${RESPONSE_ID}" \
     -H "Authorization: Bearer API_TOKEN"
```

1つのリクエストで複数のキーワードを検索することもできます。

```bash
{
  "multi":[
    {"query":{"q":"best+smartphones+2025"}},
    {"query":{"q":"best+laptops+2025"}}
  ]
}
```

非同期リクエストについて詳しくは[こちら](https://docs.brightdata.com/scraping-automation/serp-api/asynchronous-requests)をご覧ください。

### AI Overview

<img width="700" alt="bright-data-google-search-api-screenshot-google-ai-overview" src="https://github.com/bright-jp/google-search-api/blob/main/images/416276209-3c7be724-e8d9-45ed-b781-017b1cbec9d4.png" />

Googleは、検索結果の上部にAI生成の要約（AI Overviews）を含めることがあります。`brd_ai_mode=1` を使用すると、これらのAI生成オーバービューが表示される可能性が高まります。

```bash
curl --proxy brd.superproxy.io:33335 \
     --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
     "https://www.google.com/search?q=how+does+caffeine+affect+sleep&brd_ai_mode=1"
```


## Support & Resources

- **Documentation:** [SERP API Docs](https://docs.brightdata.com/scraping-automation/serp-api/)
- **SEO Use Cases:** [SEO Tracking and Insights](https://brightdata.jp/use-cases/serp-tracking)
- **Other Guides:**
    - [SERP API](https://github.com/bright-jp/serp-api)
    - [Web Unlocker API](https://github.com/bright-jp/web-unlocker-api)
    - [Google Maps Scraper](https://github.com/bright-jp/Google-Maps-Scraper)
    - [Google News Scraper](https://github.com/bright-jp/Google-News-Scraper)
- **Interesting Reads:**
    - [Best SERP APIs](https://brightdata.jp/blog/web-data/best-serp-apis)
    - [Build a RAG Chatbot with SERP API](https://brightdata.jp/blog/web-data/build-a-rag-chatbot)
    - [Scrape Google Search with Python](https://brightdata.jp/blog/web-data/scraping-google-with-python)
- **Technical Support:** [Contact Us](mailto:support@brightdata.com)