<h1>Şartlı Render</h1>

React ile ihtiyacınız olan davranışı kapsayan farklı componentler oluşturabilirsiniz.
Daha sonra, uygulamanızın state'ine bağlı olarak yalnızca bir kısmını görüntüleyebilirsiniz.

React'te şartlı render, JavaScript koşulları ile aynı şekilde çalışır.
Geçerli durumu temsil eden elemanlar oluşturmak için `if` veya koşullu operatör gibi JavaScript operatörlerini kullanın
ve bunları eşleştirmek için  UI'ı güncelleştirmeye izin verin.

Bu iki componenti düşünün:

```js
function UserGreeting(props) {
  return <h1>Tekrardan hoşgeldin!</h1>;
}

function GuestGreeting(props) {
  return <h1>Lütfen üye ol.</h1>;
}
```

Bir kullanıcının oturum açıp açmadığına bağlı olarak bu componentlerin herhangi birini görüntüleyen bir
`Greeting` componenti oluşturacağız:

```js
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // isLoggedIn={true} olarak değiştirip farkı test edebilirsiniz.
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/ZpVxNq?editors=0011">CodePen'de Deneyin</a>

<i>Adım adım incelemekte fayda var.

1. İlk olarak ReactDOM, `Greeting` componentini render ediyor.

2. Farkettiğiniz gibi componentin içerisinden props olacak bir `isLoggedIn={false}` değerini gönderiyor.

3. `Greeting` componentinde, parametre olarak gönderilen `boolean` (true yada false) değeri bir değişkene atıyor.

4. Ardından bu değer true ise `UserGreeting` componentini, false ise `GuestGreeting` componentini return ediyor.</i>

<h2>Element Değişkenleri</h2>

Elementleri depolamak için değişkenleri kullanabilirsiniz.

Bu, koşullu olarak componentin bir bölümünü oluşturmanıza yardımcı olabilir, ancak çıktının geri kalanı değişmez.

`LoginButton` ve `LogoutButton` düğmelerini temsil eden bu iki yeni componenti inceleyelim:

```js
function LoginButton(props) {
  return (
    <button onClick={props.onClick}>
      Giriş Yap
    </button>
  );
}

function LogoutButton(props) {
  return (
    <button onClick={props.onClick}>
      Çıkış Yap
    </button>
  );
}
```

Aşağıdaki örnekte, `Greeting` adı verilen state'i olan component oluşturacağız.
Geçerli durumuna bağlı olarak `<LoginButton />` veya `<LogoutButton />` işlevlerini oluşturacaktır:

```js
class Greeting extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;

    let button = null;
    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <UserGreeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <Greeting />,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/QKzAgB?editors=0010">CodePen'de Deneyin</a>

Bir değişkeni bildirmek ve  `if` ifadesi kullanmak koşullu olarak bir componenti oluşturmak için iyi bir yoldur,
bazen daha kısa bir syntax kullanmak isteyebilirsiniz.
Aşağıda açıklanan, JSX'de koşulları sıralamanın birkaç yolu vardır.

<h2>&& Operatörü</h2>

Herhangi bir ifadeyi JSX'e süslü parantez içine sararak gömebilirsiniz.
Buna JavaScript mantıksal `&&` operatörü dahildir.
Koşullu olarak bir elementi dahil etmek için kullanışlı olabilir:

```js
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Merhaba!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          {unreadMessages.length} adet okunmamış mesajınız bulunmaktadır.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/ozJddz?editors=0010">CodePen'de Deneyin</a>

<i>JavaScript `true && ifade` olduğunda burada `ifade` kısmında yazacağımız kodu çalıştırır.
Yani `&&`nin sol tarafı true ise, sağ tarafını çalıştırır.

`false && ifade` durumunda ise `false` olarak değerlendirir.

Kısa if-else kullanımda `x = (x == 1) ? ++x` şeklinde kullanım yapamıyoruz.
Mutlaka `else` durumunuda yazmamız gerekiyor. Yani şu şekilde: `x = (x == 1) ? ++x : --x`

Fakat && operatörü ile else durumu olmadan kısa yoldan sadece `if` kontrolü yapmış oluyoruz.
</i>

<h2>If-Else Şartlı Operatörü</h2>

Koşullu olarak oluşturma yöntemi için bir başka yöntem de JavaScript if-else operatörünü kullanmaktır.

`ifade ? dogru : yanlis`

<i>Bu kullanım if { } else { }'in kısa kullanımıdır.
`ifade` olarak belirtilen yer eğer true ise `dogru` yazan yerdeki kod çalışır,
aksi taktirde ise `yanlis` yazan yerdeki kod çalışır.</i>

Aşağıdaki örnekte, if-else koşulunu küçük bir metin bloğu oluşturmak için kullanıyoruz.

```js
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      Kullanıcı siteye giriş <b>{isLoggedIn ? 'yaptı' : 'yapmadı'}</b>.
    </div>
  );
}
```

Bununla birlikte daha büyük ifadeler için de kullanılabilir, ancak kod karmaşıklaşır:

```js
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn ? (
        <LogoutButton onClick={this.handleLogoutClick} />
      ) : (
        <LoginButton onClick={this.handleLoginClick} />
      )}
    </div>
  );
}
```

Tıpkı JavaScript'te olduğu gibi, siz ve ekibiniz hangisinin daha okunabilir olduğunu düşünüyorsa o yöntemi kullanabilir.

<h2>Componentin Render Edilmesini Önlemek</h2>

Nadiren de olsa, bir component, başka bir component tarafından oluşturulmuş olsa bile gizlenmesini isteyebilir.
Bunu yapmak için `null` return etmek gereklidir.

Aşağıdaki örnekte, `<WarningBanner />` componenti, `warn` adlı props değerine bağlı olarak oluşturulmuştur.
Props değeri `false` ise, component oluşturmaz:

```js
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Uyarı!
    </div>
  );
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = {showWarning: true}
    this.handleToggleClick = this.handleToggleClick.bind(this);
  }

  handleToggleClick() {
    this.setState(prevState => ({
      showWarning: !prevState.showWarning
    }));
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? 'Gizle' : 'Göster'}
        </button>
      </div>
    );
  }
}

ReactDOM.render(
  <Page />,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/Xjoqwm?editors=0010">CodePen'de Deneyin</a>

Bir componenti `null` olarak `render` yöntemiyle return etmek, componentin lifecycle fonksiyonlarının başlatılmasını etkilemez.
Örneğin, `componentWillUpdate` ve `componentDidUpdate` yine de çağrılacaktır.

<a href="https://omergulcicek.github.io/reactjs/hizli-baslangic/listeler-ve-keyler">Sıradaki Eğitim: Listeler ve Keyler</a>
