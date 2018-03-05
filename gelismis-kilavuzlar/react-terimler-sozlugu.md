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

JSX, JavaScript'in syntax uzantısıdır. Bir şablon diline benzer ancak JavaScript özellikleri vardır. JSX, JavaScript nesnelerini return eden `React.createElement()` çağrılarına derlenir. JSX'e temel bir giriş elde etmek için dokümanlara bakın ve <a href="https://omergulcicek.github.io/reactjs/jsx-nedir">burada JSX hakkında daha ayrıntılı bir bilgi</a> bulabilirsiniz.

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

Elementler hakkında detaylı bilgi için <a href="https://omergulcicek.github.io/reactjs/elementleri-render-etmek">elementleri render etmek</a> konusunu inceleyebilirsiniz.

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

Component oluşturma hakkında daha fazla bilgi için <a href="https://omergulcicek.github.io/reactjs/component-ve-props">component</a> dokümanına bakın.

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

Lifecycle fonksiyonları hakkında daha fazla bilgi için <a href="https://omergulcicek.github.io/reactjs/lifecycle-fonksiyonlari">lifecycle fonksiyonları</a> dokümanına bakın.

<h2>Keys</h2>

Bir `key` elementin dizileri oluşturulurken eklenmesi gereken özel bir string attributetüdür. Keyler yardımı ile hangi elementlerin değiştiğini, eklendiğini veya kaldırıldığını belirleyebilirsiniz. Elementlere istikrarlı bir kimlik kazandırmak için bir dizideki elemente key verilmelidir.

Keyler yalnızca aynı dizindeki kardeş elementler arasında benzersiz olmalıdır. Tüm uygulamada benzersiz olması gerekmez.

Keylere `Math.random()` gibi bir şey kullanmayın. React keylerinin istikrarlı bir kimliği olması, böylece React'in element ekleme, kaldırma gibi işlemleri belirleyebilmesi için önemlidir. İdeal olarak, keyler verilerinizden gelen benzersiz ve kararlı tanımlayıcılara (örneğin `post.id`) karşılık gelmelidir.

Keyler hakkında daha fazla bilgi için <a href="https://omergulcicek.github.io/reactjs/listeler-ve-keyler">listeler ve keyler</a> dokümanına bakın.

<i>Gelişmiş kılavuzlar sonlanmıştır. Bu aşamadan sonra <b>Uygulamalı Eğitim</b>e geçiş yapılacaktır.</i>

<a href="https://omergulcicek.github.io/reactjs/uygulamali-egitim/xox-oyunu">Sıradaki Eğitim: XOX Oyunu</a>
