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

* JSX ile bir string yerine event işleyicisi olarak bir fonskyion iletirsiniz.

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

  clickOlayi() {
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

<a href="https://omergulcicek.github.io/reactjs/sartli-render">Sıradaki Eğitim: Şartlı Render</a>
