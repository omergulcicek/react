<h1>JSX Nedir?</h1>

Böyle bir değişken tanımladığımızı düşünün:

```js
const element = <h1>Merhaba Dünya!</h1>;
```

Bu string yada HTML değildir.

Buna JSX denir, JavaScript için bir syntax uzantısıdır.

JSX, React elementleri üretir. Bir sonraki bölümde bunları DOM'a render etmeyi keşfedeceğiz.

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
  return <h1>Merhaba yabancı!</h1>;
}
```

<h2>JSX ile Attribute Belirlemek</h2>
String ifadeleri attribute olarak belirtmek için tırnak işaretleri kullanabilirsiniz:

```js
const element = <div tabIndex="0"></div>;
```

Bir attribute'e JavaScript ifadesi yerleştirmek için süslü parantezleri de kullanabilirsiniz:

```js
const element = <img src={kullacini.profilURL}></img>;
```
Bir attribute'e JavaScript ifadesi yerleştirirken süslü parantezler arasına tırnak işareti koymayın. Tırnak işaretleri string değerler için ve süslü parantezler ise JavaScript ifadeleri için kullanmanız gerekir. Her ikisi birden aynı attribute'te kullanılamaz.

>**Uyarı:**
>
>JSX JavaScript'e HTML'den daha yakın olduğundan ReactDOM, HTML nitelik adları yerine `camelCase` adlandırma kuralını kullanır.
>
>Örneğin JSX'te `class` yerine `className`, `tabindex` yerine `tabIndex` kullanılır.

<h2>JSX ile Çocukların Belirtilmesi</h2>

Bir etiket boşsa (<i>çocuk içermiyorsa manasında</i>), XML gibi hemen `/>` ile kapatabilirsiniz:

```js
const element = <img src={kullanici.profilURL} />;
```

JSX etiketleri çocuk içerebilir:

```js
const element = (
  <div>
    <h1>Merhaba!</h1>
    <h2>Seni burada görmek güzel.</h2>
  </div>
);
```

<i>JSX elementindeki ana kapsayıcının içindeki ifadeler `çocuk` olarak adlandırılır. Örneğin, üstteki ifadede `<div>` ana kapsayıcısının içerisinde bulunan `<h1>` ve `<h2>` etiketleri çocuk olarak adlandırılır.</i>

<h2>JSX, Enjeksiyon Saldırılarını Önler</h2>

Input'tan gelen içeriği JSX'e yerleştirmek güvenlidir:

```js
const baslik = yanit.inputtanGelenKotuNiyetliGiris;
// bu güvenlidir:
const element = <h1>{baslik}</h1>;
```

Varsayılan olarak React DOM, JSX'in içindeki herhangi bir değeri değişkene atmadan önce ifadeyi unicode'a çevirir. Böylece, uygulamanızda açıkça yazılmamış bir şeyi hiçbir zaman enjekte edememenizi sağlar. İşlenmeden önce her şey bir string'e dönüştürülür. Bu, XSS saldırılarını önlemeye yardımcı olur.

<i>Örneğin `&` ifadesi `&amp;`, `<` ifadesi `&lt;`, `>` ifadesi `&gt;`, `"` ifadesi `&quot;`, `'` ifadesi `&#39;` şekline dönüşecektir. Böylece input üzerinden XSS saldırısı yapmaya kalkılsa bile yazılan kod tamamen string'e dönüşmüş olduğundan etkisiz olacaktır.</i>

<h2>JSX Nesneleri Temsil Eder</h2>

Babel, JSX'i `React.createElement()` çağrılarına derlemektedir.

<i>Yani bizim yazdığımız tüm JSX ifadeleri <a href="https://babeljs.io/">Babel</a> tarafından derlenerek saf JavaScript'in anlayacağı şekilde objelere dönüşür.</i>

Bu iki örnek aynıdır:

```js
const element = (
  <h1 className="selamlama">
    Merhaba Dünya!
  </h1>
);
```

```js
const element = React.createElement(
  'h1',
  {className: 'selamlama'},
  'Merhaba Dünya!'
);
```

`React.createElement()` hatasız kod yazmanıza yardımcı olmak için birkaç kontrol gerçekleştirir ancak aslında böyle bir nesne oluşturur:

```js
// Not: Bu yapı basitleştirilmiştir
const element = {
  type: 'h1',
  props: {
    className: 'selamlama',
    children: 'Merhaba Dünya!'
  }
};
```

Bu nesneler React elementleri olarak adlandırılır. Bunları, ekranda görmek istediğiniz şeyin açıklaması olarak düşünebilirsiniz. React, bu nesneleri okur, onları DOM'u oluşturmak ve güncel tutmak için kullanır.

<a href="https://omergulcicek.github.io/reactjs/elementleri-render-etmek">Sıradaki Eğitim: Elementleri Render Etmek</a>
