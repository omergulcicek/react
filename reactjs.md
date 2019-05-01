<h1>Ömer Gülçiçek</h1>

<h2>React Js Dokümanı</h2>

<a href="https://github.com/omergulcicek/reactjs">github.com/omergulcicek/reactjs</a>

Tüm Türkçe dokümanlar için: <a href="https://turkcedokuman.com/">turkcedokuman.com</a>

Bu pdf 21 Eylül 2018 tarihinde hazırlanmıştır.

---

<h1>React JS Kurulumu</h1>

Online olarak katılmayı deneyin ya da local geliştirme ortamınızı oluşturun.

<h2>Online Kod Ortamı</h2>

React'i online kod ortamında denemek istiyorsanız, <a href="https://codepen.io/omergulcicek/pen/ypMLXP">CodePen</a> ya da <a href="https://codesandbox.io/s/new">CodeSandbox</a> sitelerini kullanabilirsiniz.

<h2>React HTML Şablonu</h2>

Kendi text editörünüzü kullanmayı tercih ederseniz, <a href="https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html">bu HTML dosyasını</a> indirebilir, düzenleyebilir ve tarayıcınızdaki local dosya sisteminden açabilirsiniz. Kod dönüştürmesini yavaş yapar, bu nedenle sadece öğrenme aşamasında kullanın, projeleriniz için kullanmayın.

<h2>Hızlı Başlangıç</h2>

React kavramlarına adım adım bir giriş için <a href="https://omergulcicek.github.io/react/merhaba-dunya">hızlı başlangıç bölümü</a>ne gidin.

Bir örnek üzerinden eğitim için <a href="https://omergulcicek.github.io/react/xox-oyunu">uygulamalı eğitim bölümü</a>nü deneyin.

<h2>Geliştirme Ortamı</h2>

Yukarıdaki hafif çözümler, React'a yeni başladıysanız ya da denemek için en uygun yöntemlerdir.

<i>React JS'i bilgisayarınıza kurup, localinizde proje geliştirmeye başlamak istiyorsanız aşağıdaki adımları inceleyin.</i>

>  Not:
>
>  Olası uyumsuzluk sorunlarını önlemek için tüm React paketleri aynı sürümü kullanmalıdır. (`react`, `react-dom` vs.)

<h2>NodeJS Kurulumu</h2>

<i><a href="https://nodejs.org/en/">NodeJS</a> sitesine girip aşağıda görüldüğü gibi soldaki butona tıklayıp nodejs'i indiriyoruz.</i>

<img src="https://i.hizliresim.com/1Jn00N.png">

<i>Ardından klasik kurulumu tamamladıktan sonra <b>Node.js command prompt</b> programını çalıştırıp, kurulumlarımızı bu konsol üzerinden yapacağız.</i>

Yeni bir React projesine başlamak için en kolay yol, bir başlangıç kiti kullanmaktır.

<i>React ekibi tarafından önerilen çeşitli başlangıç kitleri bulunmakta; <a href="https://github.com/facebookincubator/create-react-app">Create React App</a>, <a href="https://learnnextjs.com/">Next.js</a>, <a href="https://www.gatsbyjs.org/">Gatsby</a>, <a href="https://github.com/insin/nwb">nwb</a>, <a href="https://github.com/jaredpalmer/razzle">razzle</a>, <a href="https://neutrino.js.org/">Neutrino</a>. React projesi başlatmak için resmi olarak desteklenen Create React App'ı detaylı açıklayalım.</i>

<h2>Create React App</h2>

<a href="https://github.com/facebookincubator/create-react-app">Create React App</a>, yeni bir React single page application'a başlamanın en iyi yoludur. Geliştirme ortamınızı, en yeni JavaScript özelliklerini kullanabilmenizi, güzel bir geliştirici deneyimi yaşamanızı ve uygulamanızı üretim için optimize etmenizi sağlar. NodeJS 6 veya daha üst sürümünün bilgisayarınızda kurulu olması gerekir (<i>Sunucuda gerekli değildir</i>).

<i>Create React App'i özetlemek gerekirse bu, React uygulamaları oluşturmanız için ihtiyacınız olan birçok şeyi içerisinde barındıran bir pakettir.</i>

İçerisine neler dahil edilmiştir?
* React, JSX, ES6, Flow syntax desteği
* Autoprefixed CSS ile otomatik olarak düzeltilen CSS'ler (-webkit veya diğer ön eklere gerek yoktur)
* Genel hatalar konusunda uyaran bir canlı geliştirme sunucusu
* Kod üzerinde yaptığımız değişiklikleri kaydettiğimiz anda arayüze yansıması için hot reloading
* JavaScript kod standartlarına uygun yazmanız için ESLint vs

<i>İlk olarak nodejs kurup, ardından aşağıdaki adımları gerçekleştirerek ilk uygulamamızı oluşturmaya başlayalım.</i>

```sh
npm install -g create-react-app
```

<img src="https://i.hizliresim.com/Yg5RZE.png">

<i>Ardından `my-app` adında bir proje oluşturuyoruz.</i>

```sh
create-react-app my-app
```

<i>Kurulum başarılı olduğunda aşağıdaki gibi bir çıktı ile kaşılacaksınız.</i>

<img src="https://i.hizliresim.com/XPYpAO.png">

Eğer npm 5.2.0+ sürümü yüklüyse, bunun yerine <a href="https://www.npmjs.com/package/npx">npx</a> kullanabilirsiniz.

```sh
npx create-react-app my-app
```

Bu komutlar geçerli klasörde `my-app` isimli bir dizin oluşturacaktır.
Bu dizinin içinde, proje yapısını oluşturacak ve geçişli bağımlılıkları kuracaktır.

<i>Projenin klasör yapısı aşağıdaki gibi olacaktır. Yapılandırma veya karmaşık klasör yapıları yok, sadece uygulamanızı oluştururken gereken dosyaları içerir.</i>

```
my-app
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   └── favicon.ico
│   └── index.html
│   └── manifest.json
└── src
    └── App.css
    └── App.js
    └── App.test.js
    └── index.css
    └── index.js
    └── logo.svg
    └── registerServiceWorker.js
```

<i>Kurulum tamamlandıktan sonra aşağıdaki komutlar ile proje klasörünüze girebilirsiniz. Ardından `npm start` ya da `yarn start` komutu ile projenizi localde açabilirsiniz.</i>

```sh
cd my-app
npm start
```

<i>Otomatik olarak localhost sayfası açılacaktır. Kodda değişiklik yaparsanız, sayfa otomatik olarak yeniden yüklenir. Konsolda ise hata uyarılarını görürsünüz. Kod yazmaya başlamak için `src/App.js` dosyasını düzenleyin ve kaydedin.</i>

<h2>Projeyi Build Etmek</h2>

<i>Kodunuzu yazdınız ve sunucunuza yüklemek istiyorsunuz, o halde `npm run build` komutu ile üretim için gerekli klasörler hazırlanır. React'ı düzgün bir şekilde paketler ve yapıyı en iyi performans için optimize eder. CSS ve JavaScript kodlarını minified eder (sıkıştırır) ve rastgele isimlendirir.</i>

```sh
npm run build
```

<i>Oluşturulan `build` klasörünün içerisindeki dosyaları sunucunuza atarak test edebilirsiniz.</i>

---

<h1>Merhaba Dünya</h1>

React'i kullanmanın en kolay yolu, <a href="https://codepen.io/omergulcicek/pen/ypMLXP">CodePen'deki bu Merhaba Dünya örnek kodu</a>nu kullanmaktır.

Herhangi bir şey yüklemenize gerek yoktur (<i>React JS, React DOM ve Babel eklenmiştir</i>).
Dokümantasyonu farklı bir sekmede açıp codepen üzerinden kodları test edebilirsiniz.

Yerel bir geliştirme ortamı kullanmayı tercih ediyorsanız <a href="https://omergulcicek.github.io/react/reactjs-kurulumu">kurulum sayfası</a>nı inceleyin.

En küçük React örneği şuna benzer:

```js
ReactDOM.render(
  <h1>Merhaba Dünya!</h1>,
  document.getElementById('root')
);
```

<i>Bu kod, HTML'de <b>root</b> id'li etiket içerisine <b>h1</b> başlığı ile Merhaba Dünya yazacaktır.</i>

Bundan sonraki bölümlerde, React aşamalı olarak anlatılacaktır. React uygulamalarının yapı taşları olan element ve componentleri inceleyeceğiz.

Component konusuna hakim olduktan sonra, küçük ve yeniden kullanılabilir parçalardan karmaşık uygulamalar oluşturabilirsiniz.

<h2>JavaScript ile ilgili bir not</h2>

React bir JavaScript kütüphanesidir. Bu nedenle JavaScript dilini temel düzeyde bilmeniz gerekiyor.

Kendinizi yeterli görmüyorsanız <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript">JavaScript bilgilerinizi yenilemenizi öneririz</a>,
böylece konuları daha kolay anlayabilirsiniz.


<i>Ek kaynaklar;</i>
<a href="https://www.w3schools.com/js/">w3schools</a>,
<a href="https://www.codecademy.com/learn/introduction-to-javascript">codecademy</a>,
<a href="https://www.youtube.com/results?search_query=javascript+dersleri">youtube</a>


---

<h1>JSX Nedir?</h1>

Böyle bir değişken tanımladığımızı düşünün:

```js
const element = <h1>Merhaba Dünya!</h1>;
```

Bu string ya da HTML değildir.

Buna JSX denir, JavaScript için bir syntax uzantısıdır.

JSX, React elementleri üretir. Bir sonraki bölümde bunları DOM'a render etmeyi keşfedeceğiz.

<i>DOM'a render etmek, yazdığınız React kodunun derlenip HTML'e yerleştirilme işlemine denir. Bir sonraki sayfada detaylıca anlatılacaktır.</i>

Başlamanız için gerekli olan JSX'in temel bilgilerine aşağıdan erişebilirsiniz.

<h2>Neden JSX?</h2>

React, olayların nasıl işlendiğini, durumun zaman içinde nasıl değiştiğini kontrol eder ve bunları arayüze aktarır.

React yazmak için JSX'i kullanmak zorunda değilsiniz.
Fakat yazım şekli HTML'i andırdığı için kolayca alışacak ve hızlıca kod yazabileceksiniz.
Ayrıca React'in daha kullanışlı hata ve uyarı mesajları göstermesine izin verir.

O halde JSX yazmaya başlayalım!

<h2>Javascript ifadelerini JSX'e Yerleştirmek</h2>

Herhangi bir JavaScript ifadesini JSX'de süslü parantez içine sarmalayarak yerleştirebilirsiniz.

<i>Örneğin; `{ 2 + 2 }`, `{ user.firstName }` ve `{ formatName(user) }` gibi sayısal işlem, obje, değişken, fonksiyon vb kullanabilirsiniz.</i>

```js
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Ömer',
  lastName: 'Gülçiçek'
};

const element = (
  <h1>
    Merhaba, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

<a href="https://reactjs.org/redirect-to-codepen/introducing-jsx">CodePen'de Deneyin</a>

<h2>Fonksiyonları JSX'e Yerleştirmek</h2>

Derleme sonrasında, JSX ifadeleri JavaScript fonksiyonları haline gelir.

Yani, if deyimleri ve döngüler içinde JSX'i kullanabilir ayrıca bir fonksiyondan JSX return edebiliriz.

```js
function getGreeting(user) {
  if (user) {
    return <h1>Merhaba {formatName(user)}!</h1>;
  }
  return <h1>Merhaba yabancı.</h1>;
}
```

<h2>JSX ile Attribute Belirlemek</h2>
String ifadeleri attribute olarak belirtmek için tırnak işaretleri kullanabilirsiniz:

```js
const element = <div tabIndex="0"></div>;
```

Bir attribute'e JavaScript ifadesi yerleştirmek için süslü parantezleri de kullanabilirsiniz:

```js
const element = <img src={user.avatarUrl}></img>;
```
Bir attribute'e JavaScript ifadesi yerleştirirken süslü parantezler arasına tırnak işareti koymayın. Tırnak işaretleri string değerler için ve süslü parantezler ise JavaScript ifadeleri için kullanmanız gerekir. Her ikisi birden aynı attribute'te kullanılamaz.

>**Uyarı:**
>
>JSX JavaScript'e HTML'den daha yakın olduğundan ReactDOM, HTML nitelik adları yerine `camelCase` adlandırma kuralını kullanır.
>
>Örneğin JSX'te `class` yerine `className`, `tabindex` yerine `tabIndex` kullanılır.

<h2>JSX ile Child Belirlemek</h2>

Bir etiket boşsa (<i>child içermiyorsa manasında</i>), XML gibi hemen `/>` ile kapatabilirsiniz:

```js
const element = <img src={user.avatarUrl} />;
```

JSX etiketleri child içerebilir:

```js
const element = (
  <div>
    <h1>Merhaba!</h1>
    <h2>Seni burada görmek güzel.</h2>
  </div>
);
```

<i>JSX elementindeki ana kapsayıcının içindeki ifadeler `child` (çocuk) olarak adlandırılır. Örneğin, üstteki ifadede `<div>` ana kapsayıcısının içerisinde bulunan `<h1>` ve `<h2>` etiketleri child olarak adlandırılır.</i>

<h2>JSX, Enjeksiyon Saldırılarını Önler</h2>

Input'tan gelen içeriği JSX'e yerleştirmek güvenlidir:

```js
const title = response.inputtanGelenKotuNiyetliGiris;
// bu güvenlidir:
const element = <h1>{title}</h1>;
```

Varsayılan olarak React DOM, JSX'in içindeki herhangi bir değeri değişkene atmadan önce ifadeyi unicode'a çevirir. Böylece, uygulamanızda açıkça yazılmamış bir şeyi hiçbir zaman enjekte edememenizi sağlar. İşlenmeden önce her şey bir string'e dönüştürülür. Bu, XSS saldırılarını önlemeye yardımcı olur.

<i>Örneğin `&` ifadesi `&amp;`, `<` ifadesi `&lt;`, `>` ifadesi `&gt;`, `"` ifadesi `&quot;`, `'` ifadesi `&#39;` şekline dönüşecektir. Böylece input üzerinden XSS saldırısı yapmaya kalkılsa bile yazılan kod tamamen string'e dönüşmüş olduğundan etkisiz olacaktır.</i>

<h2>JSX Nesneleri Temsil Eder</h2>

Babel, JSX'i `React.createElement()` çağrılarına derlemektedir.

<i>Yani bizim yazdığımız tüm JSX ifadeleri <a href="https://babeljs.io/">Babel</a> tarafından derlenerek saf JavaScript'in anlayacağı şekilde objelere dönüşür.</i>

Bu iki örnek aynıdır:

```js
const element = (
  <h1 className='greeting'>
    Merhaba Dünya!
  </h1>
);
```

```js
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Merhaba Dünya!'
);
```

`React.createElement()` hatasız kod yazmanıza yardımcı olmak için birkaç kontrol gerçekleştirir ancak aslında böyle bir nesne oluşturur:

```js
// Not: Bu yapı basitleştirilmiştir
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Merhaba Dünya!'
  }
};
```

Bu nesneler React elementleri olarak adlandırılır. Bunları, ekranda görmek istediğiniz şeyin açıklaması olarak düşünebilirsiniz. React bu nesneleri okur, onları DOM'u oluşturmak ve güncel tutmak için kullanır.

---

<h1>Elementleri Render Etmek</h1>

Elementler React uygulamalarının en küçük yapı taşlarıdır.

Bir element, ekranda görmek istediğiniz şeyi tanımlar:

```js
const element = <h1>Merhaba Dünya</h1>;
```
Tarayıcı DOM elementlerinden farklı olarak, React elementleri düz nesnelerdir ve oluşturulması kolaydır.
React DOM, React elementleriyle eşleşecek şekilde DOM'u güncellemekle ilgilenir.

<i>Bu konu hakkında detaylı Türkçe bilgi için <a href="https://fatihacet.com/react-ve-virtual-dom-mimarisi-uzerine">Fatih Acet'in makalesi</a>ne göz atabilirsiniz.</i>

>**Not:**
>
>Daha yaygın olarak bilinen component kavramıyla elementler karıştırılabilir.
>Bir sonraki bölümde componentleri tanıtacağız.

<i>Elementleri birer değişken, componentleri ise fonksiyon olarak düşünebilirsiniz; birbirinden farklı şeylerdir.</i>

<h2>Bir Elementi DOM'a Render Etmek</h2>

HTML dosyanızda bir `<div>` olduğunu varsayalım:

```html
<div id="root"></div>
```

Buna root DOM düğümü diyoruz çünkü içindeki her şey React DOM tarafından yönetilecektir.

<i>DOM düğümü hakkında detaylı bilgi için <a href="https://www.w3schools.com/js/js_htmldom_navigation.asp">JavaScript HTML DOM Navigation</a> içeriğini inceleyenilirsiniz.</i>

Sadece React ile oluşturulmuş uygulamalar genellikle tek bir root DOM düğümüne sahiptir.

React'i mevcut bir uygulamaya entegre ediyorsanız, istediğiniz kadar çok sayıda ayrı root DOM düğümü olabilir.

React elementini bir root DOM düğümüne dönüştürmek için, her ikisini de `ReactDOM.render()` işlevine yerleştirin.

```js
const element = <h1>Merhaba Dünya!</h1>;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

<a href="http://codepen.io/gaearon/pen/rrpgNB?editors=1010">CodePen'de Deneyin</a>

Sayfanızda "Merhaba Dünya!" başlığı görüntülenecektir.

<h2>Oluşturulan Bir Elementi Güncellemek</h2>

React elementleri değişmez. Bir element oluşturduktan sonra, elementin alt elementlerini veya attributelerini değiştiremezsiniz.

<i>Konu hakkında detaylı bilgi için </i><a href="https://medium.com/codefiction/i%CC%87pin-ucunu-ka%C3%A7%C4%B1rmamak-redux-8d822da0d19b">Onur Aykaç'ın yazdığı makale</a><i>de <b>Javascript’te immutable ve mutable kavramı</b> bölümünü okuyabilirsiniz.</i>

Bildiğimiz kadarıyla UI'ı güncellemenin tek yolu yeni bir element oluşturmak ve `ReactDOM.render()` fonksiyonuna geçirmektir.

Aşağıdaki saat örneğini inceleyelim.

```js
function tick() {
  const element = (
    <div>
      <h1>Merhaba Dünya!</h1>
      <h2>Saat şu anda {new Date().toLocaleTimeString()}</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

<a href="http://codepen.io/gaearon/pen/gwoJZk?editors=0010">CodePen'de Deneyin</a>

`ReactDOM.render()` fonksiyonunu her saniye setInterval() içerisinden çağırır.

>**Not:**
>
>Pratikte React uygulamalarının çoğu, bir kez `ReactDOM.render()` elementini çağırır.
>
>Birbiriyle bağlantı kurduğu için konuları atlamadan okumaya devam edin.

<i>Yukarıdaki saat örneğinde `setInterval` fonksiyonu sayesinde her saniye fonksiyon çağırılır ve ReactDOM render edilir.
Fakat pratikte bu kodlar bu şekilde yazılmıyor. ReactDOM bir kez render edilir ve oluşturulan elementler `state`ler yardımıyla güncellenir.
İlerleyen konularda bunlara değineceğiz.</i>

React DOM, componenti ve child (<i>çocuk</i>) componentleri önceki componentle karşılaştırır ve DOM'u istenen duruma getirmek için gereken yerlerde DOM güncellemelerini uygular.

<i>Yani, React DOM tüm componentleri yeniden yüklemez. Değişiklik olan yeri algılar ve DOM üzerinde sadece o kısmı günceller, buda performansı olumlu yönde etkiler.</i>

Tarayıcı üzerinden bu örneği inceleyerek doğrulayabilirsiniz.

<img src="https://reactjs.org/granular-dom-updates-c158617ed7cc0eac8f58330e49e48224.gif" alt="react dom örneği">

---

<h1>Component ve Props</h1>

Componentler, uygulamanızı tekrar kullanılabilir parçalara ayırmanıza ve her bir parçayı ayrı ayrı düşünmenize izin verir.

Kavramsal olarak, componentler JavaScript fonksiyonlarına benzemektedir.

Bunlar rasgele girdileri (`props` olarak adlandırılır) kabul eder ve ekranda neler görüneceğini açıklayan React elementleri return ederler.

<i>Sitenizi büyük bir puzzle olarak düşünün. React ile önce teker teker puzzle parçalarını oluşturup ardından bunları birleştirerek büyük resmi oluşturacaksınız.</i>

<h2>Fonksiyonel ve Class Componentleri</h2>

Bir componenti tanımlamanın en basit yolu, bir JavaScript fonksiyonu yazmaktır:

```js
function Welcome(props) {
  return <h1>Merhaba {props.name}</h1>;
}
```
Bu fonksiyon geçerli bir React componenti olduğundan, tek bir `props` parametresini obje olarak alır ve bir React componenti return eder.

Bu componenti "fonksiyonel" olarak adlandırırız çünkü tam anlamıyla JavaScript fonksiyonudur.

Bir componenti tanımlamak için bir ES6 sınıfı da kullanabilirsiniz:
(<i>ES6 hakkında detaylar eklenecektir.</i>)

```js
class Welcome extends React.Component {
  render() {
    return <h1>Merhaba {this.props.name}</h1>;
  }
}
```

Yukarıdaki iki component, React'in bakış açısından eşittir.

Class'ların sonraki bölümlerde göreceğimiz bazı ek özellikleri var.
O zamana kadar componentleri en saf hallerini kullanacağız.

<i>İlerleyen konularda class'lar içerisine constructor, props, state ve çeşitli fonksiyonlar dahil olacak.
Fakat konuyu dağıtmamak adına class'ları yukarıdaki en saf halleriyle kullanmaya devam edelim.</i>

<h2>Componentleri Render Etmek</h2>

Daha önce yalnızca DOM etiketlerini temsil eden React elementleriyle karşılaştık:

```js
const element = <div />;
```

Bununla birlikte, elementler componentleri de temsil edebilir:

```js
const element = <Welcome name="Ömer" />;
```

React, kullanıcı tanımlı bir componenti temsil eden bir element görürse, JSX attributelerini tek bir obje olarak bu componente aktarır. Bu objeye `props` diyoruz.

<i>Yani bir componente `<Welcome name="Ömer" surname="Gülçiçek" job="Yazılım Mühendisi" />` gibi
birden çok attribute eklediğimiz zaman, React bunları aşağıdaki gibi tek bir objede toplar, buna `props` denir.
Ardından bu props objesini `Welcome` componentine parametre olarak gönderir.
`Hosgeldin` componentinde `props.name` kullanım şekli ile "Ömer" değerini çekebiliriz.</i>

```html
<Welcome name="Ömer" surname="Gülçiçek" job="Yazılım Mühendisi" />

props = {
   name: "Ömer",
   surname: "Gülçiçek",
   job: "Yazılım Mühendisi"
}
```

Örneğin, bu kod sayfaya "Merhaba Ömer" başlığını yazar:

```js
function Welcome(props) {
  return <h1>Merhaba {props.name}</h1>;
}

const element = <Welcome name="Ömer" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

<a href="https://reactjs.org/redirect-to-codepen/components-and-props/rendering-a-component">CodePen'de Deneyin</a>

Bu örnekteki olayları aşama aşama inceleyelim:

1. `ReactDOM.render()` fonksiyonundan `<Welcome name='Ömer' />` elementini çağırırız.

2. React, `Welcome` componentine parametre olarak `{name: 'Ömer'}` objesini alır.

3. `Welcome` componenti `<h1>Merhaba Ömer</h1>` elementini return eder.

4. React DOM, DOM'u `<h1>Merhaba Ömer</h1>` olacak şekilde günceller.

>**Uyarı:**
>
>Component adlarını daima büyük harfle başlatın.
>
>Örneğin, `<div />` bir DOM etiketini temsil eder ama `<Welcome />` bir componenti temsil eder.

<h2>Componentleri Oluşturmak</h2>

Component çıktılarında başka componentlere başvurabilir.
Bu, herhangi bir componenti farklı şekillerde kullanmamızı sağlar.
Bir buton, bir form, bir diyalog, bir ekran: React uygulamalarında, hepsi genel olarak component olarak ifade edilir.

Örneğin, `Welcome`'i birçok kez çağıran bir `App` componenti oluşturabiliriz:

```js
function Welcome(props) {
  return <h1>Merhaba {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Ömer" />
      <Welcome name="Muhammed" />
      <Welcome name="Burak" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

<a href="https://reactjs.org/redirect-to-codepen/components-and-props/composing-components">CodePen'de Deneyin</a>

Genelde, React uygulamalarında tek bir `App` componenti çağrılır.
Bununla birlikte, React'ı varolan bir uygulamaya entegre ederseniz,
`Buton` gibi küçük bir component ile iç componentten dışa doğru kodlamaya başlayabilir ve görünüm hiyerarşisinin en üst noktasına yavaş yavaş ilerleyebilirsiniz.

Bu örnekteki olaylarıda aşama aşama inceleyelim:

1. `ReactDOM.render()` ilk olarak `<App />` componentini çağırdı.

2. `<App />` componenti ise 3 tane `<Welcome />` componenti return edecek. Fakat `<Welcome />` componentine parametre olarak farklı objeler yollanmış.

3. İlk `<Welcome />` componenti ekrana `Merhaba Ömer` yazacak. Ardından tekrar `<Welcome />` componenti çağrılacak fakat bu sefer objedeki ad Muhammed, son olarakta Burak olacak.

4. Sonuç olarak ekranda bir `div` içerisinde `Merhaba Ömer`, `Merhaba Muhammed` ve `Merhaba Burak` yazan başlıklar yazdırılacaktır.

<h2>Componentleri Parçalamak</h2>

Componentleri daha küçük componentleri bölmekten korkmayın.

Örneğin, bu `Yorum` componentini düşünün:

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

<a href="https://reactjs.org/redirect-to-codepen/components-and-props/extracting-components">CodePen'de Deneyin</a>

`author` (obje), `text` (string) ve `date` (date) props olarak kabul eder ve bir yorum divi return eder.

Bu component, iç içe birçok componenti olduğu için değiştirilmesi zor olabilir, bu yüzden componenti parçalayarak küçük componentler oluşturalım.

İlk olarak `Avatar` componentini oluşturalım:

```js
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```

Ardından `Comment` componentinin içerisinden, yeni oluşturduğumuz `Avatar` componentini çağıralım.

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

Ardından, `UserInfo` componentini ayıklayacağız:

```js
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}
```

Şimdide `Comment` componentinin nasıl görüldüğüne bakalım.

```js
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

<a href="https://reactjs.org/redirect-to-codepen/components-and-props/extracting-components-continued">CodePen'de Deneyin</a>

Componentleri küçük parçalara bölmek başlangıçta gereksiz bir iş ya da zaman kaybı gibi gözükebilir, ancak daha büyük uygulamalarda tekrar kullanılabilir component paletine sahip olmak önemlidir.

<h2>Propslar Yalnızca Okunabilir</h2>

Bir component (fonksiyon veya class) oluşturduğunuzda, kendi propslarını hiçbir zaman değiştirmemelisiniz.
Bir `sum` fonksiyonu düşünün:

```js
function sum(a, b) {
  return a + b;
}
```

Bu fonksiyonlara `pure` (saf) denir çünkü parametrelerini değiştirmeye çalışmazlar ve aynı parametreler için aynı sonuca her zaman return edilir.

Buna karşın, bu fonksiyon kendi parametresini değiştirdiği için saf değildir:

```js
function withdraw(account, amount) {
  account.total -= amount;
}
```

React oldukça esnektir fakat tek bir katı kuralı vardır:

Tüm React componentleri, propslar ile ilgili olarak saf fonksiyonlar gibi hareket etmelidir.

Elbette uygulama arayüzü dinamiktir ve zaman içinde değişecektir.
Bir sonraki bölümde `state` kavramı tanıtılacaktır.
State, React componentlerine, kullanıcı eylemlerine ve diğer herhangi bir şeye bu kuralı ihlal etmeden değerlerin değiştirmesine izin verir.

<i>Özet olarak, propsları asla değiştirmeye kalkmıyoruz. Propslar sadece okunabilir. Bir sonraki bölümde state kavramı işlenecektir.
Propslar state'lerden değeri çekecek, değeri değiştirmek istediğimizde state'i değiştireceğiz. Haliyle propsta değişmiş olacak.</i>

---

<h1>State ve Lifecycle</h1>

<a href="https://github.com/omergulcicek/reactjs/blob/master/elementleri-render-etmek.md">Önceki konularda</a> gördüğümüz
saat örneğini düşünün.

Şu ana kadar UI'ı güncellemenin tek bir yolunu öğrendik.

Görüntülenen çıktıyı değiştirmek için `ReactDOM.render()` fonksiyonunu her saniye çağırıyorduk:

```js
function tick() {
  const element = (
    <div>
      <h1>Merhaba Dünya!</h1>
      <h2>Saat şu anda {new Date().toLocaleTimeString()}</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

<a href="http://codepen.io/gaearon/pen/gwoJZk?editors=0010">CodePen'de Deneyin</a>

Bu bölümde, `Clock` componentini yeniden kullanımının doğru yöntemini öğreneceğiz.

Zamanlayıcıyı kendisi ayarlayacak ve her saniyede bir güncelleme yapacaktır.

`Clock` componentinin nasıl göründüğünü yazmakla başlayabiliriz:

```js
function Clock(props) {
  return (
    <div>
      <h1>Merhaba Dünya!</h1>
      <h2>Saat şu anda {props.date.toLocaleTimeString()}</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

<a href="http://codepen.io/gaearon/pen/dpdoYR?editors=0010">CodePen'de Deneyin</a>

<i>Daha önce anlatılmıştı fakat tekrar etmekte fayda var.
`Clock` componenti çağrılırken attribute olarak `date={new Date()}` gönderiliyor.
Bu attribute, `Clock` componentine parametre olarak gelir ve adı `props`tur.
`Clock` componentine bu tarihi yazdırmak içinde `props.date` şeklinde kullanıyoruz.</i>

Bunu bir kez yazmak ve `Clock` component güncellemesini kendisi gerçekleştirsin isteriz:

```js
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

Bunu uygulamak için `Clock` componentine `state` eklemeliyiz.
Stateler propslara benzer, ancak tamamen component tarafından kontrol edilir.
Daha önce belirttiğimiz gibi, class olarak tanımlanan componentlerin bazı ilave özellikler var.
State yalnızca classlar için kullanılabilen bir özelliktir.

<h2>Bir Fonksiyonun Class'a Dönüştürülmesi</h2>

<i>Bu kısıma kadar componentleri fonksiyon olarak tanımlamıştık.
Fakat React'ta class olarak oluşturmaya alışmak daha doğru olacaktır.
Şimdi adım adım bir fonksiyonun class'a çevrilme işlemini inceleyelim.</i>

`Clock` fonksiyon componentini aşağıdaki adımlarla class componentine dönüştürebiliriz.

1. `React.Component`ine extend eden aynı ada sahip bir ES6 classı oluşturalım. (<i>`class Clock extends React.Component`</i>)

2. Buna `render()` adı verilen boş bir fonksiyon ekleyin.

3. Fonksiyonun içerisindeki kodları `render()`ın içerisine taşıyın.

4. `props`un adını `this.props` olarak değiştirin.

```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.props.date.toLocaleTimeString()}/h2>
      </div>
    );
  }
}
```

<a href="http://codepen.io/gaearon/pen/zKRGpo?editors=0010">CodePen'de Deneyin</a>

<i>Fonksiyon component yerine class component kullanımına alışın.
Üst kısımdaki adımları anlamadıysanız tekrar tekrar okumanızda fayda var.</i>

`Clock` componenti bir fonksiyon yerine bir class olarak tanımlanmış oldu.

Bu, `state` ve `lifecycle` (yaşam döngüsü) gibi ek özellikleri kullanmamızı sağlar.

<h2>Bir Class'a State Eklemek</h2>

Bir class'a state eklemek için aşağıdaki 3 adımı dikkatlice inceleyiniz.

1. `this.props.date` satırını `this.state.date` olarak güncelleyin:

```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.date.toLocaleTimeString()}</h2>
      </div>
    );
  }
}
```

2. Class componentimizin içerisine state'i ilk anda tanımlayan bir constructor oluşturalım.

<i>Constructor fonksiyonu, bir classla beraber oluşturulan, nesnenin oluşturulması ve başlatılması için özel bir fonskiyondur. Bir classta "constructor" ismiyle yalnızca bir tane özel fonskiyon olabilir. Class oluşturulduğu anda içerisindeki kodlar çalışır.</i>

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.date.toLocaleTimeString()}</h2>
      </div>
    );
  }
}
```

`props`un constructorden nasıl alındığına dikkat ediniz:

<i>`constructor`e parametre olarak `props` ekleyip, içerisine `super(props);` satırını ekliyoruz.</i>

```js
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```

Class componenleri her zaman constructore `props` ile çağırmalıdır.
`<Clock />` componentinden `date` attribute'ünü kaldırın:

```js
ReactDOM.render(
  //eski hali = <Clock date={new Date()} />
  <Clock />,
  document.getElementById('root')
);
```

Zamanlayıcı kodunu daha sonra componentin kendisine geri ekleyeceğiz.

Şu anda sonuç şöyle görünüyor:

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.date.toLocaleTimeString()}</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

<a href="http://codepen.io/gaearon/pen/KgQpJd?editors=0010">CodePen'de Deneyin</a>

Şimdi, `Clock`i kendi zamanlayıcısını oluşturup her saniyede bir güncelleyeceğiz.

<h2>Bir Classa Lifecycle Fonksiyonları Ekleme</h2>

Birçok componente sahip uygulamalarda, componentler yok edildiğinde alınan kaynakları boşaltmak çok önemlidir.

`Clock`, DOM'a ilk defa çağırıldığında bir zamanlayıcı ayarlamak istiyoruz. Buna React'te `mounting` denir.

Ayrıca, Saat componentinden üretilen DOM kaldırıldığında,
bu <a href="https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/clearInterval">zamanlayıcıyı temizlemek</a> istiyoruz.
Buna ise React'te `unmounting` denir.

Bir component DOM'a yazdırılıp kaldırıldığında bazı kod satırlarını çalıştırmak için class componente özel yöntemler ekleyebiliriz:

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    //Component oluşturulduğunda çalışacak fonksiyon
  }

  componentWillUnmount() {
    //Component kaldırıldığında çalışacak fonksiyon
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.date.toLocaleTimeString()}</h2>
      </div>
    );
  }
}
```

Bu fonksiyonlara `lifecycle hooks` (yaşam döngüsü kancaları) adı verilir.

Component çıktısı DOM'a aktarıldıktan sonra `componentDidMount()` fonksiyonu çalışır.
Bu, zamanlayıcı ayarlamak için iyi bir yerdir:

```js
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
```

<i>`() => this.tick()` kullanımı `ES6` ile gelen kısa fonksiyon kullanımıdır.

`ES5`'teki kullanımı `function() { return this.tick();` }</i>

Zamanlayıcı `this`in üzerine nasıl kaydettiğimizi unutmayın.

Zamanlayıcıyı `componentWillUnmount()` fonksiyonunda temizleyeceğiz:


```js
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
```

Son olarak, `Clock` componentini her saniyede bir çalışacağı `tick()` adında bir fonksiyon oluşturacağız.

Bu fonksiyon state'eki tarihi `this.setState()` kullanarak güncelleyecektir.

<i>Daha önceki konularda `props`ların yalnızca okunabilir olduğunu ve güncellenmemesi gerektiğinin notunu düşmüştük.
Bizler (`this.setState()` ile) `state`'i değiştireceğiz, React ise o state'i kullanan yerleri (`props`ları) kendisi güncelleyecek.</i>

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  //Fonksiyon tanımlarken başına "function" yazmadığımıza dikkat edin.
  //React componentleri içerisinde fonksiyon tanımlamak istediğimizde direkt isim vererek yazıyoruz.
  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.date.toLocaleTimeString()}</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

<a href="http://codepen.io/gaearon/pen/amqdNA?editors=0010">CodePen'de Deneyin</a>

Neler olup bittiğini hızla özetleyelim:

1) `ReactDOM.render()` içerisinde `<Clock />` componenti çağırıldığında, React `Clock` componentinin constructorünü çağırır.
`Clock` componentinin geçerli saati göstermesi gerektiği için `this.state`'i geçerli saat ile başlatır.
Daha sonra bu state güncellenecek.

2) React sonra `Clock` componentinin `render()` fonksiyonunu çağırır.
React, ekranda neyin görüntülenmesi gerektiğini öğrenir.
Daha sonra, `Clock` componentinin çıktısı ile eşleşecek şekilde DOM'u güncelleştirir.

3) `Clock` componentinin çıktısı DOM'a eklendiğinde, React, `componentDidMount()` fonksiyonunu çağırır.
Her saniye çalışacak olan `tick()` fonksiyonunu `timerID`de tutar.

4) Her saniye tarayıcı `tick()` fonksiyonunu çağırır.
`Clock` componentinin içinde, geçerli saati içeren bir nesneyle `setState()`i çağırarak bir UI güncellemesi için`setInterval()` fonksiyonunu hazırlar.
`setState()` çağrısı sayesinde React, statin değiştiğini bilir ve ekranda ne olması gerektiğini öğrenmek için tekrar `render()` eder.
Bu sefer `render()` yöntemindeki `this.state.date` güncellenmiş olacaktır. React DOM'u buna göre günceller.

5) `Clock` componenti DOM'dan kaldırıldıysa, React, `timerID` durduğu anda `componentWillUnmount()` fonksiyonunu çağırır.

<h2>State'i Doğru Kullanmak</h2>

`setState()` hakkında bilmeniz gereken üç şey vardır.

<h5>State'i Doğrudan Değiştirmeyin</h5>

Örneğin, bu bir componenti yeniden oluşturmaz:

```js
// Yanlış Kullanım
this.state.comment = 'Merhaba';
```

`setState()`i şu şekilde kullanın:

```js
// Doğru Kullanım
this.setState({comment: 'Merhaba'});
```

`this.state`i atayabileceğiniz tek yer `constructor`dür.

<h5>State Güncellemeleri Asenkron Olabilir</h5>

React, birden fazla `setState()` çağrısını performans için tek bir güncelleme haline getirebilir.

Çünkü `this.props` ve `this.state` eşzamansız olarak güncellenebilir.

Örneğin, bu sayaç güncellemesi başarısız olabilir:

```js
// Yanlış Kullanım
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

Bunu düzeltmek için, bir objeden ziyade bir fonksiyonu kabul eden ikinci bir `setState()` formunu kullanın.
Bu işlev önceki durumu ilk argüman olarak, güncelleme ikinci argüman olarak uygulandığında sahne alacaktır:

```js
// Doğru Kullanım
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
```

<i>Yukarıdaki örnekte ES6 ile gelen ok fonksiyonu kullandık fakat normal fonksiyonlarla da yapabilirdik:</i>

```js
// Doğru Kullanım
this.setState(function(prevState, props) {
  return {
    counter: prevState.counter + props.increment
  };
});
```

<h5>State'leri Toplu Güncelleştirmek</h5>

`setState()` öğesini çağırdığınızda, React state'i birleştirir. Bu yüzden birden fazla state aynı anda güncellenebilir.


```js
constructor(props) {
  super(props);
  this.state = {
    posts: [],
    comments: []
  };
}
```

Ayrıca bunları ayrı `setState()` çağrılarıyla bağımsız olarakta güncelleyebilirsiniz:

```js
componentDidMount() {
  fetchPosts().then(response => {
    this.setState({
      posts: response.posts
    });
  });

  fetchComments().then(response => {
    this.setState({
      comments: response.comments
    });
  });
}
```

<i>`setState`i kullandığımızda tüm state'ler değiştirilmez. Yalnızca belirtilen state güncellenir.
Yani `this.setState({comments})` şeklinde kullanıldığında sadece `this.state.comments` güncellenir, `this.state.posts` güncellenmez.</i>

---

<h1>Click ve Change Olayları</h1>

React elementleri ile click ve change gibi olayları izlemek, DOM elementlerindeki olayları işlemekle çok benzerdir.

<i>Click, change gibi olaylara `event` denir.
Tam liste için <a href="https://www.w3schools.com/jsref/dom_obj_event.asp">tıklayınız</a>.
Daha akılda kalıcı olması ve ağırlıklı olarak `click` ve `change` olayları kullanıldığı için
başlıktada `event olayları` yerine `click ve change olayları` başlığını kullandım.</i>

Bazı syntax farklılıkları vardır:

* React eventleri, küçük harf yerine `camelCase` kullanılarak isimlendirilir.

<i>camelCase'den daha öncede bahsetmiştik.
İlk kelime hariç diğer kelimelerin ilk harfleri büyük ve birleşik yazılır. Arada - (tire) kullanılmaz.
React'te `class` yerine `className`, `tabindex` yerine `tabIndex`, `onclick` yerine `onClick`, `onchange` yerine `onChange` kullanılır.</i>)

* JSX ile bir string yerine event işleyicisi olarak bir fonksiyon iletirsiniz.

Örneğin, HTML'de:

```html
<button onclick="activateLasers()">
  Linki aktifleştir
</button>
```

React'te ise biraz farklıdır:

```html
<button onClick={activateLasers}>
  Linki aktifleştir
</button>
```

Başka bir fark ise React'te varsayılan davranışı engellemek için `false` return etmektir.
`preventDefault`'u açıkça çağırmalısınız.
Örneğin, düz HTML'de yeni bir sayfayı açmanın varsayılan bağlantı davranışını önlemek için şunları yazabilirsiniz:

```html
<a href="#" onclick="console.log('Bağlantıya tıklandı.'); return false">
  Tıkla
</a>
```

React'te bunun yerine:

```js
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('Bağlantıya tıklandı.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Tıkla
    </a>
  );
}
```

Burada, `e` sentetik bir olaydır.
React, bu sentetik olayları <a href="https://www.w3.org/TR/DOM-Level-3-Events">W3C spesifikasyonu</a>na göre tanımlar;
dolayısıyla tarayıcılar arası uyumluluk konusunda endişelenmenize gerek yoktur.

React'i kullanırken genellikle bir DOM elementi oluşturulduktan sonra, o elementin click eventini izlemek için
`addEventListener`i çağırmamamız gerekir.
Bunun yerine, element başlangıçta oluşturulduğunda bir click izleyicisi oluşturun.

Bir componenti ES6 classı kullanarak tanımladığınızda, ortak bir desen, bir olay işleyicisinin classtaki bir fonksiyon olmasını sağlar. Örneğin, bu `Toggle` componenti, kullanıcının "Açık" ve "Kapalı" durumları arasında geçiş yapmasını sağlayan bir buton oluşturur:


```js
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // Click, change gibi olayların çalışabilmesi için aşağıdaki gibi bind etmek gerekir.
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'Açık' : 'Kapalı'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

<a href="http://codepen.io/gaearon/pen/xEmzGg?editors=0010">CodePen'de Deneyin</a>

<i>Bind etmek ile ilgili detaylı bilgi için kendi yazığım <a href="https://omergulcicek.com/blog/bind-fonksiyonu">bind fonksiyonu</a> adlı makaleyi okuyabilirsiniz.</i>

JSX geriçağırımlarında bu konuda dikkatli olmalısınız. JavaScript'te, class fonskyionları varsayılan olarak bağlı değildir.
`this.handleClick`'i `bind` etmeyi (bağlamayı) unutursanız ve `onClick`e iletirseniz, fonksiyon çağrıldığında bu `undefined` olur.

Bu, React'e özgü davranış değildir; fonksiyonların JavaScript'te nasıl işlediğinin bir parçasıdır.
Genellikle, onClick = {this.handleClick} gibi bir yöntemin arkasından `()` olmadan işaret ederseniz, bu yöntemi bind etmeniz gerekir.

Bu şekilde bind etmek istemiyorsanız, iki farklı yolu daha vardır.

```js
class LoggingButton extends React.Component {
  // Bu syntax `this`'nin clickOlayi içinde bağlanmasını sağlar.
  // Uyarı: Bu *deneysel* bir syntaxtır.
  handleClick = () => {
    console.log(this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Tıkla
      </button>
    );
  }
}
```

Bu syntax <a href="https://github.com/facebookincubator/create-react-app">Create React App</a>'te varsayılan olarak etkindir.

Return işleminde bir ok fonksiyonu kullanabilirsiniz:

```js
class LoggingButton extends React.Component {
  handleClick() {
    console.log(this);
  }

  render() {
    // Bu syntax `this`'in bind edilmesini sağlar.
    return (
      <button onClick={(e) => this.handleClick(e)}>
        Tıkla
      </button>
    );
  }
}
```

Bu syntax ile ilgili sorun, `LoggingButton`un her işleyişinde farklı bir callback oluşturulmasıdır.
Çoğu durumda, bu iyidir.
Bununla birlikte bu callback, alt componentlere `props` olarak iletilirse, bu componentler ek bir yeniden oluşturma işleyebilir.
Genellikle, constructorde bind etmenizi öneririz.

<h2>Bağımsız Değişkenleri Event Olaylarına Aktarma</h2>

Bir döngü içinde, bir event olayına fazladan bir parametre göndermek isteyebilirsiniz.
Örneğin, `id` satır kimliğiyse, aşağıdakilerden herhangi biri işe yarayabilir:

```js
<button onClick={(e) => this.deleteRow(id, e)}>Satırı Sil</button>
<button onClick={this.deleteRow.bind(this, id)}>Satırı Sil</button>
```

Yukarıdaki iki satır eşittir, <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions">ok fonksiyonları</a>nı ve
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind">Function.prototype.bind</a>ı kullanır.

Her iki durumda da, React olayını temsil eden `e` argümanı id'den sonra ikinci bir parametre olarak aktarılır.
Bir ok fonskiyonu ile bunu açıkça belirtmeliyiz, ancak `bind` ile başka argümanlar otomatik olarak iletilir.

---

<h1>Şartlı Render</h1>

React ile ihtiyacınız olan davranışı kapsayan farklı componentler oluşturabilirsiniz.
Daha sonra, uygulamanızın state'ine bağlı olarak yalnızca bir kısmını görüntüleyebilirsiniz.

React'te şartlı render, JavaScript koşulları ile aynı şekilde çalışır.
Geçerli durumu temsil eden elemanlar oluşturmak için `if` veya koşullu operatör gibi JavaScript operatörlerini kullanın
ve bunları eşleştirmek için  UI'ı güncelleştirmeye izin verin.

Bu iki componenti düşünün:

```js
function UserGreeting(props) {
  return <h1>Tekrardan hoşgeldin!</h1>;
}

function GuestGreeting(props) {
  return <h1>Lütfen üye ol.</h1>;
}
```

Bir kullanıcının oturum açıp açmadığına bağlı olarak bu componentlerin herhangi birini görüntüleyen bir
`Greeting` componenti oluşturacağız:

```js
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // isLoggedIn={true} olarak değiştirip farkı test edebilirsiniz.
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/ZpVxNq?editors=0011">CodePen'de Deneyin</a>

<i>Adım adım incelemekte fayda var.

1. İlk olarak ReactDOM, `Greeting` componentini render ediyor.

2. Farkettiğiniz gibi componentin içerisinden props olacak bir `isLoggedIn={false}` değerini gönderiyor.

3. `Greeting` componentinde, parametre olarak gönderilen `boolean` (true ya da false) değeri bir değişkene atıyor.

4. Ardından bu değer true ise `UserGreeting` componentini, false ise `GuestGreeting` componentini return ediyor.</i>

<h2>Element Değişkenleri</h2>

Elementleri depolamak için değişkenleri kullanabilirsiniz.

Bu, koşullu olarak componentin bir bölümünü oluşturmanıza yardımcı olabilir, ancak çıktının geri kalanı değişmez.

`LoginButton` ve `LogoutButton` düğmelerini temsil eden bu iki yeni componenti inceleyelim:

```js
function LoginButton(props) {
  return (
    <button onClick={props.onClick}>
      Giriş Yap
    </button>
  );
}

function LogoutButton(props) {
  return (
    <button onClick={props.onClick}>
      Çıkış Yap
    </button>
  );
}
```

Aşağıdaki örnekte, `Greeting` adı verilen state'i olan component oluşturacağız.
Geçerli durumuna bağlı olarak `<LoginButton />` veya `<LogoutButton />` işlevlerini oluşturacaktır:

```js
class Greeting extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;

    let button = null;
    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <UserGreeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <Greeting />,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/QKzAgB?editors=0010">CodePen'de Deneyin</a>

Bir değişkeni bildirmek ve  `if` ifadesi kullanmak koşullu olarak bir componenti oluşturmak için iyi bir yoldur,
bazen daha kısa bir syntax kullanmak isteyebilirsiniz.
Aşağıda açıklanan, JSX'de koşulları sıralamanın birkaç yolu vardır.

<h2>&& Operatörü</h2>

Herhangi bir ifadeyi JSX'e süslü parantez içine sararak gömebilirsiniz.
Buna JavaScript mantıksal `&&` operatörü dahildir.
Koşullu olarak bir elementi dahil etmek için kullanışlı olabilir:

```js
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Merhaba!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          {unreadMessages.length} adet okunmamış mesajınız bulunmaktadır.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/ozJddz?editors=0010">CodePen'de Deneyin</a>

<i>JavaScript `true && ifade` olduğunda burada `ifade` kısmında yazacağımız kodu çalıştırır.
Yani `&&`nin sol tarafı true ise, sağ tarafını çalıştırır.

`false && ifade` durumunda ise `false` olarak değerlendirir.

Kısa if-else kullanımda `x = (x == 1) ? ++x` şeklinde kullanım yapamıyoruz.
Mutlaka `else` durumunuda yazmamız gerekiyor. Yani şu şekilde: `x = (x == 1) ? ++x : --x`

Fakat && operatörü ile else durumu olmadan kısa yoldan sadece `if` kontrolü yapmış oluyoruz.
</i>

<h2>If-Else Şartlı Operatörü</h2>

Koşullu olarak oluşturma yöntemi için bir başka yöntem de JavaScript if-else operatörünü kullanmaktır.

`ifade ? dogru : yanlis`

<i>Bu kullanım if { } else { }'in kısa kullanımıdır.
`ifade` olarak belirtilen yer eğer true ise `dogru` yazan yerdeki kod çalışır,
aksi taktirde ise `yanlis` yazan yerdeki kod çalışır.</i>

Aşağıdaki örnekte, if-else koşulunu küçük bir metin bloğu oluşturmak için kullanıyoruz.

```js
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      Kullanıcı siteye giriş <b>{isLoggedIn ? 'yaptı' : 'yapmadı'}</b>.
    </div>
  );
}
```

Bununla birlikte daha büyük ifadeler için de kullanılabilir, ancak kod karmaşıklaşır:

```js
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn ? (
        <LogoutButton onClick={this.handleLogoutClick} />
      ) : (
        <LoginButton onClick={this.handleLoginClick} />
      )}
    </div>
  );
}
```

Tıpkı JavaScript'te olduğu gibi, siz ve ekibiniz hangisinin daha okunabilir olduğunu düşünüyorsa o yöntemi kullanabilir.

<h2>Componentin Render Edilmesini Önlemek</h2>

Nadiren de olsa, bir component, başka bir component tarafından oluşturulmuş olsa bile gizlenmesini isteyebilir.
Bunu yapmak için `null` return etmek gereklidir.

Aşağıdaki örnekte, `<WarningBanner />` componenti, `warn` adlı props değerine bağlı olarak oluşturulmuştur.
Props değeri `false` ise, component oluşturmaz:

```js
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Uyarı!
    </div>
  );
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = {showWarning: true}
    this.handleToggleClick = this.handleToggleClick.bind(this);
  }

  handleToggleClick() {
    this.setState(prevState => ({
      showWarning: !prevState.showWarning
    }));
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? 'Gizle' : 'Göster'}
        </button>
      </div>
    );
  }
}

ReactDOM.render(
  <Page />,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/Xjoqwm?editors=0010">CodePen'de Deneyin</a>

Bir componenti `null` olarak `render` yöntemiyle return etmek, componentin lifecycle fonksiyonlarının başlatılmasını etkilemez.
Örneğin, `componentWillUpdate` ve `componentDidUpdate` yine de çağrılacaktır.

---

<h1>Listeler ve Keyler</h1>

Önce, JavaScript'te listeleri nasıl dönüştürdüğümüzü gözden geçirelim.
Aşağıdaki kod göz önüne alındığında, bir dizi sayı almak ve değerlerini ikiye katlamak için `map()` fonksiyonunu kullanıyoruz.
`map()` tarafından return edilen çift katlı değerleri kaydederiz:

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);
```

Konsola `[2, 4, 6, 8, 10]` yazacaktır.

<i>Google Chrome'da (diğer tarayıcılarda da benzer ya da aynıdır) <b>F12</b>'ye basıp,
"Console (yada Konsol)" sekmesine gelip bu kodları yapıştırarak test edebilirsiniz.

Ok fonksiyonları ile ilgili dokümantasyon hazırlandığında bu kısım güncellenecektir.
Kısaca özet geçmek gerekirse yukarıda map fonksiyonunun içerisinde yapılan işlem (`(number) => number * 2`) şudur:

`number` parametre alınır ve `number*2` return edilir.

Fonksiyonun kolay okunabilir hali ise şudur:
</i>

```js
function(number) {
  return number*2;
}
```

React'te, dizi elemanlarını listelere dönüştürmek neredeyse aynıdır.

<h2>Birden Çok Component Vermek</h2>

Koleksiyonları oluşturabilir ve bunları JSX içine süslü parantez `{}` kullanarak ekleyebilirsiniz.

Aşağıda, JavaScript `map()` fonksiyonu kullanarak numbers dizisinde döngü oluşturuyoruz.
Her liste için bir `<li>` return ediyoruz. Son olarak, elde edilen sonuç dizisini `listItems`e atayacağız:

```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
```

Bütün `listItems` dizesini `<ul>` elemanının içerisine dahil ediyoruz ve bunu DOM'a gönderiyoruz:

```javascript
ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/GjPyQr?editors=0011">CodePen'de Deneyin</a>

Bu kod, ekrana `ul` kapsayıcısı ve `li`ler içerisinde rakamları yazacaktır.

<h2>Temel Liste Componenti</h2>

Genellikle listeleri bir component içinde render ederiz.

Önceki örneği, `numbers` adında bir dizi kabul eden ve liste çıktısı yapan bir componente dönüştürebiliriz.

```javascript
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

Bu kodu çalıştırdığınızda, liste için bir `key` (anahtar) verilmesi yönünde bir uyarı verilir.

<i>Burada key kelimesine (Türkçe'si anahtar demek olmasına rağmen) anahtar çevirisi tam olarak uymuyor.
Key denirken aslında benzersizi ifade etmektedir (ID, Kimlik numarası, parmak izi gibi)</i>.

Bir `key`, listeleri oluşturulurken eklenmesi gereken özel bir attribute'tür.
Bir sonraki bölümde bunun neden önemli olduğunu anlatacağız.
`numbers.map()` içindeki listelere birer `key` atayalım.

```js
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/jrXYRR?editors=0011">CodePen'de Deneyin</a>

<h2>Keyler</h2>

`Key`ler yardımı ile hangi listenin değiştiğini, eklendiğini veya kaldırıldığını belirleyebiliriz.
Elemanlara istikrarlı bir kimlik kazandırmak için dizideki listelere `key` verilmelidir:

```js
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

Bir `key` seçmenin en iyi yolu, kardeşleri (<i>diğer `li`ler</i>) arasında bir tanımlanan bir kimlik kullanmaktır.
Çoğu zaman, verilerinizdeki id'ler `key` olarak kullanılır:

```js
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

Eğer bu tarzda bir yapınız yoksa benzersiz olacağı için `key`lere `index` verebiliriz:

```js
const todoItems = todos.map((todo, index) =>
  // Listelerin benzersiz id'leri yoksa bu yöntemi kullanın.
  <li key={index}>
    {todo.text}
  </li>
);
```

Listelerin sırası değişebilirse keyler için index kullanmanızı önermiyoruz.
Bu, performansı olumsuz etkileyebilir ve component state'i ile ilgili sorunlara neden olabilir.

Ayrıntılı bilgi için <a href="https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318">Robin Pokorny</a>'nin makalesini inceleyebilirsiniz (<i>İngilizce</i>).

Listelere siz key atamazsanız React varsayılan olarak index'i atar.

<h2>Keyler Yalnızca Kardeşleri Arasında Benzersiz Olmalıdır</h2>

Dizilerde kullanılan keyler kardeşleri arasında benzersiz olmalıdır.
Bununla birlikte, global olarak benzersiz olması gerekmez.

İki farklı diziyi üretirken aynı keyleri kullanabiliriz:

```js
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Merhaba Dünya', content: 'React Öğreniyoruz!'},
  {id: 2, title: 'Ömer Gülçiçek', content: 'React JS Türkçe Dokümantasyon'}
];
ReactDOM.render(
    <Blog posts={posts} />,
    document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/NRZYGN?editors=0010">CodePen'de Deneyin</a>

Keyler React'te bir ipucu işlevi görür ancak componentlere aktarılmazlar.
Componentlerde aynı değere ihtiyacınız varsa, açıkça farklı bir ada sahip bir props olarak iletebilirsiniz:

```js
const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);
```

Yukarıdaki örnekte, `Post` componenti `props.id`yi okuyabilir, ancak `props.key`i okuyamaz.

<h2>map() Fonksiyonunu JSX İçine Karıştırmak</h2>

Yukarıdaki örneklerde hep farklı bir `listItems` değişkeni tanımlayıp ve JSX'e dahil ettik:

```js
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

JSX, herhangi bir ifadeyi süslü parantez içine yerleştirmeye izin verir, böylece `map()` fonksiyonu ile sonucu sıralayabiliriz:

```js
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}
```

<a href="https://codepen.io/gaearon/pen/BLvYrB?editors=0010">CodePen'de Deneyin</a>

Bazen bu daha temiz koda neden olur, ancak bu stil de istismar edilebilir.
JavaScript'te olduğu gibi okunabilirlik açısından bir değişkenin çıkartılmaya değer olup olmadığına karar vermek size aittir.
Kod çok iç içe geçmişse, bir componenti ayıklamak için doğru zamanın geldiğini aklınızda bulundurun.

---

<h1>Formlar</h1>

HTML form elemanları, React'te diğer DOM elemanlarından biraz farklı çalışır, çünkü form elemanlarının kendilerine has iç stateleri vardır.
Örneğin, bu kod HTML'de bir form içerisinde `name` girişi ister:

```html
<form>
  <label>
    Adınız:
    <input type="text" name="name" />
  </label>
  <input type="submit" value="Gönder" />
</form>
```

<h2>Kontrollü Componentler</h2>

HTML'de, `<input>`, `<textarea>` ve `<select>` gibi form elemanları genellikle kendi state'ini korur ve kullanıcı girdisine dayalı olarak güncelleşir.
React'te ise state'ler genellikle componentlerin `this.state` özelliğinde saklanır ve yalnızca `setState()` ile güncellenir.

React state'te tek kaynak olarak ikisini birleştirebiliriz.
Ardından form oluşturan React componenti, sonraki kullanıcı girişi üzerinde bu formda olanı da kontrol eder.
Değeri React tarafından bu şekilde kontrol edilen bir giriş form elemanına `kontrollü component` denir.

Örneğin, bir önceki örnekte, `name` değerinin yazılıp submit edildiğinde `name`ı alert ile yazdırmak istiyorsak,
formu kontrollü bir component olarak oluşturabiliriz:

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Gönderilen değer: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Gönder" />
      </form>
    );
  }
}
```

<a href="https://codepen.io/gaearon/pen/VmmPgp?editors=0010">CodePen'de Deneyin</a>

<i>`value` attribute'ü input'un kendisinde zaten var.
Öyleyse bu değeri almak için yeni bir React state'i oluşturmaya gerek yok.
Bu inputta `value` olarak state'i yazdıracağız ve input'ta her değişiklik olduğunda bu state'i güncelleyeceğiz.</i>

Kontrollü bir componentte her state değişimi, `handleChange` fonksiyonunu çalıştıracaktır.
Örneğin, adın büyük harflerle yazılmasını isteseydik, `handleChange` fonksiyonunu şu şekilde yazabilirdik:


```javascript
handleChange(event) {
  this.setState({value: event.target.value.toUpperCase()});
}
```

<i>Buradaki `event.target` input'un ta kendisidir.

Bunu fonksiyon içerisinde `console.dir(event.target);` yazarak konsoldan doğrulayabilirsiniz.

Haliyle `event.target.value` ise o inputtaki değeri alacaktır.</i>

<h2>Textarea Tagı</h2>

HTML'de, `<textarea>` tagı yazıyı çocuğunda tanımlar:

<i>Yani yazılan yazı `input`ta olduğu gibi tagın kendisinde değil, tagın içerisindedir.</i>

```html
<textarea>
  Merhaba, burası textarea yazı alanıdır.
</textarea>
```

Bunun yerine React, `<textarea>`  için bir `value` attribute'ü kullanır.
Bu şekilde `<textarea>` kullanan bir form, tek satırlı bir girdi kullanan bir forma çok benzer şekilde yazılabilir:

```javascript
class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 'Bu kısma bir şeyler yazınız.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Gönderilen değer: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Essay:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Gönder" />
      </form>
    );
  }
}
```

`this.state.value`in constructor'te başlatıldığına dikkat edin, böylece `textarea` içerisinde varsayılan olarak bu yazı bulunacaktır.

<h2>Select Tagı</h2>

HTML'de `<select>`, bir açılır liste oluşturur. Örneğin, aşağıdaki kod bazı illeri listeler:

```html
<select>
  <option value="istanbul">İstanbul</option>
  <option value="ankara">Ankara</option>
  <option selected value="trabzon">Trabzon</option>
  <option value="izmir">İzmir</option>
</select>
```

`Trabzon` seçeneğinin başlangıçta `selected` attribute'ü yüzünden seçili olarak geleceğini unutmayın.
React, bu `selected` attribute'ünü kullanmak yerine,` select` etiketinde bir `value` attribute'ü kullanır.
Kontrollü bir componentte bu daha kullanışlıdır çünkü yalnızca bir yerde güncelleme yapmanızı sağlar. Örneğin:

```javascript
class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'Trabzon'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Hangi ilde yaşamak isterdiniz: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          En sevdiğiniz il:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="istanbul">İstanbul</option>
            <option value="ankara">Ankara</option>
            <option value="trabzon">Trabzon</option>
            <option value="izmir">İzmir</option>
          </select>
        </label>
        <input type="submit" value="Gönder" />
      </form>
    );
  }
}
```

<a href="https://codepen.io/gaearon/pen/JbbEzX?editors=0010">CodePen'de Deneyin</a>

Genel olarak bu, `<input type="text">`, `<textarea>` ve `<select>`  elementlerinin çok benzer şekilde çalışmasını sağlar.

> Not
>
> Bir `select` etiketinde birden fazla seçeneği seçmenize izin veren bir diziyi `value` attribute'üne yazabilirsiniz:
>
>```js
><select multiple={true} value={['B', 'C']}>
>```

<h2>File Input Tagı</h2>

HTML'de `<input type="file">` aygıt depolama alanından bir veya daha fazla dosya seçmenizi sağlar.

```html
<input type="file" />
```
React'te bir `<input type="file" />`, önemli bir farkla normal bir `<input />`a benzer şekilde çalışır: <b>read-only</b>'dir.

(<i>Yani yalnızca okunabilirdir, `props`lar gibi.</i>)

<h2>Çoklu Girişleri Ele Alma</h2>

Çoklu kontrollü `input` öğelerini ele almanız gerektiğinde,
her öğeye bir `name` özniteliği ekleyebilir ve işleyici işlevinin `event.target.name` değerine dayanarak ne yapılacağını seçmesine izin verebilirsiniz.

Örneğin:

```js
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```

<a href="https://codepen.io/gaearon/pen/wgedvV?editors=0010">CodePen'de Deneyin</a>

Verilen girdi ismine karşılık gelen state keyini güncellemek için ES6 syntax'ını nasıl kullandığımıza dikkat edin:


```js
this.setState({
  [name]: value
});
```

Buda ES5'teki eşdeğer kodudur.

```js
var partialState = {};
partialState[name] = value;
this.setState(partialState);
```

<h2>Kontrollü Giriş Boş Değer</h2>

Kontrollü bir component üzerindeki props'u belirlemek, kullanıcının isteği dışında girişi değiştirmesini önler.
`value` belirttiyseniz ancak girdi hala düzenlenebilir ise, yanlışlıkla `value`i ` undefined` veya `null` olarak ayarlamış olabilirsiniz.

Aşağıdaki kod bunu göstermektedir.
(Giriş ilk önce kilitlenir ancak kısa bir gecikme sonrasında düzenlenebilir hale gelir.)

```javascript
ReactDOM.render(<input value="merhaba" />, mountNode);

setTimeout(function() {
  ReactDOM.render(<input value={null} />, mountNode);
}, 1000);

```

---

<h1>State Güncellemek</h1>

Çoğu zaman, birden çok componentin aynı state'i yansıtması gerekir. Bu bölümde, suyun belirli bir sıcaklıkta kaynayıp kaynayamayacağını hesaplayan fonksiyonları oluşturacağız.

`BoilingVerdict` adlı bir componentle başlayacağız. `Celsius` sıcaklığını bir props ile parametre olarak kabul eder ve suyu kaynatmaya yetecek kadar olup olmadığını return eder:

```js
function BoilingVerdict(props) {
  if (props.celsius >= 100) {
    return <p>Su kaynar.</p>;
  }
  return <p>Suyun kaynaması için yeterli sıcaklık değil.</p>;
}
```

Sonra, `Calculator` adlı bir component oluşturacağız.

Sıcaklığı girmenizi sağlayıp, bu değeri `this.state.temperature`'te tutacak:

```js
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    return (
      <fieldset>
        <legend>Celsius sıcaklığını giriniz:</legend>
        <input value={temperature} onChange={this.handleChange} />
        <BoilingVerdict celsius={parseFloat(temperature)} />
      </fieldset>
    );
  }
}
```

<a href="https://codepen.io/gaearon/pen/ZXeOBm?editors=0010">CodePen'de Deneyin</a>

<h2>İkinci Inputu Eklemek</h2>

Şimdi yapacağımız şey ise Celsius inputuna ek olarak, bir Fahrenheit inputu sağlamak.

`TemperatureInput` componentinden devam edebiliriz.
Yeni bir `scale` propsu ekleyeceğiz ki bunlar `c` ya da `f` olabilirler:

```js
const scaleNames = {
  c: 'Celsius',
  f: 'Fahrenheit'
};

class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    const scale = this.props.scale;
    return (
      <fieldset>
        <legend>{scaleNames[scale]} sıcaklığını giriniz:</legend>
        <input value={temperature} onChange={this.handleChange} />
      </fieldset>
    );
  }
}
```

Artık iki ayrı sıcaklık girişi oluşturmak için `Calculator` componentini şu şekilde değiştirebiliriz:

```js
class Calculator extends React.Component {
  render() {
    return (
      <div>
        <TemperatureInput scale="c" />
        <TemperatureInput scale="f" />
      </div>
    );
  }
}
```

<a href="https://codepen.io/gaearon/pen/jGBryx?editors=0010">CodePen'de Deneyin</a>

Şu anda iki inputumuz var, ancak sıcaklıkların birine rakam yazdığımızda diğeri güncellenmiyor.
Bu bizim gereksinimimizle çelişiyor, onları senkronize etmeyi istiyoruz.

<h2>Dönüştürme Fonksiyonları</h2>

İlk olarak Celsius ve Fahrenheit'ı birbirine dönüştürmek için gerekli iki fonksiyonu yazacağız:

```js
function toCelsius(fahrenheit) {
  return (fahrenheit - 32) * 5 / 9;
}

function toFahrenheit(celsius) {
  return (celsius * 9 / 5) + 32;
}
```

Bu iki fonksiyon, sıcaklıkları birbirine dönüştürür.

<h2>State Güncellemek</h2>

Şu anda, `TemperatureInput` componenti bağımsız olarak değerlerini local state'te tutuyor:

```js
class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    // ...   
```

Bununla birlikte, bu iki inputun birbiriyle senkronize edilmesini istiyoruz.
Celsius inputu güncellendiğinde, Fahrenheit inputu dönüştürülen sıcaklığı göstermelidir; aynı zamanda tersi de çalışmalıdır.

React'ta state, ihtiyaç duyan componentlerin en yakın ortak atasına taşınarak gerçekleştirilir.

Bunun yerine, state'i `TemperatureInput`den çıkaracak ve onu `Calculator` içine taşıyacağız.

Bunun nasıl olduğunu adım adım işleyelim.

İlk olarak, `TemperatureInput` componentinde `this.state.temperature` öğesini `this.props.temperature` olarak değiştirelim.

```js
  render() {
    // Önceden: const temperature = this.state.temperature;
    const temperature = this.props.temperature;
    // ...
```

Propsların read-only (<i>sadece okunabilir, değiştirilemez</i>) olduğunu biliyoruz.
`temperature` state'teyken, `TemperatureInput` bunu değiştirmek için `this.setState()`yi çağırabilir.

Şimdi, `TemperatureInput` sıcaklığı güncellemek istediğinde, `this.props.onTemperatureChange` fonksiyonu yardımı ile yapacak:

```js
  handleChange(e) {
    // Önceden: this.setState({temperature: e.target.value});
    this.props.onTemperatureChange(e.target.value);
    // ...
```

>Not:
>
>`temperature` veya `onTemperatureChange` adlarının özel bir anlamı yoktur. Onlara, `value` ve `onChange` gibi isimler verdik, başka bir şey diyebilirdik.

```js
class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    this.props.onTemperatureChange(e.target.value);
  }

  render() {
    const temperature = this.props.temperature;
    const scale = this.props.scale;
    return (
      <fieldset>
        <legend>{scaleNames[scale]} sıcaklığını giriniz:</legend>
        <input value={temperature}
               onChange={this.handleChange} />
      </fieldset>
    );
  }
}
```

Şimdi `Calculator` componentine geçelim.
Mevcut inputun `temperature` ve `scale` değerlerini statede tutarız.

Örneğin, Celsius'a 37 yazarsak, `Calculator` componentinin state'i şöyle olacaktır:

```js
{
  temperature: '37',
  scale: 'c'
}
```

Eğer daha sonra Fahrenheit'ı 212 olarak değişirsek `Calculator` componenti şöyle olur:

```js
{
  temperature: '212',
  scale: 'f'
}
```

Her ikisinin girdisinide tutabilirdik fakat gereksiz olurdu.
En son girilen girdinin değerini ve gösterdiği ölçeği tutmak yeterlidir.
Daha sonra `temperature` ve `scale` değerlerine bağlı olarak diğerinin değerini hesaplayabiliriz.

```js
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleCelsiusChange = this.handleCelsiusChange.bind(this);
    this.handleFahrenheitChange = this.handleFahrenheitChange.bind(this);
    this.state = {temperature: '', scale: 'c'};
  }

  handleCelsiusChange(temperature) {
    this.setState({scale: 'c', temperature});
  }

  handleFahrenheitChange(temperature) {
    this.setState({scale: 'f', temperature});
  }

  render() {
    const scale = this.state.scale;
    const temperature = this.state.temperature;
    const celsius = scale === 'f' ? tryConvert(temperature, toCelsius) : temperature;
    const fahrenheit = scale === 'c' ? tryConvert(temperature, toFahrenheit) : temperature;

    return (
      <div>
        <TemperatureInput
          scale="c"
          temperature={celsius}
          onTemperatureChange={this.handleCelsiusChange} />

        <TemperatureInput
          scale="f"
          temperature={fahrenheit}
          onTemperatureChange={this.handleFahrenheitChange} />

        <BoilingVerdict
          celsius={parseFloat(celsius)} />
      </div>
    );
  }
}
```

<a href="https://codepen.io/gaearon/pen/WZpxpz?editors=0010">CodePen'de Deneyin</a>

Şu anda, hangi inputun düzenlediğiniz önemli değil, Calculator'daki `this.state.temperature` ve `this.state.scale` güncellenir. Inputlardan bir tanesi olduğu gibi değeri alır, diğer input değeri daima buna dayalı olarak yeniden hesaplanır.

<img src="https://reactjs.org/react-devtools-state-ef94afc3447d75cdc245c77efb0d63be.gif" alt="Monitoring State in React DevTools">

---

<h1>Composition ve Inheritance</h1>

React'ın güçlü bir modeli var ve componentler arasında kodu tekrar kullanmak için
`inheritance` (<i>miras</i>) yerine `composition` (<i>birleşim</i>) kullanılmasını öneriyoruz.

Bu bölümde, React'e yeni gelen geliştiricilerin genellikle inheritance ile ilgili karşılaştığı birkaç sorunu ele alacağız
ve bunları compositionlarla nasıl çözebileceğimizi göstereceğiz.

<h2>Containment (Kapsama)</h2>

Bazı componentler önceden çocuklarını bilmezler.

Bu, genel kutuları temsil eden `Sidebar` veya `Dialog` gibi componentler için özellikle geçerlidir.

Bu tür componentlerin, çocuklarını doğrudan çıktılarına yerleştirmek için `children` kullanmalarını öneriyoruz:

<i>Bildiğiniz gibi, `props` sayesinde o componente tüm attributeleri alıyorduk.
`props.children` dediğimizde ise o componente yerleştirilmiş child (çocuk) componentleri/içeriği (vb) alıyoruz.</i>

```js
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}
```

<i>Yukarıdaki `FancyBorder` componenti bir `div` return ediyor.
Bu div ise props ile `color`ı parametre olarak alacak.</i>

<i>Alttaki `WelcomeDialog` componenti ise `FancyBorder` componentini return ediyor ve renk olarakta `blue` gönderilmiş.</i>

```js
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Hoşgeldiniz
      </h1>
      <p className="Dialog-message">
        Bu dokümantasyonu starlayarak destek olabilirsiniz!
      </p>
    </FancyBorder>
  );
}
```

<a href="https://codepen.io/gaearon/pen/ozqNOV?editors=0010">CodePen'de Deneyin</a>

`<FancyBorder>` JSX etiketinin içindeki herhangi bir şey `children` olarak `FancyBorder` componentine geçirilir.

Aşağıdaki yöntem daha az yaygındır, ancak bazen kullanılabiliyor.
Bu gibi durumlarda `children` kullanmak yerine kendi yöntemlerinizi hazırlayabilirsiniz:

```js
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
```

<a href="https://codepen.io/gaearon/pen/gwZOJp?editors=0010">CodePen'de Deneyin</a>

<i>Burada atrribute olarak `SplitPane` componentine `left` ve `right` propslarına component gönderilmiştir.
Propslar ile bir yazı, rakam, değişken, component gibi her hangi bir şeyi gönderebilirsiniz.</i>

<h2>Uzmanca Kod</h2>

Bazen componentleri, diğer componentlerin "özel durumları" olarak düşünürüz.

React'te bu, daha "özel" bir componentin daha "jenerik" bir component oluşturduğu ve props ile yapılandırdığı composition ile elde edilir:

```js
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog
      title="Hoşgeldiniz"
      message="Bu dokümantasyonu starlayarak destek olabilirsiniz!" />
  );
}
```

<a href="https://codepen.io/gaearon/pen/kkEaOZ?editors=0010">CodePen'de Deneyin</a>

Aşağıdaki daha karışık olan örneği inceleyerek anlamaya çalışın:

```js
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
      {props.children}
    </FancyBorder>
  );
}

class SignUpDialog extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.handleSignUp = this.handleSignUp.bind(this);
    this.state = {login: ''};
  }

  render() {
    return (
      <Dialog title="Mars Keşif Programı"
              message="Size nasıl başvurmalıyız?">
        <input value={this.state.login}
               onChange={this.handleChange} />
        <button onClick={this.handleSignUp}>
          Kayıt Ol
        </button>
      </Dialog>
    );
  }

  handleChange(e) {
    this.setState({login: e.target.value});
  }

  handleSignUp() {
    alert(`Uçağa hoşgeldiniz, ${this.state.login}!`);
  }
}
```

<a href="https://codepen.io/gaearon/pen/gwZbYa?editors=0010">CodePen'de Deneyin</a>

<h2>Inheritance Hakkında</h2>

Facebook binlerce componentte React kullanıyor ve component hiyerarşileri oluştururken önerdiğimiz herhangi bir kullanım durumu bulamadık.

Props and compositionlar, componentin görünümünü ve davranışını açık ve güvenli bir şekilde özelleştirmeniz için gereken tüm esnekliği verir.

Componentler arasında UI olmayan işlevselliği yeniden kullanmak istiyorsanız ayrı bir JavaScript modülü içine ayıklamanızı öneririz.
Componentler içe aktarabilir ve bu fonksiyonu, nesneyi veya bir sınıfı uzatmadan kullanabilir.

<i>Konu anlatımları sonlanmıştır. Bu aşamadan sonra <b>Gelişmiş Kılavuzlar</b> konularına geçiş yapılacaktır.</i>

---

<h1>Derinlemesine JSX</h1>

Temel olarak, JSX sadece `React.createElement(component, props, ...children)` fonksiyonları için syntax sağlar.

JSX kodu:

```js
<MyButton color="blue" shadowSize={2}>
  Tıkla
</MyButton>
```

Yukarıdaki kodu, bu koda derler:

```js
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'Tıkla'
)
```

Hiçbir child yoksa etiketi direkt kapatarakta kullanabilirsiniz:

```js
<div className="sidebar" />
```

Yukarıdaki kodu, bu koda derler:

```js
React.createElement(
  'div',
  {className: 'sidebar'},
  null
)
```

JSX'in JavaScript'e nasıl dönüştürüldüğünü test etmek isterseniz, <a href="https://babeljs.io/repl/#?presets=react&code_lz=GYVwdgxgLglg9mABACwKYBt1wBQEpEDeAUIogE6pQhlIA8AJjAG4B8AEhlogO5xnr0AhLQD0jVgG4iAXyJA">online Babel derleyicisini</a> deneyebilirsiniz.

<h2>React'te Element Tipini Belirleme</h2>

Bir JSX etiketinin ilk harfi, React elementinin türünü belirler.

Büyük harfle başlayan bir JSX etiketi, bunun bir React componenti olduğunu belirtir. Bu etiketler, adlandırılmış değişkene doğrudan referans olarak derlenir; bu nedenle, JSX `<Foo />` ifadesini kullanırsanız, `Foo` scope (<i>kapsam</i>) dahilinde olmalıdır.

<h2>React Scope'ta Olmalı</h2>

JSX `React.createElement` çağrısına derlediğinden, `React` kitaplığı daima JSX kodunuzun scope'unda olmalıdır.

Örneğin, `React` ve `CustomButton` doğrudan JavaScript'te atıf yapılmamasına rağmen, bu kodda her iki importta gereklidir:

```js
import React from 'react';
import CustomButton from './CustomButton';

function WarningButton() {
  // return React.createElement(CustomButton, {color: 'red'}, null);
  return <CustomButton color="red" />;
}
```

Bir JavaScript paketleyicisi kullanmazsanız ve React'i  `<script>` etiketi ile yüklediyseniz, zaten `React` globali scopetadır.

<h2>Nokta Notasyonunu JSX Türü İçin Kullanma</h2>

JSX içinde nokta işareti kullanarak bir React componentine başvurabilirsiniz. Birçok React componenti ihraç eden bir modülünüz varsa bu uygundur. Örneğin, `MyComponents.DatePicker` bir component ise, bunu doğrudan JSX'den şu şekilde kullanabilirsiniz:

```js
import React from 'react';

const MyComponents = {
  DatePicker: function DatePicker(props) {  
    return <div>Buraya {props.color} geldiğini düşünün.</div>;
  }
}

function BlueDatePicker() {
  return <MyComponents.DatePicker color="blue" />;
}
```

<h2>Componentler Büyük Harf İle Başlamalıdır</h2>

Bir element türü küçük harfle başlarsa, `<div>` veya `<span>` gibi yerleşik bir componente atıfta bulunur ve `React.createElement` alanına aktarılan bir string `'div'` veya `'span'` ile sonuçlanır. `<Foo />` gibi büyük harfle başlayan türler `React.createElement(Foo)`'ya derlenir ve JavaScript dosyanızda tanımlanmış veya içe aktarılmış bir componente karşılık gelir.

Componentlerin ilk harfini büyük harfle isimlendirmenizi öneririz. Küçük harfle başlayan bir componente sahipseniz, JSX'de kullanmadan önce baş harfini büyük harfe dönüştürün.

Örneğin, bu kod beklendiği gibi çalışmaz:

```js
import React from 'react';

// Hata! Bu bir component ve baş harfi büyük yazılmış olmalıydı:
function hello(props) {
  // Doğru! Div, geçerli bir HTML etiketi olduğu için <div> kullanımının meşru olduğunu söyleyebiliriz.
  return <div>Merhaba {props.toWhat}</div>;
}

function HelloWorld() {
  // Yanlış! React <hello />'nun büyük harf kullanmadığından bunun bir HTML etiketi olduğunu düşünür.
  return <hello toWhat="World" />;
}
```

Bunu düzeltmek için, `hello` elementini `Hello` olarak yeniden adlandırıp, ona atıfta bulunmak için ise `<Hello />` kullanacağız:

```js
import React from 'react';

// Doğru! Bu bir component ve baş harfi büyük yazılmıştır:
function Hello(props) {
  // Doğru! Div, geçerli bir HTML etiketi olduğu için <div> kullanımının meşru olduğunu söyleyebiliriz.
  return <div>Merhaba {props.toWhat}</div>;
}

function HelloWorld() {
  // Doğru! React, <Hello />'nun component olduğunu bilir çünkü büyük harfle başlamıştır.
  return <Hello toWhat="World" />;
}
```

<h2>Runtime Olarak Tür Seçimi</h2>

React element türü olarak genel bir ifade kullanamazsınız. Elementin türünü belirtmek için genel bir ifade kullanmak istiyorsanız, önce önce baş harfi büyük bir değişkene atayın. Bu, genellikle bir pakete dayalı farklı bir component oluşturmak istediğinizde ortaya çıkar:

```js
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
  photo: PhotoStory,
  video: VideoStory
};

function Story(props) {
  // Yanlış! JSX türü bir obje olamaz.
  return <components[props.storyType] story={props.story} />;
}
```
Bunu düzeltmek için önce türü baş harfi büyük bir değişkene atayacağız:

```js
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
  photo: PhotoStory,
  video: VideoStory
};

function Story(props) {
  // Doğru! JSX türü baş harfi büyük yazılmış bir değişken olabilir.
  const SpecificStory = components[props.storyType];
  return <SpecificStory story={props.story} />;
}
```

<h2>JSX'te Propslar</h2>

Propsları JSX'de belirtmenin birkaç farklı yolu vardır.

<h3>JavaScript İfadeleri Olarak Props</h3>

Herhangi bir JavaScript ifadesini `{}` ile çevreleyerek yazabilirsiniz. Örneğin, bu JSX'de:

```js
<MyComponent foo={1 + 2 + 3 + 4} />
```

`MyComponent` için, `props.foo` değeri `1 + 2 + 3 + 4`  ifadesini hesaplar ve `10` olur.

`if` ifadelerini ve` for` döngülerini JSX'te doğrudan kullanamayız. Bunun yerine, bunları çevreleyen koda yerleştirebilirsiniz.

Örneğin:

```js
function NumberDescriber(props) {
  let description;
  if (props.number % 2 == 0) {
    description = <strong>even</strong>;
  } else {
    description = <i>odd</i>;
  }
  return <div>{props.number}, {description} sayıdır.</div>;
}
```

<a href="https://omergulcicek.github.io/react/sartli-render">Şartlı render</a> ve <a href="https://omergulcicek.github.io/react/listeler-ve-keyler">döngüler</a> hakkında ilgili bölümlerde daha fazla bilgi edinebilirsiniz.

<h3>String Literaller</h3>

Bir string ifadeyi props olarak geçirebilirsiniz. Bu iki JSX ifadesi aynıdır:

```js
<MyComponent message="Merhaba Dünya" />

<MyComponent message={'Merhaba Dünya'} />
```

Bir string gönderirken, değeri HTML-unescaped'dir. Dolayısıyla bu iki JSX ifadesi aynıdır:

```js
<MyComponent message="&lt;3" />

<MyComponent message={'<3'} />
```

<h3>Propslar Default Olarak True'dur</h3>

Değer girmezseniz, default (<i>varsayılan</i>) olarak propslar `true` olur. Bu iki JSX ifadesi aynıdır.

```js
<MyTextBox autocomplete />

<MyTextBox autocomplete={true} />
```

Genel olarak bunu kullanmanızı önermiyoruz çünkü `{foo: true}` yerine, `{foo: foo}` için kısa olan ES6 nesne kısayolu `{foo}` ile karıştırılabilir.

<h3>Spread Attributeler</h3>

Bir `props`unuz varsa ve bunu JSX'de geçirmek istiyorsanız, bütün props nesnesini geçmek için `...`yı spread bir operatör olarak kullanabilirsiniz. Bu iki component aynıdır:

```js
function App1() {
  return <Greeting firstName="Ömer" lastName="Gülçiçek" />;
}

function App2() {
  const props = {firstName: 'Ömer', lastName: 'Gülçiçek'};
  return <Greeting {...props} />;
}
```

Ayrıca, tüm propsları geçirirken componentinizin tüketeceği belirli propsu ayrı olarak seçebilirsiniz.

```js
const Button = props => {
  const { kind, ...other } = props;
  const className = kind === "primary" ? "PrimaryButton" : "SecondaryButton";
  return <button className={className} {...other} />;
};

const App = () => {
  return (
    <div>
      <Button kind="primary" onClick={() => console.log("Tıklandı!")}>
        Merhaba Dünya!
      </Button>
    </div>
  );
};
```

Yukarıdaki örnekte `kind` güvenli bir şekilde tüketilir ve DOM'da `<button>` elemanına geçirilmez.
Diğer tüm propslar, `...other` nesnesi aracılığıyla geçirilir ve bu component gerçekten esnek hale gelir. Bir `onClick` ve `children` propsundan geçtiğini görebilirsiniz.

Spread attributeleri kullanışlı olabilir, ancak gereksiz componentleri kendileri için önemsemeyen componentlere veya geçersiz HTML attributelerini DOM'a geçirmeyi kolaylaştırır. Bu syntaxı dikkatli kullanmanızı öneririz.

<h2>JSX'te Children</h2>

Hem bir açılış etiketi hem de bir kapanış etiketi içeren JSX ifadelerde, bu etiketler arasındaki içerik `props.children` olarak aktarılır. Childrenları geçmenin birkaç farklı yolu vardır:

<i>Bu konu ile ilgili olan <a href="https://omergulcicek.github.io/react/composition-ve-inheritance">composition ve inheritance</a> konusunuda okuyabilirsiniz.</i>

<h3>String Literaller</h3>

Açılış ve kapanış etiketleri arasına bir string koyabiliriz, bu string `props.children` olacaktır. Örneğin:

```js
<MyComponent>Merhaba Dünya!</MyComponent>
```

Bu geçerli JSX'dir ve `MyComponent`deki `props.children`, basitçe "Merhaba Dünya!" stringi olacaktır.

JSX bir satırın başında ve sonunda olan boşlukları kaldırır. Boş satırları da kaldırır. Etiketlerin yanındaki yeni satırlar kaldırılır; string değişkenlerinin ortasında oluşan yeni satırlar tek bir alana yoğuşturulur. Yani aşağıdaki örneklerin hepsi aynı şeyi yapar:

```js
<div>Merhaba Dünya/div>

<div>
  Merhaba Dünya
</div>

<div>
  Merhaba
  Dünya
</div>

<div>

  Merhaba Dünya
</div>
```

<h3>JSX'te Children</h3>

İstediğiniz kadar componenti children (<i>çocuk</i>) olarak kullanabilirsiniz, iç içe geçmiş componentleri görüntülemek için kullanışlıdır:

```js
<MyContainer>
  <MyFirstComponent />
  <MySecondComponent />
</MyContainer>
```

Bir React componenti dizi return edebilir:

```js
render() {
  // Liste öğelerini fazladan bir element ile sarmanıza gerek yok!
  return [
    // Keyleri unutmayın
    <li key="A">First item</li>,
    <li key="B">Second item</li>,
    <li key="C">Third item</li>,
  ];
}
```

<i>Keyler hakkında detaylı bilgi için <a href="https://omergulcicek.github.io/react/listeler-ve-keyler">listeler ve keyler</a> konusundan <b>keyler</b> başlığına bakabilirsiniz.</i>

<h3>Children JavaScript İfadeleri</h3>

JavaScript ifadesini childrena `{}`e koyarak geçirebilirsiniz. Örneğin, bu ifadeler aynıdır:

```js
<MyComponent>Örnek</MyComponent>

<MyComponent>{'Örnek'}</MyComponent>
```

Bu, keyfi uzunlukta JSX ifadelerinin bir listesini oluşturmak için genellikle yararlıdır. Örneğin, bu bir HTML listesi oluşturur:

```js
function Item(props) {
  return <li>{props.message}</li>;
}

function TodoList() {
  const todos = ['Ömer', 'Burak', 'Muhammed'];
  return (
    <ul>
      {todos.map((message) => <Item key={message} message={message} />)}
    </ul>
  );
}
```

JavaScript ifadeleri diğer children türleri ile birlikte kullanılabilir. Bu genellikle string şablonlarının yerine yararlıdır:

```js
function Hello(props) {
  return <div>Merhaba {props.addressee}!</div>;
}
```

<h3>Children Türünden Functions </h3>

Normalde, JSX'e eklenen JavaScript ifadeleri bir stringe, bir React elementi veya bu şeylerin bir listesine göre değerlendirilir. Bununla birlikte, `props.children`, yalnızca React'in nasıl yapılacağını bildiği türden değil, herhangi bir veri türünden geçebileceği için diğer herhangi bir `props` gibi çalışır. Örneğin, özel bir componente sahipseniz, bir callback'i `props.children` olarak almasını sağlayabilirsiniz:

```js
// Tekrarlanan bir component üretmek için childrenların callback'leri çağırır
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
    items.push(props.children(i));
  }
  return <div>{items}</div>;
}

function ListOfTenThings() {
  return (
    <Repeat numTimes={10}>
      {(index) => <div key={index}>Bu listede {index} olan öğedir.</div>}
    </Repeat>
  );
}
```

<h3>Booleans, Null ve Undefined Yok Sayılır</h3>

`false`, `null`, `undefined` ve `true` geçerli childrenlardır. Onlar sadece render yapılmazlar. Bu JSX ifadeleri hep aynı şeyi yapacak:

```js
<div />

<div></div>

<div>{false}</div>

<div>{null}</div>

<div>{undefined}</div>

<div>{true}</div>
```

Bu, koşullu olarak React elementlerini oluşturmak için yararlı olabilir. JSX yalnızca `showHeader` true ise `<Header />` componentini görür, false ise görmez:

```js
<div>
  {showHeader && <Header />}
  <Content />
</div>
```

Bir uyarı, '0' sayısı gibi bazı <b>falsy</b> değerleri React tarafından render edilir. Örneğin, bu kod, `props.messages` boş bir dizi olduğunda '0' yazdırılacağı için beklediğiniz gibi davranmayacaktır:

```js
<div>
  {props.messages.length &&
    <MessageList messages={props.messages} />
  }
</div>
```

<i>Falsy değeri, boolean bağlamında değerlendirildiğinde false değerine çeviren bir değerdir. JavaScript, if-else ve döngüler gibi herhangi bir değeri bir boolena gerektiren bağlamlarda zorlamak için tür tipi dönüştürme özelliğini kullanır.</i>

<i>JavaScript'teki false değerlerin örnekleri (false'a çevrilir ve böylece if bloğunu atlar):</i>

```js
if (false)
if (null)
if (undefined)
if (0)
if (NaN)
if ('')
if ("")
if (document.all) [1]
```

<i>Normalde `true && kod` olduğunda ilk ifade true olduğu için sağ kısımdaki kod çalışacaktır. `false && kod` olduğunda ise kod hiçbir çıktı vermeyecektir. JavaScript'te `1 && kod` olduğunda 1'i true olarak değerlendirip kodu çalıştırır fakat `0 && kod` olduğunda 0'ı false olarak değerlendirmez ve ekrana `0` yazar.</i>

Bunu düzeltmek için, `&&` önündeki ifadenin her zaman boolean olduğundan emin olun:

```js
<div>
  {props.messages.length > 0 &&
    <MessageList messages={props.messages} />
  }
</div>
```

Aksine, çıktıda `false`,` true`, `null` veya` undefined` gibi bir değerleri görmek istiyorsanız, önce bir string haline getirmeniz gerekir:

```js
<div>
  JavaScript değişkenim {String(myVariable)}.
</div>
```

---

<h1>ES6 Olmadan React</h1>

Normalde bir React componentini düz bir JavaScript sınıfı olarak tanımlarsınız:

```javascript
class Greeting extends React.Component {
  render() {
    return <h1>Merhaba, {this.props.name}</h1>;
  }
}
```

ES6'yı kullanmıyorsanız, yerine `create-react-class` modülünü kullanabilirsiniz:

```javascript
var createReactClass = require('create-react-class');
var Greeting = createReactClass({
  render: function() {
    return <h1>Merhaba, {this.props.name}</h1>;
  }
});
```

ES6 sınıflarının API'leri birkaç istisna dışında `createReactClass()`a benzemektedir.

<h2>Varsayılan Propsları Bildirmek</h2>

Fonksiyonlar ve ES6 sınıflarıyla `defaultProps`, componentin kendisinde bir özellik olarak tanımlanır:

```js
class Greeting extends React.Component {
  // ...
}

Greeting.defaultProps = {
  name: 'Ömer'
};
```

`CreateReactClass()` ile iletilen obje üzerinde bir fonksiyon olarak `getDefaultProps()` tanımlamanız gerekir:

```javascript
var Greeting = createReactClass({
  getDefaultProps: function() {
    return {
      name: 'Ömer'
    };
  },

  // ...

});
```

<h2>Başlangıç State'ini Ayarlama</h2>

ES6 sınıflarında, başlangıç state'ini constructor içerisinde `this.state` ile tanımlayabilirsiniz.

```javascript
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: props.initialCount};
  }
  // ...
}
```

`CreateReactClass()` ile başlangıç state'ini return eden ayrı bir `getInitialState` yöntemi sağlamanız gerekir:

```javascript
var Counter = createReactClass({
  getInitialState: function() {
    return {count: this.props.initialCount};
  },
  // ...
});
```

<h2>Autobinding</h2>

ES6 sınıfları ile oluşturulan componentlerde, metodlar normal ES6 sınıflarıyla aynı semantiği uygularlar. Bu, otomatik olarak `this`i buton clickine bağlamadıkları anlamına gelir. Constructor içerisinde `.bind(this)`i kullanmanız gerekir:

```javascript
class SayHello extends React.Component {
  constructor(props) {
    super(props);
    this.state = {message: 'Merhaba!'};
    // Bu satır önemli!
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    alert(this.state.message);
  }

  render() {
    // `this.handleClick` bağlı olduğundan bunu bir event işleyicisi olarak kullanabilirsiniz.
    return (
      <button onClick={this.handleClick}>
          Selam ver
      </button>
    );
  }
}
```

`CreateReactClass()` ile tüm metodlar bağlandığı için buna gerek yoktur:

```javascript
var SayHello = createReactClass({
  getInitialState: function() {
    return {message: 'Merhaba!'};
  },

  handleClick: function() {
    alert(this.state.message);
  },

  render: function() {
    return (
      <button onClick={this.handleClick}>
        Selam ver
      </button>
    );
  }
});
```

<i>Bind etmek ile ilgili detaylı bilgi için kendi yazdığım Türkçe makaleden yararlanabilirsiniz. Bknz: <a href="https://omergulcicek.com/blog/bind-fonksiyonu">Bind() Fonksiyonu</a></i>

ES6 sınıflarının yazılması, event işleyicileri için biraz daha fazla kalıp kod ile gelir ancak tersi büyük uygulamalarda biraz daha iyi bir performans sunar.

```js
class SayHello extends React.Component {
  constructor(props) {
    super(props);
    this.state = {message: 'Merhaba!'};
  }
  // UYARI: Bu syntax deneyseldir!
  // Burada ok fonksiyonu kullanarak yöntem bağlanır:
  handleClick = () => {
    alert(this.state.message);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Selam ver
      </button>
    );
  }
}
```

Lütfen yukarıdaki syntaxın deneysel olduğunu ve syntaxının değişebileceğini veya önerinin dilin içine girmediğini unutmayın.

Güvenli bir şekilde yazmayı tercih ederseniz birkaç seçeneğiniz vardır:

* Constructor içinde bind methodu kullanmak
* Ok fonksiyonlarını kullanmak, örneğin `onClick={(e) => this.handleClick(e)}`
* `createReactClass` kullanmaya devam etmek

<h2>Mixinler</h2>

>**Not:**
>
>ES6 hiçbir mixin desteği olmadan başlatıldı. Bu nedenle, ES6 sınıfları ile React kullandığınızda mixin desteği olmayacaktır.
>
>**Ayrıca, mixin kullanan kodlarda çok sayıda sorun bulduk ve bunları yeni projelerinizde kullanmanızı önermiyoruz**
>
>Bu bölüm yalnızca referans içindir.

Bazen çok farklı componentler bazı ortak fonksiyonları paylaşabilir. Bunlara bazen kesişen konular da denir. `createReactClass`, bunun için eski bir `mixins` sistemi kullanmanızı sağlar.

Bir zaman aralığında kendisini güncellemek isteyen bir component, çok sık karşılaşılan bir kullanım durumudur. `SetInterval()` kullanmak kolaydır; ancak, `setInterval()` ile işiniz bittiğinde bunu iptal etmek önemlidir. React, bir component oluşturulmaya başlandığında veya yok edildiğinde sizi bilgilendiren lifecycle fonksiyonlarını kullanmanızı sağlar. Componenti yok edildiğinde otomatik olarak temizlenecek kolay bir `setInterval()` methodu sağlamak için bu yöntemleri kullanan basit bir mixin oluşturalım.

<i>Lifecycle fonksiyonları ile ilgili detaylı bilgi için <a href="https://omergulcicek.github.io/react/state-ve-lifecycle">State ve lifecycle</a> konusunda <b>"Bir Classa Lifecycle Fonksiyonları Ekleme"</b> başlığını inceleyebilirsiniz.</i>

```js
var SetIntervalMixin = {
  componentWillMount: function() {
    this.intervals = [];
  },
  setInterval: function() {
    this.intervals.push(setInterval.apply(null, arguments));
  },
  componentWillUnmount: function() {
    this.intervals.forEach(clearInterval);
  }
};

var createReactClass = require('create-react-class');

var TickTock = createReactClass({
  mixins: [SetIntervalMixin], // Mixini kullan
  getInitialState: function() {
    return {seconds: 0};
  },
  componentDidMount: function() {
    this.setInterval(this.tick, 1000); // Mixin üzerinde bir metod çağır
  },
  tick: function() {
    this.setState({seconds: this.state.seconds + 1});
  },
  render: function() {
    return (
      <p>
        Sayfa {this.state.seconds} saniyedir çalışıyor.
      </p>
    );
  }
});

ReactDOM.render(
  <TickTock />,
  document.getElementById('example')
);
```

Bir component çoklu mixin kullanıyorsa ve birkaç mixin aynı lifecycle fonksiyonu tanımlarsa (diğer bir deyişle, birkaç mixin, component yok edildiğinde bazı temizlemeler yapmak isterse), tüm lifecycle fonksiyonunun çağrılmasının garanti altına alınması sağlanır.

---

<h1>JSX Olmadan React</h1>

JSX, React'ı kullanmak için şart değildir.

JSX bizlere sadece yazım kolaylıkları sağlar. JSX ile yapabileceğiniz herhangi bir şeyi düz JavaScript ile yapılabiliriz.

Örneğin, bu kod JSX ile yazılmıştır:

```js
class Hello extends React.Component {
  render() {
    return <div>Merhaba {this.props.toWhat}</div>;
  }
}

ReactDOM.render(
  <Hello toWhat="Dünya" />,
  document.getElementById('root')
);
```

Yukarıdaki kod, JSX kullanmayan bu koda derlenebilir:

```js
class Hello extends React.Component {
  render() {
    return React.createElement('div', null, `Merhaba ${this.props.toWhat}`);
  }
}

ReactDOM.render(
  React.createElement(Hello, {toWhat: 'Dünya'}, null),
  document.getElementById('root')
);
```

JSX'in JavaScript'e dönüştürülmesiyle ilgili daha fazla örnek görmek istiyorsanız, <a href="https://babeljs.io/repl/#?presets=react&code_lz=GYVwdgxgLglg9mABACwKYBt1wBQEpEDeAUIogE6pQhlIA8AJjAG4B8AEhlogO5xnr0AhLQD0jVgG4iAXyJA">online Babel derleyicisi</a>ni deneyebilirsiniz.

Sürekli `React.createElement` yazmaktan sıkıldıysak, bir kısaltma kullanmak mantıklı olacaktır:

```js
const e = React.createElement;

ReactDOM.render(
  e('div', null, 'Merhaba Dünya'),
  document.getElementById('root')
);
```

Bu kısa formu `React.createElement` için kullanırsanız, JSX olmadan React'i kullanmak elverişli olabilir.

Alternatif olarak, daha kısa bir syntax sunan <a href="https://github.com/mlmorg/react-hyperscript">react-hyperscript</a> ve <a href="https://github.com/ohanhi/hyperscript-helpers">hyperscript-helpers</a> gibi projelere başvurabilirsiniz.

---

<h1>Fragmentler</h1>

Bir componentin birden çok element return etmesi React'te yaygın olarak kullanılır. Fragmentler, DOM'a fazladan etiket eklemeden childları gruplanmasına izin verir.

<i>Normalde React'te bir componentin içeriği kapsayıcı bir element ile return edilirdi. Kapsayıcı element olmazsa hata veriyordu. Buda fazladan `<div>` tagı oluşturulmasına sebep oluyordu. Fakat `React v16.2.0` ile artık hayali bir kapsayıcı olan `Fragment`i oluşturabiliyoruz. Bu fragmentler çıktıyı kapsadığı için içerik return edilebilecek fakat çıktıda görünmeyeceklerdir. Böylece fazladan div oluşumu önlenmiş olacaktır.</i>

<i>Aşağıdaki içeriği React componentinde return etmek istediğimizi düşünelim.</i>

```html
Biraz yazı
<h2>Başlık</h2>
Daha fazla yazı
<h2>Diğer başlık</h2>
Daha fazla yazı
```

React versiyon 16.2.0'dan önce bunu gerçekleştirmenin tek yolu, childları `div`, `span` gibi bir tag ile aşağıdaki gibi sarmalamaktır:

```js
render() {
  return (
    // Fazladan bir div :(
    <div>
      Biraz yazı
      <h2>Başlık</h2>
      Daha fazla yazı
      <h2>Diğer başlık</h2>
      Daha fazla yazı
    </div>
  );
}
```

<h2>Kullanımı</h2>

<i>return edilecek değerleri `<React.Fragment>` componenti içerisine yerleştirmeniz yeterli.</i>

```jsx
class Columns extends React.Component {
  render() {
    return (
      <React.Fragment>
        <td>Merhaba</td>
        <td>Dünya</td>
      </React.Fragment>
    );
  }
}
```

<i>`React.Fragment` yerine sadece `Fragment` ile kapsamak isterseniz aşağıdaki gibi bir yol izleyebilirsiniz.</i>

```js
const Fragment = React.Fragment;

<Fragment>
  <ChildA />
  <ChildB />
  <ChildC />
</Fragment>

// Her ikiside aynı şeydir
<React.Fragment>
  <ChildA />
  <ChildB />
  <ChildC />
</React.Fragment>
```

<h3>Kısa Syntax</h3>

Fragmentler için yeni bir kısa syntaxta var ancak henüz tüm popüler toollar (<i>araçlar</i>) tarafından desteklenmemektedir.

```jsx
class Columns extends React.Component {
  render() {
    return (
      <>
        <td>Merhaba</td>
        <td>Dünya</td>
      </>
    );
  }
}
```

 `<></>` kullanabilirsiniz fakat keys ya da attribute kullanımını desteklemez (<i>Sadece kapsayıcı olarak kullanılır</i>).

Birçok toolsun henüz kısa syntax kullanımını desteklemediğini unutmayın, bu nedenle destek gelene kadar açıkça `<React.Fragment>` yazın.

<h3>Keyli Fragmentler</h3>

`<React.Fragment>` syntaxı ile bildirilen parçaların keyleri olabilir. Örneğin bir açıklama listesi oluşturmak için:

```jsx
function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        // `key` olmazsa, React bir key uyarısı verecektir
        <React.Fragment key={item.id}>
          <dt>{item.term}</dt>
          <dd>{item.description}</dd>
        </React.Fragment>
      ))}
    </dl>
  );
}
```

`Fragment`e aktarılabilen tek attribute `key`dir. Gelecekte, click-change olayları gibi ek attributeler için destek ekleyebiliriz.

<a href="https://codepen.io/reactjs/pen/VrEbjE?editors=1000">CodePen'de Deneyin</a>

---

<h1>Lifecycle Fonksiyonları</h1>

`React.Component` soyut temel bir sınıftır, bu nedenle doğrudan React.Componente başvurmak mantıklı değildir. Bunun yerine, genellikle classın alt classını tanımlayıp, bir `render()` metodu tanımlarsınız.

Normalde bir React componentini düz bir JavaScript sınıfı olarak tanımlarsınız:

```js
class Greeting extends React.Component {
  render() {
    return <h1>Merhaba, {this.props.name}</h1>;
  }
}
```

ES6'yı henüz kullanmıyorsanız, bunun yerine `create-react-class` modülünü kullanabilirsiniz. Daha fazla bilgi edinmek için <a href="https://omergulcicek.github.io/react/es6-olmadan-react">ES6 olmadan React</a> konusuna bakın.

Unutmayın, kendi temel component classlarınızı oluşturmanızı önermiyoruz. Kodun tekrar kullanımı React'te inheritancetan ziyade composition yoluyla elde edilir. Composition kullanma konusunda bir fikir edinmek için <a href="https://omergulcicek.github.io/react/composition-ve-inheritance">composition ve inheritance</a> sayfasını inceleyin.

Her componentin, lifecycle  fonksiyonları vardır. İçerisinde `will` geçen fonksiyonlar component oluşturulmasından hemen önce çağrılırken, içerisinde `did` geçen fonksiyonlar component kaldırıldıktan sonra çağrılır.

<i>Şimdi tüm fonksiyonları bölümlendirip, ardından her birini açıklayacağız. Başlıklara çeviri yapılmamıştır, altlarına Türkçesi eklenmiştir.</i>

<h4>Mounting</h4>

<i>Oluşturmak</i>

Bu fonksiyonlar, bir component örneği oluşturulurken ve DOM'a eklendiğinde çağrılır:

- `constructor()`
- `componentWillMount()`
- `render()`
- `componentDidMount()`

<h4>Updating</h4>

<i>Güncellemek</i>

Bir güncelleme, props ya da state değişikliklerinden kaynaklanabilir. Bu fonksiyonlar, bir componentin güncellenmesiyle çağrılır.

- `componentWillReceiveProps()`
- `shouldComponentUpdate()`
- `componentWillUpdate()`
- `render()`
- `componentDidUpdate()`

<h4>Unmounting</h4>

<i>Kaldırmak</i>

Bu fonksiyon, bir component DOM'dan kaldırıldığında çağrılır:

- `componentWillUnmount()`

<h4>Error Handling</h4>

<i>Hata işleme</i>

Bu fonksiyon, render sırasında lifecycle fonksiyonlarında veya herhangi bir alt componentin constructoründe bir hata olduğunda çağrılır.

- `componentDidCatch()`

<h3>Diğer API'ler</h3>

Her component aşağıdaki API'leride içerisinde barındırır:

- `setState()`
- `forceUpdate()`

<h3>Class Property</h3>

- `defaultProps`

* * *

<h3>render()</h3>

```js
render()
```
 `render()` fonksiyounu zorunludur.

Çağrıldığında, `this.props` ve `this.state`i incelemeli ve aşağıdaki türlerden birine return etmelidir:

- <b>React Elementleri</b>. Genellikle JSX aracılığıyla oluşturulur. Bir element, yerel bir DOM componenti (`<div />`) veya kullanıcı tanımlı bir component (`<MyComponent />`) olabilir.
- <b>String ve sayı</b>. Bunlar DOM'da metin düğümleri olarak render edilir.
- <b>Portaller</b>. `ReactDOM.createPortal` ile oluşturuldu. <i><a href="https://reactjs.org/docs/portals.html">Detaylı bilgi</a></i>
- <b>null</b>. Hiçbir şey yapmaz.
- <b>Boolean</b>. Hiçbir şey yapmaz. (Çoğunlukla `test`in boolean olduğu durumda `return test && <Child />` desenini desteklemek için vardır.)

`null` ya da `false` return ederkem, `ReactDOM.findDOMNode(this)` `null` return eder.

`render()` fonksiyonu, componentin state'ini değiştirmez, çağrıldığında her seferinde aynı sonucu return eder. Tarayıcıyla etkileşime girmeniz gerekiyorsa, bunun yerine ` componentDidMount()` ya da diğer lifecycle fonksiyonları ile çalışmalarınızı gerçekleştirin.

> Not
>
> `shouldComponentUpdate()` fonksiyonu `false` return ederse `render()` çağrılmayacaktır.

* * *

<h3>constructor()</h3>

```js
constructor(props)
```

Bir React componentinin constructorü, oluşturulmadan önce çağrılır. Bir `React.Component` alt sınıfı için constructorü uygularken, herhangi bir koddan önce `super(props)`u çağırmalısınız. Aksi takdirde, `this.props` constructorde hatalara neden olur.

Constructore herhangi bir abonelik sunmaktan kaçının. Bunun yerine, `componentDidMount()` kullanın.

Constructor, state'i başlatmak için doğru yerdir. Bunu yapmak için sadece bir nesneyi `this.state`e atayın; Constructor'den `setState()` fonksiyonunu çağırmaya çalışmayın. Constructor ayrıca, click-change olaylarını bind etmek için sıklıkla kullanılır.

<i>Bind fonksiyonu hakkında detaylı bilgiye kendi yazmış olduğum <a href="https://omergulcicek.com/blog/bind-fonksiyonu">Bind() fonksiyonu</a> adlı makaleden erişebilirsiniz.</i>

State, click-change olaylarını kullanmayacaksanız, React componenti için bir constructor oluşturmak zorunda değilsiniz.

* * *

<h3>componentWillMount()</h3>

```js
componentWillMount()
```

`componentWillMount()`, component oluşturulmadan hemen önce çağrılır, dolayısıyla bu yöntemde eş zamanlı olarak `setState()` başlamayacaktır. Genellikle, bunun yerine `constructor()`ü kullanmanızı öneririz.

* * *

<h3>componentDidMount()</h3>

```js
componentDidMount()
```

`componentDidMount()`, bir component render edildikten hemen sonra çağrılır. Uzak bir uç noktadan veri yüklemeniz gerekiyorsa, bu ağ isteğini başlatmak için iyi bir yerdir.

Bu fonksiyon, herhangi bir abonelik ayarlamak için iyi bir yerdir. Bunu yaparsanız, `componentWillUnmount ()` da aboneliğinizi iptal etmeyi unutmayın.

Bu yöntemde `setState()` çağrısı ek bir render işlemine neden olur, ancak tarayıcı ekranını güncellemeden önce gerçekleşir. `render()` fonksiyonunun bu durumda iki kez çağrılmasına rağmen kullanıcının ara state'i göremez. Bu kalıp sıklıkla performans sorunlarına neden olduğundan dikkatli kullanın.

* * *

<h3>componentWillReceiveProps()</h3>

```js
componentWillReceiveProps(nextProps)
```

`componentWillReceiveProps()`, bir component yeni bir props almaya başlamadan önce çağrılır. Props değişikliklerine tepki olarak state güncellemeniz gerekiyorsa (örneğin sıfırlamak için), `this.props` ve `nextProps` metodlarını karşılaştırabilir ve bu metoddaki `this.setState()` fonksiyonunu kullanarak state geçişleri gerçekleştirebilirsiniz.

React, propsta değişiklik yapılmamış olsa bile bu metodu çağırabilir, bu nedenle yalnızca değişiklikleri ele almak istiyorsanız geçerli ve sonraki değerleri karşılaştırdığınızdan emin olun.

React, mounting sırasında `componentWillReceiveProps()` fonksiyonunu ilk props grubu ile çağırmaz. Componentlerin propslarının bazıları güncellenmişse bu fonksiyonu çağırır. `this.setState()` fonksiyonunu çağrılması genellikle `componentWillReceiveProps()` fonksiyonunu tetiklemez.

* * *

<h3>shouldComponentUpdate()</h3>

```js
shouldComponentUpdate(nextProps, nextState)
```

Bir componentin çıktısı, state veya propstaki güncel değişiklikten etkilenmezse React'e bildirmek için `shouldComponentUpdate()` kullanın. Varsayılan davranış, her state değişiminde tekrar render edilmesidir ve çoğu durumda varsayılan davranışı kullanmalısınız.

`shouldComponentUpdate()` yeni props veya state alındığında render edilmeden önce çağrılır. Varsayılan değer `true`dur. Bu fonksiyon, componentin ilk render edilişinde veya `forceUpdate()` kullanıldığında çağrılmaz.

`false` değerininin return edilmesi, state değiştiğinde child componentlerin yeniden render edilmesini engellemez.

`shouldComponentUpdate()` fonksiyonu `false` return ederse `componentWillUpdate()`, `render()` ve `componentDidUpdate()` çağrılmayacaktır. React'in gelecekte `shouldComponentUpdate()`i sıkı bir yönerge yerine bir ipucu olarak ele alabileceğini ve `false` değerini return etmenin componentin yeniden render edilmesine neden olabileceğini unutmayın.

Belirli bir componentin görüntülenmesinden sonra yavaş olduğunu belirlerseniz, `shouldComponentUpdate()` fonksiyonunu sığ bir props ve state karşılaştırması ile uygulayan `React.PureComponent`ten devralmak için değiştirebilirsiniz. Elle yazmak istediğinizden eminseniz, `this.props` ile` nextProps` ve `this.state` ile `nextState`i karşılaştırabilir ve `false` return ederek React güncellemesini geçebilirsiniz.

`ShouldComponentUpdate()`te eşitlik kontrolleri yapmanızı veya `JSON.stringify()` fonksiyonunu kullanmanızı önermiyoruz. Çok verimsizdir ve performansa zarar verir.

* * *

<h3>componentWillUpdate()</h3>

```js
componentWillUpdate(nextProps, nextState)
```

`componentWillUpdate()` yeni props veya state alındığında render edilmeden hemen önce çağrılır. Bunu, güncelleme gerçekleşmeden önce hazırlık yapmak için bir fırsat olarak kullanın. Bu fonksiyon ilk render için çağrılmaz.

Burada `this.setState()` fonksiyonunu çağıramayacağınızı unutmayın; `componentWillUpdate()` return etmeden önce bir React componentinin güncellemesini tetikleyecek başka bir şey yapmanız (örn. bir Redux eylemi göndermeniz) gerekir.

Props değişikliklerine tepki olarak state'i güncellemek istiyorsanız, bunun yerine `componentWillReceiveProps()` kullanın.

> Not
>
> `shouldComponentUpdate()` false return ederse, `componentWillUpdate()` çağrılmayacaktır.

* * *

<h3>componentDidUpdate()</h3>

```js
componentDidUpdate(prevProps, prevState)
```

`componentDidUpdate()`, güncelleme gerçekleştikten hemen sonra çağrılır. Bu fonksiyon ilk render için çağrılmaz.

Bunu, component güncellendiğinde DOM üzerinde çalışmak için kullanın. Bu ayrıca, mevcut yeri önceki yerlerle kıyasladığınız sürece network istekleri yapmak için iyi bir yerdir (örneğin props değişmediğinde bir network isteği gerekmeyebilir).

> Not
>
> `shouldComponentUpdate()` false return ederse, `componentDidUpdate()` çağrılmayacaktır.

* * *

<h3>componentWillUnmount()</h3>

```js
componentWillUnmount()
```

`componentWillUnmount()`, bir component unmounted ve destroyed edilmeden hemen önce çağrılır. Bu fonksiyonda, zamanlayıcıları geçersiz kılma, network isteklerini iptal etme veya `componentDidMount()` fonksiyonunda oluşturulan abonelikleri temizleme gibi gerekli temizliği yapın.

* * *

<h3>componentDidCatch()</h3>

```js
componentDidCatch(error, info)
```

Hata sınırları, alt component ağacının herhangi bir yerindeki JavaScript hatalarını yakalayan, bu hataları log'a yazan ve çöktüğü compoennt ağacı yerine bir yedek UI görüntüleyen React componentleridir. Hata sınırları, render, lifecycle fonksiyonlar ve altındaki ağacın constructorlerinde hataları yakalar.

Beklenmedik istisnalardan kurtarmak için yalnızca hata sınırlarını kullanın; onları kontrol akışı için kullanmaya çalışmayın.

Daha fazla ayrıntı için React 16'daki <a href="https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html">Error Handling</a> bölümüne bakın.

> Not
>
> Hata sınırları yalnızca alt componentlerin içindeki hataları yakalar . Bir hata sınırı kendi içinde bir hata yakalayamaz.

* * *

<h3>setState()</h3>

```js
setState(updater[, callback])
```

`setState()`, component state'indeki değişiklikleri ekler ve bu componentin çocuklarının güncellenen state ile yeniden render edilmesini gerektiğini React'e bildirir. Bu, kullanıcı arabirimini güncellemek için kullandığınız birincil yöntemdir.

Componenti güncellemek için hemen bir komut yerine `setState()` fonksiyonunu çağırın. Daha iyi bir performans için React onu geciktirebilir ve sonra birkaç componenti tek seferde güncelleştirebilir.

`setState()` her zaman componenti hemen güncellemez. Güncelleme işini daha sonraya bırakıp toplu olarak yapabilir. Bu, `setState()` fonksiyonunu potansiyel bir tuzağa düşürdükten sonra `this.state` dosyasını okumayı kolaylaştırır. Bunun yerine, `componentDidUpdate` veya `setState(updater, callback)` kullanın; ikisi de güncelleme uygulandıktan sonra tetiklenecektir. State'i bir önceki state'e göre ayarlamanız gerekiyorsa, aşağıdaki `updater` argümanını okuyun.

```js
(prevState, props) => stateChange
```

`prevState`, önceki state'e yapılan atıftır. Doğrudan değişime uğratılmamalıdır. Bunun yerine, değişiklikler `prevState` ve `props` parametrelerine dayanan yeni bir nesne oluşturarak temsil edilmelidir. Örneğin, stateteki bir değeri `props.step` ile artırmak istediğimizi varsayalım:

```js
this.setState((prevState, props) => {
  return {counter: prevState.counter + props.step};
});
```

Güncelleyici fonksiyonu tarafından alınan hem `prevState` hem de `props`un güncel olması garanti edilir. Güncelleyicinin çıktısı derhal `prevState` ile birleştirilir.

`SetState()` fonksiyonunun ikinci parametresi, `setState` tamamlandıktan ve component yeniden render edildikten sonra yürütecek isteğe bağlı bir callback fonksiyonudur. Genellikle bunun yerine bu mantık için `componentDidUpdate()` kullanmanızı öneririz.

İsteğe bağlı olarak, bir objeyi bir fonksiyon yerine `setState()`in ilk argümanı olarak geçirebilirsiniz:

```js
setState(stateChange[, callback])
```

Bu, yeni bir state'e, örneğin bir alışveriş sepeti öğe miktarını ayarlamak için `stateChange` öğesinin sığ bir birleştirme gerçekleştirir:

```js
this.setState({quantity: 2})
```

Bu `setState()` şekli aynı zamanda eşzamansızdır ve aynı döngüde birlikte kullanılabilir. Örneğin, aynı döngüde bir maddenin miktarını birden çok kez artırmayı denerseniz, eşdeğerlik şu şekilde sonuçlanacaktır:

```js
Object.assign(
  previousState,
  {quantity: state.quantity + 1},
  {quantity: state.quantity + 1},
  ...
)
```

Sonraki çağrılar aynı döngüdeki önceki çağrıların değerlerini geçersiz kılacak, bu nedenle miktar yalnızca bir kez artırılacaktır. Bir sonraki state önceki state'e bağlıysa, bunun yerine updater işlev formunu kullanmanızı öneririz:

```js
this.setState((prevState) => {
  return {quantity: prevState.quantity + 1};
});
```
Detaylı bilgi için <a href="https://omergulcicek.github.io/react/state-ve-lifecycle">state ve lifecycle</a> sayfasını inceleyenilirsiniz.

* * *

<h3>forceUpdate()</h3>

```js
component.forceUpdate(callback)
```

Varsayılan olarak, componentinde state ya da props değiştiği zaman, component yeniden render edilir. `render()` fonksiyonu diğer bazı verilere bağlı ise, `forceUpdate()` fonksiyonunu çağırarak componentin yeniden oluşturulması gerektiğini React'e bildirebilirsiniz.

`forceUpdate()` çağrısı, `shouldComponentUpdate()` atlanarak componentte `render()` çağırılmasına neden olur. Bu, her bir çocuğun `shouldComponentUpdate()` fonksiyonu da dahil olmak üzere, alt componentlerin  lifecycle fonksiyonlarını tetikleyecektir.

`forceUpdate()` fonksiyonunun tüm kullanımlarından kaçınmaya çalışmalısınız ve sadece `render()`da `this.props` ve `this.state`ten okuma yapmalısınız.


* * *

<h2>Class Property</h2>

<h3>defaultProps</h3>

`defaultProps`, class için varsayılan props koymak için component clasının kendisinde bir özellik olarak tanımlanabilir. Bu, tanımlanmamış props için kullanılır, ancak boş props için kullanılamaz. Örneğin:

```js
class CustomButton extends React.Component {
  // ...
}

CustomButton.defaultProps = {
  color: 'blue'
};
```

`props.color` parametre olarak gönderilmezse, varsayılan olarak `blue` değerini alır:

```js
  render() {
    return <CustomButton />; // props.color, blue olacaktır
  }
```

`props.color` null tanımlanırsa, null olacaktır:

```js
  render() {
    return <CustomButton color={null} /> ; // props.color, null olacaktır
  }
```

---

<h2>Single Page Application</h2>

Single page application yani kısa adıyla SPA, tek HTML sayfası yükleyen bir uygulamadır ve uygulamanın çalışması için gerekli tüm dosyaları (JavaScript, CSS vb) içerir. Sayfa veya sonraki sayfalarla olan herhangi bir etkileşim için servera gidip gelmesi gerektirmez; bu da sayfanın yeniden yüklenmediği anlamına gelir.

Reactte SPA oluşturabilmenize rağmen, bu bir zorunluluk değildir. React, hali hazırda çalışan bir sitenin küçük bölümlerini geliştirmek için de kullanılabilir. React'te yazılmış kod, diğer diller ile de kullanılabilir. Facebook'un sitesi buna en iyi örnektir.

<h2>ES6, ES2015, ES2016</h2>

Bu kısaltmalar, JavaScript dilinin bir uygulaması olan ECMAScript standartlarının en yeni sürümlerine karşılık gelir. ES6 sürümü (ES2015 olarak da bilinir), ok fonksiyonları, classlar, şablon değişmezleri, `let` ve `const` ifadeleri gibi önceki sürümlere pek çok ekleme içerir.

<h2>Compiler</h2>

Bir JavaScript derleyicisi, güncel sürümlerde yazılmış (<i>örneğin ES6</i>) kodunu alır, tarayıcıların anlayacağı syntaxa dönüştürür. Bunun için React ile en sık kullanılan derleyici <a href="https://babeljs.io/">Babel</a>dir.

<h2>Bundler</h2>

Bundlerlar (<i>paketleyiciler</i>), JavaScript ve CSS kodunu ayrı modüller (çoğunlukla yüzlerce tanesi) olarak yazarlar ve tarayıcılar için daha iyi optimize edilmiş birkaç dosyaya birleştirirler. React uygulamalarında yaygın olarak kullanılan bazı paketleyiciler arasında <a href="https://webpack.js.org/">Webpack</a> ve <a href="http://browserify.org/">Browserify</a> bulunur.

<h2>Package Manager</h2>

Package manager (<i>Paket yöneticileri</i>), projenizdeki bağımlılıkları yönetmenize izin veren araçlardır. <a href="https://www.npmjs.com/">npm</a> ve <a href="http://yarnpkg.com/">yarn</a>, React uygulamalarda yaygın olarak kullanılan iki paket yöneticisidir. Her ikisi de aynı npm paketi kayıt defteri için istemcilerdir.

## CDN

CDN, Content Delivery Network (<i>İçerik Dağıtım Ağı</i>) kısaltmasıdır. CDN'ler, tüm dünyadaki bir sunucudan önbelleklenmiş statik içeriği sağlar.

## JSX

JSX, JavaScript'in syntax uzantısıdır. Bir şablon diline benzer ancak JavaScript özellikleri vardır. JSX, JavaScript nesnelerini return eden `React.createElement()` çağrılarına derlenir. JSX'e temel bir giriş elde etmek için dokümanlara bakın ve <a href="https://omergulcicek.github.io/react/jsx-nedir">burada JSX hakkında daha ayrıntılı bir bilgi</a> bulabilirsiniz.

React DOM, HTML attribute adları yerine camelCase adlandırma kuralını kullanıyor. Örneğin, JSX'de `tabindex`,` tabIndex` olur. `Class` özelliği de JavaScript'de ayrılmış bir sözcük olduğu için` class` niteliği `className` olarak da yazılmıştır:

```js
const name = 'Ömer Gülçiçek';
ReactDOM.render(
  <h1 className="hello">Benim adım {name}!</h1>,
  document.getElementById('root')
);
```  

<h2>Elementler</h2>

React elementleri, React uygulamalarının yapı taşlarıdır. Daha yaygın olarak bilinen component kavramıyla elementler karıştırabilir. Bir element, ekranda görmek istediğiniz şeyi tanımlar. React elementleri değişmez.

```js
const element = <h1>Merhaba Dünya</h1>;
```

Elementler doğrudan kullanılmaz, ancak componentler ile return edilir.

Elementler hakkında detaylı bilgi için <a href="https://omergulcicek.github.io/react/elementleri-render-etmek">elementleri render etmek</a> konusunu inceleyebilirsiniz.

<h2>Componentler</h2>

React componentleri, sayfaya uygulanacak bir React elementini return eden, küçük, tekrar kullanılabilir kod parçacıklarıdır. React componentinin en basit sürümü, React elementi return eden basit bir JavaScript fonksiyonuna örnek olarak:

```js
function Welcome(props) {
  return <h1>Merhaba {props.name}</h1>;
}
```

Componentler ES6 classları ile de yapılabilir:

```js
class Welcome extends React.Component {
  render() {
    return <h1>Merhaba {this.props.name}</h1>;
  }
}
```

Componentler, farklı parçalara bölünebilir ve başka component içinde kullanılabilir. Componentler, diğer componentleri, dizileri, stringleri ve sayıları return edebilir. UI'ızın bir bölümünü birkaç kez kullandıysa (Button, Panel, Avatar) veya kendi başına yeterince karmaşıksa (App, FeedStory, Comment), yeniden kullanılabilir bir component olması küçük parçalara ayırmak iyi bir yoldur. Component adları daima büyük harfle başlamalıdır (<wrapper /> değil, <Wrapper /> olmalı).

Component oluşturma hakkında daha fazla bilgi için <a href="https://omergulcicek.github.io/react/component-ve-props">component</a> dokümanına bakın.

<h3>props</h3>

`props` bir React componentinde, bir üst componentten alt componentlere geçirilen verilerdir.

Unutmayın ki `props`lar yalnızca okunurdur; hiçbir şekilde değiştirilmemelidirler:

```js
// Yanlış!
props.number = 42;
```

<h3>props.children</h3>

Her component için `props.children` mevcuttur. Bir componentin açılış ve kapanış etiketleri arasındaki içeriğe denir. Örneğin:

```js
<Welcome>Merhaba Dünya</Welcome>
```

`Merhaba Dünya` stringi `Welcome` componentinde `props.children`da tutulur:

```js
function Welcome(props) {
  return <p>{props.children}</p>;
}
```

Class componentte ise `this.props.children` ile kullanılır:

```js
class Welcome extends React.Component {
  render() {
    return <p>{this.props.children}</p>;
  }
}
```

<h3>state</h3>

Bir Component, kendisiyle ilişkili bazı veriler zaman içinde değiştiğinde `state`e ihtiyaç duyar.

`state` ile `props` arasındaki en önemli fark, `props`un ana componentten geçirilmiş olmasıdır, ancak `state` componentin kendisi tarafından yönetilmektedir. Bir component propslarını değiştiremez, ancak statei değiştirebilir. Bunu yapmak için, `this.setState()`i çağırmalıdır. Yalnızca class olarak tanımlanan componentlerin state'i olabilir.

<h2>Lifecycle Fonksiyonları</h2>

Lifecycle fonksiyonları, bir componentin farklı aşamalarında yürütülen özel fonksiyonlardır. Component oluşturulduğunda ve DOM'a eklendiğinde (mounting), component güncellendiğinde ve component kaldırıldığında DOM'da çalıştırılan fonksiyonlar vardır.

Lifecycle fonksiyonları hakkında daha fazla bilgi için <a href="https://omergulcicek.github.io/react/lifecycle-fonksiyonlari">lifecycle fonksiyonları</a> dokümanına bakın.

<h2>Keys</h2>

Bir `key` elementin dizileri oluşturulurken eklenmesi gereken özel bir string attributetüdür. Keyler yardımı ile hangi elementlerin değiştiğini, eklendiğini veya kaldırıldığını belirleyebilirsiniz. Elementlere istikrarlı bir kimlik kazandırmak için bir dizideki elemente key verilmelidir.

Keyler yalnızca aynı dizindeki kardeş elementler arasında benzersiz olmalıdır. Tüm uygulamada benzersiz olması gerekmez.

Keylere `Math.random()` gibi bir şey kullanmayın. React keylerinin istikrarlı bir kimliği olması, böylece React'in element ekleme, kaldırma gibi işlemleri belirleyebilmesi için önemlidir. İdeal olarak, keyler verilerinizden gelen benzersiz ve kararlı tanımlayıcılara (örneğin `post.id`) karşılık gelmelidir.

Keyler hakkında daha fazla bilgi için <a href="https://omergulcicek.github.io/react/listeler-ve-keyler">listeler ve keyler</a> dokümanına bakın.

---

<h1>Ajax Kullanımı</h1>

React ile istediğiniz herhangi bir AJAX kütüphanesini kullanabilirsiniz.

Popüler olanlar <a href="https://github.com/axios/axios">Axios</a>, <a href="https://api.jquery.com/jQuery.ajax/">jQuery AJAX</a> ve tarayıcıda yerleşik olarak bulunan <a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API">window.fetch</a>.

<h2>Lifecycleda AJAX isteğini nerede yapmalıyım?</h2>

AJAX isteklerini `componentDidMount` fonksiyonunda kullanmalısınız. AJAX isteğinden gelen veriyi `setState` yardımıyla state'e atarak componentin içerisinde kullanabilirsiniz.

Aşağıdaki component, `state`i doldurmak için `componentDidMount`ta bir AJAX çağrısının nasıl yapılacağını gösterir:

```js
{
  items: [
    { id: 1, name: 'Apples', price: '$2' },
    { id: 2, name: 'Peaches', price: '$5' }
  ] 
}
```

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      error: null,
      isLoaded: false,
      items: []
    };
  }

  componentDidMount() {
  //AJAX isteğini burada başlatıyoruz.
    fetch("https://api.example.com/items")
      .then(res => res.json())
      .then(
        (result) => {
        //AJAX'tan gelen veri ile state'imizi güncelliyoruz.
          this.setState({
            isLoaded: true,
            items: result.items
          });
        },
        (error) => {
          this.setState({
            isLoaded: true,
            error
          });
        }
      )
  }

  render() {
    const { error, isLoaded, items } = this.state;
    if (error) {
      return <div>Error: {error.message}</div>;
    } else if (!isLoaded) {
      return <div>Yükleniyor...</div>;
    } else {
      return (
        <ul>
          {items.map(item => (
            <li key={item.name}>
              {item.name} {item.price}
            </li>
          ))}
        </ul>
      );
    }
  }
}
```

<i>Gelişmiş kılavuzlar sonlanmıştır. Bu aşamadan sonra <b>Uygulamalı Eğitime</b> geçiş yapılacaktır.</i>

---

<h1>XOX Oyunu</h1>

Uygulamalı olarak adım adım XOX oyununu geliştireceğiz, projenin bitmiş hali şudur: <a href="https://codepen.io/gaearon/pen/LyyXgK?editors=0010">XOX Oyunu<a>

CSS kodları hazır olarak verilmiş durumda, biz sadece JavaScript geliştirmesi yapacağız.

XOX oyunu için görseldeki gibi 3x3'lük bir oyun alanına ihtiyacımız vardır.

<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSakAazYLzTjHx9BcWWc2mcfuu7Lt9ZH2xU6ee-x0MojyNLYb3w" height="100">

Burada her bir kareyi oluşturan componentimizin adı `Square` olacak.

9 kareyi birleştirerek oyun alanını render eden componentimizin adı ise `Board` olacak.

`Game` componenti ise tüm içeriği kapsayan bir tablo render edecek.

Yani başlıca üç componente sahibiz:

- Square
- Board
- Game

Başlangıç için <a href="https://codepen.io/gaearon/pen/oWWQNa?editors=0010">XOX Başlangıç Kodu</a>nu kullanacağız.

Kod uzun ve karmaşık gelebilir, fakat incelediğinizde basit şeyler ile oluşturulduğunu ve aslında karmaşık olmadığını anlayacaksınız. Yeterli düzeyde olduğunuzu düşünmüyorsanız <a href="https://omergulcicek.github.io/react/merhaba-dunya">react dokümanının en başına</a> dönerek bilgilerinizi tazeleyebilirsiniz.

---

<h1>Verileri Props Üzerinden Geçirmek</h1>

`Board` componentinden `Square` componentine bazı verileri geçirmeyi deneyelim.

Board'un `renderSquare` fonksiyonunda, bir `value` propsu `Square`ye geçirmek için kodu değiştirin:

```js
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
```

Daha sonra `{/ * TODO * /}` yazan kısmı `{this.props.value}` ile Square'ın `render` fonksiyonunu değiştirin:

```js
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

Önce: <i>Kodun ilk halinde karelerin içi boştu.</i>

<img src="https://reactjs.org/static/tictac-empty-1566a4f8490d6b4b1ed36cd2c11fe4b6-a9336.png" height="200" />

Sonra: Render edilmiş çıktıda her karede bir sayı görmeniz gerekiyor.

<img src="https://reactjs.org/static/tictac-numbers-685df774da6da48f451356f33f4be8b2-be875.png" height="200" />

<a href="https://codepen.io/gaearon/pen/aWWQOG?editors=0010">Mevcut kodu görüntüleyin</a>

<i>`Board` componentinin render fonksiyonundan `this.renderSquare()` fonksiyonu çağırılıyor. Parametre olarak ise 0'dan 8'e kadar parametreler gönderilmiş. `this.renderSquare` fonksiyonu ise `Square` componentini return ediyordu. Fakat içerisinde herhangi bir içerik yoktu. `value={i}` yaparak `Square` componentine `value` değerleri gönderdik. `Square` componentinde ise gelen bu valueyu `this.props.value` ile yazdırdık. Böylece oyun alanımızda karelerde 0'dan 8'e kadar rakamlar yazdırarak verileri props üzerinden componente geçirmiş olduk.</i>

---

<h1>Etkileşimli Component</h1>

`Square` componentine tıkladığınızda bir "X" işareti dolduracak şekilde güncelleyelim. `Square` componentinde `render()` fonksiyonunu şöyle değiştirmeyi deneyin:


```js
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={() => alert('tıklandı')}>
        {this.props.value}
      </button>
    );
  }
}
```

Bir kareye tıklarsanız, tarayıcınızda alert (<i>uyarı</i>) almanız gerekiyor.

Burada JavaScript ok fonksiyon syntaxı kullanılmıştır. Fonksiyonu `onClick` propsu olarak geçtiğimizi unutmayın.

<i>Normalde click change gibi olaylarda bind etmek gerekiyor fakat ok fonksiyonu ve bazı diğer yöntemleri kullanarak constructorde bind etmedende click ve change'i kullanabiliyoruz. Detaylar için <a href="https://omergulcicek.github.io/react/click-ve-change-olaylari">click ve change olayları</a> başlığına bakabilirsiniz.</i>

`OnClick = {alert ('tıklandı')}` olarak yazsaydık, click yapmak yerine sadece uyarırdı.

React componentleri, constructorde `this.state`e sahip olabilirler; bu component için özel olarak düşünülmelidir. Kareye tıklatıldığında değişmesini sağlayalım.

İlk önce, state'i başlatmak için classa bir constructor ekleyin:

```js
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => alert('tıklandı')}>
        {this.props.value}
      </button>
    );
  }
}
```

JavaScript classlarında, bir alt clasın constructorünü tanımlarken, `super();`i çağırmanız gerekir.

Şimdi ise click yapıldığında karede X yazması için state'i güncelleyecek şekilde kodumuzu değiştirelim.

* `this.props.value`u `this.state.value` ile `<button>` etiketinin içinde değiştirin.

<i>Önceki halinde üst componentten parametre alıyorduk fakat artık state'teki değeri alacağımız için `props` yerine `state` kullanmalıyız.</i>

* `() => alert()`ı `() => this.setState({value: 'X'})` olacak şekilde değiştirin.

<i>Daha sonra X ve O yazması için gerekli kodları ekleyeceğiz. Şimdilik her click yapıldığında stateteki valueyu X olacak şekilde güncelliyoruz. State güncellendiğinde component tekrardan render edildiği için güncel değeri karenin içerisine yazacaktır.</i>

Şimdi `<button>` tagımız şu şekilde görünmelidir:

```js
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => this.setState({value: 'X'})}>
        {this.state.value}
      </button>
    );
  }
}
```

`this.setState` çağrıldığında, component için bir güncelleme planlanır ve componenti alt öğeleri ile birlikte yeniden render edilmesine neden olur. Component yeniden render edildiğinde, `this.state.value` `X` olur, böylece karede bir X görürsünüz.

Herhangi bir kareyi tıklarsanız, içinde bir X görünmelidir.

<a href="https://codepen.io/gaearon/pen/VbbVLg?editors=0010">Mevcut kodu görüntüleyin</a>

---

<h1>Veriyi Korumanın Önemi</h1>

Önceki kod örneğinde, `.slice()` fonksiyonunu kullanarak `squares` dizisinde değişiklik yapmadan önce kopyalamayı ve varolan dizinin orijinal halini korumanızı öneririz. Bunun ne anlama geldiğini ve neden önemli bir konu olduğunu konuşalım.

Verileri değiştirmek için genellikle iki yol vardır. İlk yöntem, bir değişkenin değerlerini doğrudan değiştirmek. İkinci yöntem ise veriyi istenen değişiklikleri de içeren yeni bir kopyasını oluşturmaktır.

<h3>Veriyi Doğrudan Değiştirmek</h3>

```js
var player = {score: 1, name: 'Ömer'};
player.score = 2;
// player objesinin son hali: {score: 2, name: 'Ömer'}
```

<h3>Verinin Kopyasını Oluşturmak</h3>

```js
var player = {score: 1, name: 'Ömer'};

var newPlayer = Object.assign({}, player, {score: 2});
// player objesi değişmedi ve kopyası oluşuturup score değerinde güncelleme yapıldı.
// newPlayer objesinin son hali: {score: 2, name: 'Ömer'}

// Veya obje yayılım syntax kullanıyorsanız, şu şekilde de yazabilirsiniz:
// var newPlayer = {...player, score: 2};
```

<h4>Daha Kolay Geri Alma / Yeniden Yapmak</h4>

Değişmezlik ayrıca bazı karmaşık özelliklerin uygulanmasını çok daha kolay hale getirir. Örneğin, bu eğitimde oyunun farklı aşamaları arasında zaman yolculuğu yapacağız.

<i>XOX oynarken önceki adımlara gidebilmek için adım adım aşamaları kayıt altına almak gerekiyor. Daha sonra uygulamamızın sağ tarafına, önceki adımlara gidebilmek için butonlar ekleyeceğiz.</i>

Değişmezlik ayrıca bazı karmaşık özelliklerin uygulanmasını çok daha kolay hale getirir. Örneğin, bu eğitimde oyunun farklı aşamaları arasında zaman yolculuğu yapacağız.

<h4>Track Değişiklikleri</h4>

Değişikliğe uğrayan bir objenin değişip değişmediğini belirlemek zordur, çünkü değişiklikler doğrudan objeye yapılır. Bu daha sonra, geçerli objeyi önceki bir kopyayla karşılaştırma, tüm obje ağacını çaprazlama ve her değişkeni ve değeri karşılaştırmayı gerektirir. Bu süreç giderek daha karmaşık hale gelebilir.

Değiştirilebilir bir objenin nasıl değiştiğini belirlemek oldukça kolay. Objenin son hali daha öncekinden farklıysa obje değişmiş demektir, bu kadar.

<h4>Reactın Ne Zaman Yeniden Render Edileceğini Belirleme</h4>

React'te değiştirilemezliğin en büyük yararı, saf componentleri oluşturduğunuzda gelir. Değişmez veriler, değişikliklerin yapılıp yapılamadığını daha kolay belirleyebildiğinden, bir componentin ne zaman yeniden oluşturulmasını istediğini belirlemeye yardımcı olur.

<h3>Fonksiyonel Componentler</h3>

Constructorü kaldırdık ve aslında React, fonksiyonel component olarak adlandırılan yalnızca bir `render` fonksiyonundan oluşan Square gibi component türleri için daha basit bir syntax destekliyor. `extends React.Component` gibi uzunca class tanımlamak yerine props alan ve render edilecek olanı return eden bir fonksiyon yazın.

Tüm Square classını bu fonksiyonla değiştirin:

```js
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```

Uygulamalarınızdaki birçok component fonksiyonel component olarak yazılabilir. Bu componentleri yazmak daha kolaydır ve React tarafından optimize edilirler.

`onClick={() => props.onClick()}`i de yalnızca `onClick={props.onClick()}` olarak değiştirdik. `onClick={props.onClick()}` işe yaramayacağına dikkat edin, çünkü onu aşağıya aktarmak yerine `props.onClick`i çağırırdı.

<a href="https://codepen.io/gaearon/pen/QvvJOv?editors=0010">Mevcut kodu görüntüleyin</a>

---

<h1>Sıradaki Oyuncu</h1>

Oyunumuzda bariz bir hata bulunmakta, sadece X hamle yapabiliyor; bunu düzeltelim.

Varsayılan ilk hareketin 'X' olacağına karar verelim. Başlangıç state'ini `Board` constructoründe değiştirelim:

```js
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }
```

Her hamle yapıldığında `xIsNext` değerini değiştirerek sıranın `X` ya da `O`ya geçmesini sağlayalım. Board'un `handleClick` fonksiyonunu` xIsNext` değerini değiştirmek için güncelleyin:

```js
  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

Şimdi X ve O sırayla hamle yapacak. Ardından, Board'un `render` fonksiyonu içindeki `status` stringini de değiştirip, sıradaki oyuncunun kim olduğunu gösterelim:

```js
  render() {
    const status = 'Sıradaki Oyuncu: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      // geri kalan kodlar değişmedi
```

Bu değişikliklerden sonra Board componentinin son hali şu şekilde olmalı:

```js
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Sıradaki Oyuncu: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

<a href="https://codepen.io/gaearon/pen/KmmrBy?editors=0010">Mevcut kodu görüntüleyin</a>

---

<h1>Kazananı Bildirmek</h1>

Bir oyunun ne zaman kazanılacağını gösterelim. Bu fonksiyonu dosyanın sonuna ekleyin:

```js
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

Birisi oyunu kazanırsa, kimin kazanıp kazanmadığını kontrol etmek ve state metnini "Kazanan: [X/O]" gösterilmesini sağlamak için `Board` componentinin `render` fonksiyonuna gerekli kodları ekleyelim.

Board'un `render`ındaki `status` bildirimini şu kodla değiştirin:

```js
  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Kazanan: ' + winner;
    } else {
      status = 'Sıradaki Oyuncu: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      // geri kalanı değişmedi
```

Artık, oyunda birisi kazanmışsa veya bir kare zaten doldurulmuşsa tıklamayı erkenden return etmek için `Board`un `handleClick`ini değiştirebilirsin:

```js
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

Tebrik ederiz! Artık tic-tac-toe oyunu geliştirdiniz. Ve şimdi React'in temellerini uygulamalı olarak gördünüz. Burada asıl kazanan sizsiniz !

<a href="https://codepen.io/gaearon/pen/LyyXgK?editors=0010">Mevcut kodu görüntüleyin</a>

---
