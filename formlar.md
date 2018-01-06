<h1>Formlar</h1>

HTML form elemanları, React'te diğer DOM elemanlarından biraz farklı çalışır, çünkü form elemanlarının kendilerine has iç stateleri vardır.
Örneğin, bu kod HTML'de bir form içerisinde `ad` girişi ister:

```html
<form>
  <label>
    Adınız:
    <input type="text" name="ad" />
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

Örneğin, bir önceki örnekte, `ad` değerinin yazılıp submit edildiğinde `ad`ı alert ile yazdırmak istiyorsak,
formu kontrollü bir component olarak oluşturabiliriz:

```javascript
class Form extends React.Component {
  constructor(props) {
    super(props);
    this.state = {deger: ''};

    this.degisiklikOldu = this.degisiklikOldu.bind(this);
    this.submitEdildi = this.submitEdildi.bind(this);
  }

  degisiklikOldu(event) {
    this.setState({deger: event.target.value});
  }

  submitEdildi(event) {
    alert("Submit'lenen değer: " + this.state.deger);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.submitEdildi}>
        <label>
          Adınız:
          <input type="text" value={this.state.deger} onChange={this.degisiklikOldu} />
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

Kontrollü bir componentte her state değişimi, `degisiklikOldu` fonksiyonunu çalıştıracaktır.
Örneğin, adın büyük harflerle yazılmasını isteseydik, `degisiklikOldu` fonksiyonunu şu şekilde yazabilirdik:


```javascript
degisiklikOldu(event) {
  this.setState({deger: event.target.value.toUpperCase()});
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
class Form extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      deger: "Bu kısma bir şeyler yazın."
    };

    this.degisiklikOldu = this.degisiklikOldu.bind(this);
    this.submitEdildi = this.submitEdildi.bind(this);
  }

  degisiklikOldu(event) {
    this.setState({value: event.target.deger});
  }

  submitEdildi(event) {
    alert("Submit'lenen değer: " + this.state.deger);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.submitEdildi}>
        <label>
          <textarea value={this.state.deger} onChange={this.degisiklikOldu} />
        </label>
        <input type="submit" value="Gönder" />
      </form>
    );
  }
}
```

`this.state.deger`in constructor'te başlatıldığına dikkat edin, böylece `textarea` içerisinde varsayılan olarak bu yazı bulunacaktır.

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
class Form extends React.Component {
  constructor(props) {
    super(props);
    this.state = {deger: "Trabzon"};

    this.degisiklikOldu = this.degisiklikOldu.bind(this);
    this.submitEdildi = this.submitEdildi.bind(this);
  }

  degisiklikOldu(event) {
    this.setState({value: event.target.value});
  }

  submitEdildi(event) {
    alert('Your favorite flavor is: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.submitEdildi}>
        <label>
          En sevdiğiniz il:
          <select value={this.state.deger} onChange={this.degisiklikOldu}>
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

```javascript
class Rezervasyon extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      gelmeDurumu: true,
      misafirSayisi: 2
    };

    this.degisiklikOldu = this.degisiklikOldu.bind(this);
  }

  degisiklikOldu(event) {
    const hedef = event.target;
    const deger = hedef.type === 'checkbox' ? hedef.checked : hedef.value;
    const ad = hedef.name;

    this.setState({
      [ad]: deger
    });
  }

  render() {
    return (
      <form>
        <label>
          Yemeğe geliyor musunuz?
          <input name="gelmeDurumu"
                 type="checkbox"
                 checked={this.state.gelmeDurumu}
                 onChange={this.degisiklikOldu} />
        </label>
        <br />
        <label>
          Sizinle gelecek olan misafir sayısı:
          <input name="misafirSayisi"
                 type="number"
                 deger={this.state.misafirSayisi}
                 onChange={this.degisiklikOldu} />
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
  [ad]: deger
});
```

Buda ES5'teki eşdeğer kodudur.

```js
var kismiState = {};
kismiState[ad] = deger;
this.setState(kismiState);
```

<h2>Kontrollü Giriş Boş Değer</h2>

Kontrollü bir component üzerindeki props'u belirlemek, kullanıcının isteği dışında girişi değiştirmesini önler.
`deger` belirttiyseniz ancak girdi hala düzenlenebilir ise, yanlışlıkla `deger`i ` undefined` veya `null` olarak ayarlamış olabilirsiniz.

Aşağıdaki kod bunu göstermektedir.
(Giriş ilk önce kilitlenir ancak kısa bir gecikme sonrasında düzenlenebilir hale gelir.)

```javascript
ReactDOM.render(<input value="merhaba" />, document.getElementById("root"));

setTimeout(function() {
  ReactDOM.render(<input value={null} />, document.getElementById("root"));
}, 1000);

```

<a href="https://omergulcicek.github.io/reactjs/state-guncellemek">Sıradaki Eğitim: State Güncellemek</a>
