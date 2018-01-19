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

ES6'yı henüz kullanmıyorsanız, bunun yerine `create-react-class` modülünü kullanabilirsiniz. Daha fazla bilgi edinmek için <a href="https://omergulcicek.github.io/reactjs/es6-olmadan-react">ES6 olmadan React</a> konusuna bakın.

Unutmayın, kendi temel component classlarınızı oluşturmanızı önermiyoruz. Kodun tekrar kullanımı React'te inheritancetan ziyade composition yoluyla elde edilir. Composition kullanma konusunda bir fikir edinmek için <a href="https://omergulcicek.github.io/reactjs/composition-ve-inheritance">composition ve inheritance</a> sayfasını inceleyin.

Her componentin, lifecycle  fonksiyonları vardır. İçerisinde `will` geçen fonksiyonlar component oluşturulmasından hemen önce çağrılırken, içerisinde `did` geçen fonksiyonlar component kaldırıldıktan sonra çağrılır.

<i>Şimdi tüm fonksiyonları bölümlendirip, ardından her birini açıklayacağız. Başlıklara çeviri yapılmamıştır, altlarına Türkçesi eklenmiştir.</i>

<h4>Mounting</h4>

<i>Oluşturmak</i>

Bu fonksiyonlar, bir component örneği oluşturulurken ve DOM'a eklendiğinde çağrılır:

- [`constructor()`](#constructor)
- [`componentWillMount()`](#componentwillmount)
- [`render()`](#render)
- [`componentDidMount()`](#componentdidmount)

<h4>Updating</h4>

<i>Güncellemek</i>

Bir güncelleme, props ya da state değişikliklerinden kaynaklanabilir. Bu fonksiyonlar, bir componentin güncellenmesiyle çağrılır.

- [`componentWillReceiveProps()`](#componentwillreceiveprops)
- [`shouldComponentUpdate()`](#shouldcomponentupdate)
- [`componentWillUpdate()`](#componentwillupdate)
- [`render()`](#render)
- [`componentDidUpdate()`](#componentdidupdate)

<h4>Unmounting</h4>

<i>Kaldırmak</i>

Bu fonksiyon, bir component DOM'dan kaldırıldığında çağrılır:

- [`componentWillUnmount()`](#componentwillunmount)

<h4>Error Handling</h4>

<i>Hata işleme</i>

Bu fonksiyon, render sırasında lifecycle fonksiyonlarında veya herhangi bir alt componentin constructoründe bir hata olduğunda çağrılır.

- [`componentDidCatch()`](#componentdidcatch)

<h3>Diğer API'ler</h3>

Her component aşağıdaki API'leride içerisinde barındırır:

- [`setState()`](#setstate)
- [`forceUpdate()`](#forceupdate)

<h3>Class Propertyleri</h3>

- [`defaultProps`](#defaultprops)
- [`displayName`](#displayname)

<h3>Instance Propertyleri</h3>

- [`props`](#props)
- [`state`](#state)

* * *

<h3>`render()`</h3>

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

`null` yada `false` return ederkem, `ReactDOM.findDOMNode(this)` `null` return eder.

`render()` fonksiyonu, componentin state'ini değiştirmez, çağrıldığında her seferinde aynı sonucu return eder. Tarayıcıyla etkileşime girmeniz gerekiyorsa, bunun yerine ` componentDidMount()` ya da diğer lifecycle fonksiyonları ile çalışmalarınızı gerçekleştirin.

> Not
>
> `shouldComponentUpdate()` fonksiyonu `false` return ederse `render()` çağrılmayacaktır.

* * *

<h3>`constructor()`</h3>

```js
constructor(props)
```

Bir React componentinin constructorü, oluşturulmadan önce çağrılır. Bir `React.Component` alt sınıfı için constructorü uygularken, herhangi bir koddan önce `super(props)`u çağırmalısınız. Aksi takdirde, `this.props` constructorde hatalara neden olur.

Constructore herhangi bir abonelik sunmaktan kaçının. Bunun yerine, `componentDidMount()` kullanın.

Constructor, state'i başlatmak için doğru yerdir. Bunu yapmak için sadece bir nesneyi `this.state`e atayın; Constructor'den `setState()` fonksiyonunu çağırmaya çalışmayın. Constructor ayrıca, click-change olaylarını bind etmek için sıklıkla kullanılır.

<i>Bind fonksiyonu hakkında detaylı bilgiye kendi yazmış olduğum <a href="https://omergulcicek.com/blog/bind-fonksiyonu">Bind() fonksiyonu</a> adlı makaleden erişebilirsiniz.</i>

State, click-change olaylarını kullanmayacaksanız, React componenti için bir constructor oluşturmak zorunda değilsiniz.

* * *

<h3>`componentWillMount()`</h3>

```js
componentWillMount()
```

`componentWillMount()`, component oluşturulmadan hemen önce çağrılır, dolayısıyla bu yöntemde eş zamanlı olarak `setState()` başlamayacaktır. Genellikle, bunun yerine `constructor()`ü kullanmanızı öneririz.

* * *

<h3>`componentDidMount()`</h3>

```js
componentDidMount()
```

`componentDidMount()`, bir component render edildikten hemen sonra çağrılır. Uzak bir uç noktadan veri yüklemeniz gerekiyorsa, bu ağ isteğini başlatmak için iyi bir yerdir.

Bu fonksiyon, herhangi bir abonelik ayarlamak için iyi bir yerdir. Bunu yaparsanız, `componentWillUnmount ()` da aboneliğinizi iptal etmeyi unutmayın.

Bu yöntemde `setState()` çağrısı ek bir render işlemine neden olur, ancak tarayıcı ekranını güncellemeden önce gerçekleşir. `render()` fonksiyonunun bu durumda iki kez çağrılmasına rağmen kullanıcının ara state'i göremez. Bu kalıp sıklıkla performans sorunlarına neden olduğundan dikkatli kullanın. 

* * *

<i>Bu kısım güncellenecek...</i>

<a href="https://omergulcicek.github.io/reactjs/react-terimler-sozlugu">Sıradaki Gelişmiş Kılavuz: React Terimler Sözlüğü</a>
