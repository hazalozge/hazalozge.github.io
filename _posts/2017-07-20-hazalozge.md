---
layout: post
title: "Json'da requests post ve get metodlarını inceleyelim"
date: 2017-07-20
---

JSON'da requests post ve get metodlarını inceleyelim.

GET ve POST kısaca http’de kullanılan metodlardır. HTML altında bir form oluşturduğunuzda bu form default haliyle GET istekeleri üretir. Eğer formunuzun POST istekleri üretmesini isterseniz bunu form tagınızın altında method özelliği ile belirtirsiniz.

Peki tam olarak GET ve POST metodlarının farkı nedir?

Bu iki method ile istekleri Python kullanarak nasıl gönderebiliriz?

Staj yaptığım yerde rast geldiğim bir olay üzerine kısaca araştırdığım bu soruların cevapları bu günkü yazımın başlıca konusu haline gelecek.

JSON:
Öncelikle... Json nedir?
JSON:
"JSON, programlama dilinden bağımsız olan Xml'e alternatif olarak kullanılan javascript tabanlı veri değişim formatıdır. JSON'un amacı veri alış verişi yaparken daha küçük boyutlarda veri alıp göndermektir.Bu özellikleri sayesinde JSON ile çok hızlı web uygulamaları oluşturabilir."

```python
{
   "tur":"met.l",
   "grup":"System of a Down"
}
```
Requests modülünün .json() özelliği tam da bunun için. Yukarıda GET parametresinden bahsetmiştik. Burda küçük bir kod parçacığı ile json'u decode edebiliyoruz
```python
import requests
r = requests.get('https://api.github.com/events')
r.json()
[{'type': 'CreateEvent', 'id': '5226537554', 'actor': {'id': 12762300, 'gravatar_id': '', ...
```
diye başlayıp uzuuunca devam eden bir metin döndürdü gördüğünüz gibi.
Ayrıca, json kütüphanesi ile de beraber kullanılabilir.
```python
import json
import requests
url = "https://api.github.com/some/endpoint"
hckn0 = {'some': 'data'}
r.requests.post(url, data=json.dumps(hckn0))
r = requests.post(url, data=json.dumps(hckn0))
print(r.text)
{"message":"Not Found","docu_mentation_url":"https://developer.github.com/v3"}
```
POST:
Post istekleri genellikle url'de görünmesini istemediğimiz zamanlarda kullanılır. Misal "get" metodunda yazdığımız veriler adres çubugunda gösterilirdi fakat POST'da gösterilmez.
Yani misalen web geçmişinde, önceki bir sitenin adres çubuğunda bilgilerimizin görünmesini engeller.
```python
payl = {'key1': 'value1', 'key2': 'value2'}
r = requests.post("http://httpbin.org/post", data=payl)
print(r.text)
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "key1": "value1", 
    "key2": "value2"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Content-Length": "23", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.13.0"
  }, 
  "json": null, 
  "origin": "62.248.25.231", 
  "url": "http://httpbin.org/post"
}
```
Peki aynısını GET ile yapsaydık ne olacaktı?
```python
r = requests.get("http://httpbin.org/post", data=payl)
print(r.text)
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<title>405 Method Not Allowed</title>
<h1>Method Not Allowed</h1>
<p>The method is not allowed for the requested URL.</p>
```
Farkı gördünüz değil mi? işte POST metodu tam da burada yardımıza koşuyor.

