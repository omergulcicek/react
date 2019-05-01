<h1>React JS Kurulumu</h1>

Online olarak katılmayı deneyin ya da local geliştirme ortamınızı oluşturun.

<h2>Online Kod Ortamı</h2>

React'i online kod ortamında denemek istiyorsanız, <a href="https://codepen.io/omergulcicek/pen/ypMLXP">CodePen</a> ya da <a href="https://codesandbox.io/s/new">CodeSandbox</a> sitelerini kullanabilirsiniz.

<h2>React HTML Şablonu</h2>

Kendi text editörünüzü kullanmayı tercih ederseniz, <a href="https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html">bu HTML dosyasını</a> indirebilir, düzenleyebilir ve tarayıcınızdaki local dosya sisteminden açabilirsiniz. Kod dönüştürmesini yavaş yapar, bu nedenle sadece öğrenme aşamasında kullanın, projeleriniz için kullanmayın.

<h2>Hızlı Başlangıç</h2>

React kavramlarına adım adım bir giriş için <a href="https://omergulcicek.github.io/react/hizli-baslangic/merhaba-dunya">hızlı başlangıç bölümü</a>ne gidin.

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

<a href="https://omergulcicek.github.io/react/hizli-baslangic/merhaba-dunya">İlk Konu: React JS ile Merhaba Dünya</a>
