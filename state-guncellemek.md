<h1>State Güncellemek</h1>

Çoğu zaman, birden çok componentin aynı state'i yansıtması gerekir. Bu bölümde, suyun belirli bir sıcaklıkta kaynayıp kaynayamayacağını hesaplayan fonksiyonları oluşturacağız.

`BoilingVerdict` adlı bir componentle başlayacağız.
`Celsius` sıcaklığını bir props ile parametre olarak kabul eder ve suyu kaynatmaya yetecek kadar olup olmadığını return eder:

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

Şimdi yapacağımız şey ise Celsius girdisine ek olarak, bir Fahrenheit girişi sağlamak.

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
    // Before: const temperature = this.state.temperature;
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
Mevcut input'un `temperature` ve `scale` değerlerini state'de tutarız.

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

<a href="https://omergulcicek.github.io/reactjs/composition-ve-inheritance">Sıradaki Eğitim: Composition ve Inheritance</a>
