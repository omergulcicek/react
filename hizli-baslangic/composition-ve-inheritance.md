<h1>Composition ve Inheritance</h1>

React'ın güçlü bir modeli var ve componentler arasında kodu tekrar kullanmak için
`inheritance` (<i>miras</i>) yerine `composition` (<i>birleşim</i>) kullanılmasını öneriyoruz.

Bu bölümde, React'e yeni gelen geliştiricilerin genellikle inheritance ile ilgili karşılaştığı birkaç sorunu ele alacağız
ve bunları compositionlarla nasıl çözebileceğimizi göstereceğiz.

<h2>Containment (Kapsama)</h2>

Bazı componentler önceden çocuklarını bilmezler.

Bu, genel kutuları temsil eden `Sidebar` veya `Dialog` gibi componentler için özellikle geçerlidir.

Bu tür componentlerin, çocuklarını doğrudan çıktılarına yerleştirmek için `children` kullanmalarını öneriyoruz:

<i>Bildiğiniz gibi, `props` sayesinde o componente tüm attributeleri alıyorduk.
`props.children` dediğimizde ise o componente yerleştirilmiş child (çocuk) componentleri/içeriği (vb) alıyoruz.</i>

```js
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}
```

<i>Yukarıdaki `FancyBorder` componenti bir `div` return ediyor.
Bu div ise props ile `color`ı parametre olarak alacak.</i>

<i>Alttaki `WelcomeDialog` componenti ise `FancyBorder` componentini return ediyor ve renk olarakta `blue` gönderilmiş.</i>

```js
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Hoşgeldiniz
      </h1>
      <p className="Dialog-message">
        Bu dokümantasyonu starlayarak destek olabilirsiniz!
      </p>
    </FancyBorder>
  );
}
```

<a href="https://codepen.io/gaearon/pen/ozqNOV?editors=0010">CodePen'de Deneyin</a>

`<FancyBorder>` JSX etiketinin içindeki herhangi bir şey `children` olarak `FancyBorder` componentine geçirilir.

Aşağıdaki yöntem daha az yaygındır, ancak bazen kullanılabiliyor.
Bu gibi durumlarda `children` kullanmak yerine kendi yöntemlerinizi hazırlayabilirsiniz:

```js
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
```

<a href="https://codepen.io/gaearon/pen/gwZOJp?editors=0010">CodePen'de Deneyin</a>

<i>Burada atrribute olarak `SplitPane` componentine `left` ve `right` propslarına component gönderilmiştir.
Propslar ile bir yazı, rakam, değişken, component gibi her hangi bir şeyi gönderebilirsiniz.</i>

<h2>Uzmanca Kod</h2>

Bazen componentleri, diğer componentlerin "özel durumları" olarak düşünürüz.

React'te bu, daha "özel" bir componentin daha "jenerik" bir component oluşturduğu ve props ile yapılandırdığı composition ile elde edilir:

```js
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog
      title="Hoşgeldiniz"
      message="Bu dokümantasyonu starlayarak destek olabilirsiniz!" />
  );
}
```

<a href="https://codepen.io/gaearon/pen/kkEaOZ?editors=0010">CodePen'de Deneyin</a>

Aşağıdaki daha karışık olan örneği inceleyerek anlamaya çalışın:

```js
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
      {props.children}
    </FancyBorder>
  );
}

class SignUpDialog extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.handleSignUp = this.handleSignUp.bind(this);
    this.state = {login: ''};
  }

  render() {
    return (
      <Dialog title="Mars Keşif Programı"
              message="Size nasıl başvurmalıyız?">
        <input value={this.state.login}
               onChange={this.handleChange} />
        <button onClick={this.handleSignUp}>
          Kayıt Ol
        </button>
      </Dialog>
    );
  }

  handleChange(e) {
    this.setState({login: e.target.value});
  }

  handleSignUp() {
    alert(`Uçağa hoşgeldiniz, ${this.state.login}!`);
  }
}
```

<a href="https://codepen.io/gaearon/pen/gwZbYa?editors=0010">CodePen'de Deneyin</a>

<h2>Inheritance Hakkında</h2>

Facebook binlerce componentte React kullanıyor ve component hiyerarşileri oluştururken önerdiğimiz herhangi bir kullanım durumu bulamadık.

Props and compositionlar, componentin görünümünü ve davranışını açık ve güvenli bir şekilde özelleştirmeniz için gereken tüm esnekliği verir.

Componentler arasında UI olmayan işlevselliği yeniden kullanmak istiyorsanız ayrı bir JavaScript modülü içine ayıklamanızı öneririz.
Componentler içe aktarabilir ve bu fonksiyonu, nesneyi veya bir sınıfı uzatmadan kullanabilir.

<i>Konu anlatımları sonlanmıştır. Bu aşamadan sonra <b>Gelişmiş Kılavuzlar</b> konularına geçiş yapılacaktır.</i>

<a href="https://omergulcicek.github.io/react/gelismis-kilavuzlar/derinlemesine-jsx">Sıradaki Gelişmiş Kılavuz: Derinlemesine JSX</a>
