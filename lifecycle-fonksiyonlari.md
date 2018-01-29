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

`null` yada `false` return ederkem, `ReactDOM.findDOMNode(this)` `null` return eder.

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

```javascript
componentDidUpdate(prevProps, prevState)
```

`componentDidUpdate()`, güncelleme gerçekleştikten hemen sonra çağrılır. Bu fonksiyon ilk render için çağrılmaz.

Bunu, component güncellendiğinde DOM üzerinde çalışmak için kullanın. Bu ayrıca, mevcut yeri önceki yerlerle kıyasladığınız sürece network istekleri yapmak için iyi bir yerdir (örneğin props değişmediğinde bir network isteği gerekmeyebilir).

> Not
>
> `shouldComponentUpdate()` false return ederse, `componentDidUpdate()` çağrılmayacaktır.

* * *

<h3>componentWillUnmount()</h3>

```javascript
componentWillUnmount()
```

`componentWillUnmount()`, bir component unmounted ve destroyed edilmeden hemen önce çağrılır. Bu fonksiyonda, zamanlayıcıları geçersiz kılma, network isteklerini iptal etme veya `componentDidMount()` fonksiyonunda oluşturulan abonelikleri temizleme gibi gerekli temizliği yapın.

* * *

<h3>componentDidCatch()</h3>

```javascript
componentDidCatch(error, info)
```

Hata sınırları, alt component ağacının herhangi bir yerindeki JavaScript hatalarını yakalayan, bu hataları log'a yazan ve çöktüğü compoennt ağacı yerine bir yedek UI görüntüleyen React componentleridir. Hata sınırları, render, lifecycle fonksiyonlar ve altındaki ağacın constructorlerinde hataları yakalar.

Beklenmedik istisnalardan kurtarmak için yalnızca hata sınırlarını kullanın; onları kontrol akışı için kullanmaya çalışmayın.

Daha fazla ayrıntı için React 16'daki <a href="https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html">Error Handling</a> bölümüne bakın.

> Not
>
> Hata sınırları yalnızca alt componentlerin içindeki hataları yakalar . Bir hata sınırı kendi içinde bir hata yakalayamaz.

* * *


<i>Bu kısım güncellenecek...</i>

<a href="https://omergulcicek.github.io/reactjs/react-terimler-sozlugu">Sıradaki Gelişmiş Kılavuz: React Terimler Sözlüğü</a>
