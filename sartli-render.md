<h1>Şartlı Render</h1>

React ile ihtiyacınız olan davranışı kapsayan farklı componentler oluşturabilirsiniz.
Daha sonra, uygulamanızın state'ine bağlı olarak yalnızca bir kısmını görüntüleyebilirsiniz.

React'te şartlı render, JavaScript koşulları  ile aynı şekilde çalışır.
Geçerli durumu temsil eden elemanlar oluşturmak için `if` veya koşullu operatör gibi JavaScript operatörlerini kullanın
ve bunları eşleştirmek için  UI'ı güncelleştirmeye izin verin.

Bu iki componenti düşünün:

```js
function KullaniciGirisi(props) {
  return <h1>Tekrardan hoşgeldin!</h1>;
}

function MisafirGirisi(props) {
  return <h1>Lütfen üye ol.</h1>;
}
```

Bir kullanıcının oturum açıp açmadığına bağlı olarak bu componentlerin herhangi birini görüntüleyen bir
`GirisKontrol` componenti oluşturacağız:

```javascript
function GirisKontrol(props) {
  const girisYaptiMi = props.girisYaptiMi;
  if (girisYaptiMi) {
    return <KullaniciGirisi />;
  }
  return <MisafirGirisi />;
}

ReactDOM.render(
  // girisYaptiMi={true} olarak değiştirip farkı test edebilirsiniz.
  <GirisKontrol girisYaptiMi={false} />,
  document.getElementById("root")
);
```

CodePen'de Deneyin

<i>Adım adım incelemekte fayda var.

1. İlk olarak ReactDOM, `GirisKontrol` componentini render ediyor.

2. Farkettiğiniz gibi componentin içerisinden props olacak bir `girisYaptiMi={false}` değerini yolluyor.

3. `GirisKontrol` componentinde, parametre olarak gönderilen `boolean` (true yada false) değeri bir değişkene atıyor.

4. Ardından bu değer true ise `KullaniciGirisi` componentini, false ise `MisafirGirisi` componentini return ediyor.</i>


<h2>Element Değişkenleri</h2>

Elementleri depolamak için değişkenleri kullanabilirsiniz.

Bu, koşullu olarak componentin bir bölümünü oluşturmanıza yardımcı olabilir, ancak çıktının geri kalanı değişmez.

`GirisButon` ve `CikisButon` düğmelerini temsil eden bu iki yeni componenti inceleyelim:


```js
function GirisButon(props) {
  return (
    <button onClick={props.onClick}>
      Giriş Yap
    </button>
  );
}

function CikisButon(props) {
  return (
    <button onClick={props.onClick}>
      Logout
    </button>
  );
}
```

Aşağıdaki örnekte, `GirisKontrol` adı verilen state'i olan component oluşturacağız.
Geçerli durumuna bağlı olarak `<GirisButon />` veya `<CikisButon />` işlevlerini oluşturacaktır:

```js
class GirisKontrol extends React.Component {
  constructor(props) {
    super(props);
    this.girisButonClick = this.girisButonClick.bind(this);
    this.cikisButonClick = this.cikisButonClick.bind(this);
    this.state = {girisYaptiMi: false};
  }

  girisButonClick() {
    this.setState({girisYaptiMi: true});
  }

  cikisButonClick() {
    this.setState({girisYaptiMi: false});
  }

  render() {
    const girisYaptiMi = this.state.girisYaptiMi;

    let button = null;
    if (girisYaptiMi) {
      button = <CikisButon onClick={this.cikisButonClick} />;
    } else {
      button = <GirisButon onClick={this.girisButonClick} />;
    }

    return (
      <div>
        <KullaniciGirisi girisYaptiMi={girisYaptiMi} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <GirisKontrol />,
  document.getElementById("root")
);
```

CodePen'de Deneyin

Bir değişkeni bildirmek ve  `if` ifadesi kullanmak koşullu olarak bir componenti oluşturmak için iyi bir yoldur,
bazen daha kısa bir syntax kullanmak isteyebilirsiniz.
Aşağıda açıklanan, JSX'de koşulları sıralamanın birkaç yolu vardır.

<h2>&& Operatörü</h2>

Herhangi bir ifadeyi JSX'e süslü parantez içine sararak gömebilirsiniz.
Buna JavaScript mantıksal `&&` operatörü dahildir.
Koşullu olarak bir elementi dahil etmek için kullanışlı olabilir:

```js
function PostaKutusu(props) {
  const okunmamisMesajlar = props.okunmamisMesajlar;
  return (
    <div>
      <h1>Merhaba!</h1>
      {okunmamisMesajlar.length > 0 &&
        <h2>
          {okunmamisMesajlar.length} adet okunmamış mesajınız bulunmaktadır.
        </h2>
      }
    </div>
  );
}

const mesajlar = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <PostaKutusu okunmamisMesajlar={mesajlar} />,
  document.getElementById("root")
);
```

CodePen'de Deneyin

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

```javascript
render() {
  const girisYaptiMi = this.state.girisYaptiMi;
  return (
    <div>
      Kullanıcı siteye giriş <b>{girisYaptiMi ? 'yaptı' : 'yapmadı'}</b>.
    </div>
  );
}
```

Bununla birlikte, daha büyük ifadeler için de kullanılabilir, ancak kod karmaşıklaşır:

```js
render() {
  const girisYaptiMi = this.state.girisYaptiMi;
  return (
    <div>
      {girisYaptiMi ? (
        <CikisButon onClick={this.cikisButonClick} />
      ) : (
        <GirisButon onClick={this.girisButonClick} />
      )}
    </div>
  );
}
```

Tıpkı JavaScript'te olduğu gibi, siz ve ekibiniz hangisinin daha okunabilir olduğunu düşünüyorsa, o yöntemi kullanabilir.

<h2>Componentin Render Edilmesini Önlemek</h2>

Nadiren de olsa, bir component, başka bir component tarafından oluşturulmuş olsa bile gizlenmesini isteyebilir.
Bunu yapmak için `null` return etmek gereklidir.

Aşağıdaki örnekte, `<UyariAfisi />` componenti, `uyari` adlı props değerine bağlı olarak oluşturulmuştur.
Props değeri `false` ise, component oluşturmaz:

```js
function UyariAfisi(props) {
  if (!props.uyari) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = {uyariGoster: true}
    this.uyariDurumunuDegistir = this.uyariDurumunuDegistir.bind(this);
  }

  uyariDurumunuDegistir() {
    this.setState(prevState => ({
      uyariGoster: !prevState.uyariGoster
    }));
  }

  render() {
    return (
      <div>
        <UyariAfisi uyari={this.state.uyariGoster} />
        <button onClick={this.uyariDurumunuDegistir}>
          {this.state.uyariGoster ? 'Gizle' : 'Göster'}
        </button>
      </div>
    );
  }
}

ReactDOM.render(
  <Page />,
  document.getElementById("root")
);
```

CodePen'de Deneyin

Bir componenti `null` olarak `render` yöntemiyle return etmek, componentin lifecycle fonksiyonlarının başlatılmasını etkilemez.
Örneğin, `componentWillUpdate` ve `componentDidUpdate` yine de çağrılacaktır.

<a href="https://omergulcicek.github.io/reactjs/listeler-ve-keyler">Sıradaki Eğitim: Listeler ve Keyler</a>
