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

<i>Lifecycle fonksiyonları ile ilgili detaylı bilgi için <a href="https://omergulcicek.github.io/reactjs/state-ve-lifecycle">State ve lifecycle</a> konusunda <b>"Bir Classa Lifecycle Fonksiyonları Ekleme"</b> başlığını inceleyebilirsiniz.</i>

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

<a href="https://omergulcicek.github.io/reactjs/gelismis-kilavuzlar/jsx-olmadan-react">Sıradaki Gelişmiş Kılavuz: JSX Olmadan React</a>
