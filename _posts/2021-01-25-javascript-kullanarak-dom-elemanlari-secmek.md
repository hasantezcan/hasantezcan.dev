---
layout: post
title: "JavaScript kullanarak DOM elemanlarını seçmek"
author: "Hasan Tezcan"
categories: blog
tags: [javascript]
image: "/DOM-selector.png"
date:   2020-01-25
---

> Bu yazı Kodluyoruz **2021 Earlybird Frontend Bootcamp'ı** sürcinde Kodluyoruz ekibinin hazırladığı video serisi için hazırlanmış bir yazılı kaynaktır. 

Bu yazıda [DOM (Document Object Model)](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) içerisinden öğeleri seçmek için kullanacağımız metotlardan bahsedeceğim.Document Object Model'de öğeler birden fazla yöntem ile seçilebilir. Birinci yöntemimiz olan element id'sini kullanarak şeçme metodu ile başlayalım.

## Get Element By ID
> **Elemanı ID'sine göre şeçmek**

`document` objesinin `getElementById()` metodu ile sayfada bulunan html elementlerinin ID'leri referans alarak seçme işlemi yapabiliyoruz. Örnek olarak;

```html
<div id="unicorn">🦄</div>
```
sayafada bulana bu elementi `getElementById()` methodunu kullanarak seçmeye çalışalım.

```js
const unicorn = document.getElementById('unicorn');
```

ID'ler büyük-küçük harf duyarlıdır. Bu sayede HTML document içinde biriçiklik gösterir ve her zaman geriye bir eleman döndürür. Bir eşleşme bulamazsa da geriye `null` dönüşünü yapar.

> **DİKKAT:** Seçmek istediğiniz elemanın id'sini yazarken eleman isminin başına **`# işaretini`** yazmanıza gerek yoktur. Yazmanız durumunda id'yi seçemeyeceksinizdir. 

```diff
- document.getElementById('#root'); // null
+ document.getElementById('root'); // <div id=​"root">​…​</div>​
```

## Get Elements By Tag Name
> **Elemanları etiket isimlerine göre şeçmek**

`getElementsByTagName()` metodu birden çok element'e ulaşmak amacı ile kullanılır.
Girdi olarak bir **html element'i** alır ve buna uygun bir HTMLCollection döndürür. Örneğin elimizde bu şekilde bir sayfa var;

```html
<p>🐱</p>
<p>🐰</p>
<p>🐯</p>
<p>🐧</p>
```

Bu sayfadaki tüm **p** elemanlarına ulaşmak istersek;

```js
const animals = document.getElementsByTagName('p'); 
// Çıktı:  HTMLCollection(4) [p, p, p, p]
```

yazmanız yeterli olcaktır.

> Ayrıca sayfadaki tüm etiketleri bu şekilde getirebilirsiniz.

```js
document.getElementsByTagName('*')
// Çıktı: HTMLCollection(33) [html, head, meta, link#.....
```

## Get Elements By Name
> Elemanları isimlerine göre getirme

`getElementsByName()` methodu elemanların **name** değerlerine göre bir [NodeList objesi](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) döndürür.

```html
<input type="text" name="e-posta">
<input type="tel" name="telefon">
<input type="date" name="tarih">
```
E-posta adıni taşıyan tüm öğeleri getirelim.

```js
const emails = document.getElementsByName('e-posta');
// Çıktı: NodeList [input]
```

> **Unutmayınki name değeri id'de olduğu gibi birick bir değer taşımaz birden fazla eleman aynı name değerini taşıyabilir.**

## Get Elements By Class Name
> **Elemanları class isimlerine göre şeçmek**

DOM'da istediğimiz class name'i taşıyan tüm elemanları seçmek için `getElementsByClassName()` methodunu kullanırız. Bu method bize bir **HTMLCollection** döndürür. Ve kullanırken class isminin başına **nokta "."** koyMAMAnız gerekir.

```html
<div class="baykuş kusu">🦉</div>
<div class="güvercin kusu">🐦</div>
<div class="kartal kusu">🦅</div>
<div class="kedi">🐱</div>
```
Hadi sayfamızdaki tüm kuşları seçelim;

```js
const kuslar = document.getElementsByClassName('kusu');
// Çıktı: HTMLCollection(3) [div.baykuş.kusu, div.güvercin.kusu, div.kartal.kusu]
```

Ayrıca bu methodla birden fazla class name belirtip **daha detaylı** bir seçim yapabilirsiniz.

```js
document.getElementsByClassName('kartal kusu');
// Çıktı: HTMLCollection [div.kartal.kusu]
```

## Query Selector
> **Tekil Sorgu seçici**

`QuerySelector ()` yöntemi, CSS seçicilere dayalı olarak DOM'dan html elemanlarını seçmenize izin veren iki modern JavaScript yönteminden biridir.
Bu yöntem ile birlikte hem css class'larını hem de id'lerini kullanabilirsiniz.
Bunu yaparken class için ön ek olarak **nokta "."**, id'ler için **kare "#"** kullanmanız gerekir. Sayfada **eşleşen ilk elemanı** size döndürecektir. Belirtilen elemanın eşleşememesi durumunda geriye `null` dönecektir.

```js
const email = document.querySelector('#signup input[name="email"]');
```

## Query Selector All
> **Çoğul Sorgu seçici**

**`querySelectorAll()` methodu,** `QuerySelector ()` methodu ile aynı mantık ile çalışır tek farkı eşeleşen ilk elamanı döndürmek yerine eşeleşen **tüm elemanları** bir NodeList objesi olark döndürmesidir.

```js
const elems = document.querySelectorAll('.bird, .animal');
console.log(elems.length); // 4
```

### Methoları bir arada kullanabilirsiniz
Yukarda öğrendiğimiz methodları birarada kullanabiliryoruz. Önce tek bir elemanı seçerek ardından içinde ikinci bir sorugu yapabiliyoruz. Örneğin;

```html
<form id="signup">
    <input type="text" name="email">
    <input type="tel" name="phone">
    <input type="date" name="date-of-birth">
</form>
```
sigup id'li elemanın içindeki tüm input elemanlarını seçmek istersek;

```js
const inputs = document.getElementById('signup').getElementsByTagName('input');
```

ya da 

```js
const inputs = document.querySelector('#signup').querySelectorAll('input');
```


### Alıştırmalar
Bu konu ile ilgili alıştırma yapmak isterseniz doğrudan tarayıcı üzerinden herhangi bir sitede inspect mod'undaki console'da anlatılan methodlar ile denemeler yapabilirsiniz. Ya da [bu linkten](https://www.w3resource.com/javascript-exercises/javascript-dom-exercises.php) alıştırmalar yapabilirsiniz.

## Sonuç
DOM üzerinden javaScript kullanarak eleman seçmek için gereken tüm methodları bu yazı boyunca öğrenmiş olduk. İhtiyacınız olan her şey buradaydı. Gerisi sizin uygun sorguları yazarak elemanlarınızı seçmenizde. Alıştırma yapmayı unutmayın. 👋👋👋


---

> ### Kaynakça
> - https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model
> - https://developer.mozilla.org/en-US/docs/Web/API/Document_object_model/Locating_DOM_elements_using_selectors
> - https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector
> - https://attacomsian.com/blog/getting-dom-elements-javascript