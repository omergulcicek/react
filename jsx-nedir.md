<h1>JSX Nedir?</h1>

Böyle bir değişken tanımladığımızı düşünün:

```js
const element = <h1>Merhaba Dünya!</h1>;
```

Bu string yada HTML değildir.

Buna JSX denir, JavaScript için bir syntax uzantısıdır.

JSX, React elementleri üretir. Bir sonraki bölümde bunları <a href="">DOM'a render etme</a>yi keşfedeceğiz. (<i>İlgili sayfa anlatıldığında bu kısma link eklenecektir</i>).

Başlamanız için gerekli olan JSX'in temel bilgilerine aşağıdan erişebilirsiniz.

<h2>Neden JSX?</h2>

React, olayların nasıl işlendiğini, durumun zaman içinde nasıl değiştiğini kontrol eder ve bunları arayüze aktarır.

React yazmak için JSX'i kullanmak zorunda değilsiniz.
Fakat yazım şekli HTML'i andırdığı için kolayca alışacak ve hızlıca kod yazabileceksiniz.
Ayrıca React'in daha kullanışlı hata ve uyarı mesajları göstermesine izin verir.

O halde JSX yazmaya başlayalım!

<h2>İfadeleri JSX'e Yerleştirmek</h2>

Herhangi bir JavaScript ifadesini JSX'de süslü parantez içine sarmalayarak yerleştirebilirsiniz.

<i>Örneğin; { 2 + 2 }, { kullanici.ad } ve { adSoyad(kullanici) } gibi sayısal işlem, obje, değişken, fonksiyon vb kullanabilirsiniz.</i>

```js
function adSoyad(kullanici) {
  return kullanici.ad + ' ' + kullanici.soyad;
}

const kullanici = {
  ad: "Ömer",
  soyad: "Gülçiçek"
};

const element = (
  <h1>
    Merhaba, {adSoyad(kullanici)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById("root")
);
```

<a>CodePen'de Deneyin</a>


<h2>İfadeleri JSX'e Yerleştirmek</h2>

Derleme sonrasında, JSX ifadeleri JavaScript işlevi haline gelir.

Yani, if deyimleri ve döngüler içinde JSX'i kullanabilir ayrıca bir fonksiyondan JSX return edebiliriz.

```js
function karsila(kullanici) {
  if (kullanici) {
    return <h1>Merhaba {adSoyad(kullanici)}!</h1>;
  }
  return <h1>Merhaba yabancı</h1>;
}
```
