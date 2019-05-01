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

<a href="https://omergulcicek.github.io/react/gelismis-kilavuzlar/react-terimler-sozlugu">Sıradaki Gelişmiş Kılavuz: React Terimler Sözlüğü</a>
