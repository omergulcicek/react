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

<a href="https://omergulcicek.github.io/reactjs/state-guncellemek">Sıradaki Eğitim: State Güncellemek</a>
