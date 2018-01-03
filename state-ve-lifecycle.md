<h1>State ve Lifecycle</h1>

<a href="https://github.com/omergulcicek/reactjs/blob/master/elementleri-render-etmek.md">Önceki konularda</a> gördüğümüz
saat örneğini düşünün.

Şu ana kadar UI'ı güncellemenin tek bir yolunu öğrendik.

Görüntülenen çıktıyı değiştirmek için `ReactDOM.render()` öğesini her saniye çağırıyorduk:

```js
function tiktak() {
  const element = (
    <div>
      <h1>Merhaba Dünya!</h1>
      <h2>Saat şu anda {new Date().toLocaleTimeString()}</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById("root")
  );
}

setInterval(tiktak, 1000);
```

CodePen'de Deneyin

Bu bölümde, `Saat` componentini yeniden kullanımının doğru yöntemini öğreneceğiz.

Zamanlayıcıyı kendisi ayarlayacak ve her saniyede bir güncelleme yapacaktır.

`Saat` componentinin nasıl göründüğünü yazmakla başlayabiliriz:

```js
function Saat(props) {
  return (
    <div>
      <h1>Merhaba Dünya!</h1>
      <h2>Saat şu anda {props.tarih.toLocaleTimeString()}</h2>
    </div>
  );
}

function tiktak() {
  ReactDOM.render(
    <Saat tarih={new Date()} />,
    document.getElementById("root")
  );
}

setInterval(tiktak, 1000);
```

CodePen'de Deneyin

<i>Daha önce anlatılmıştı fakat tekrar etmekte fayda var.
`Saat` componenti çağrılırken attribute olarak `tarih={new Date()}` gönderiliyor.
Bu attribute, `Saat` componentine parametre olarak gelir ve adı `props`tur.
`Saat` componentine bu tarihi yazdırmak içinde `props.tarih` şeklinde kullanıyoruz.
</i>

Bunu bir kez yazmak ve `Saat` component güncellemesini kendisi gerçekleştirsin isteriz:

```js
ReactDOM.render(
  <Saat />,
  document.getElementById("root")
);
```

Bunu uygulamak için `Saat` componentine `state` eklemeliyiz.
Stateler proplara benzer, ancak tamamen component tarafından kontrol edilir.
Daha önce belirttiğimiz gibi, class olarak tanımlanan componentlerin bazı ilave özellikler var.
State yalnızca classlar için kullanılabilen bir özelliktir.

<h2>Bir Fonksiyonun Class'a Dönüştürülmesi</h2>

<i>Bu kısıma kadar componentleri fonksiyon olarak tanımlamıştık.
Fakat React'ta class olarak oluşturmaya alışmak daha doğru olacaktır.
Şimdi adım adım bir fonksiyonun class'a çevrilme işlemini inceleyelim.</i>

`Saat` fonksiyon componentini aşağıdaki adımlarla class componentine dönüştürebiliriz.

1. `React.Component`ine extend eden aynı ada sahip bir ES6 classı oluşturalım. (<i>`class Saat extends React.Component`</i>)

2. Buna `render()` adı verilen boş bir fonksiyon ekleyin.

3. Fonksiyonun içerisindeki kodları `render()`ın içerisine taşıyın.

4. `props`un adını `this.props` olarak değiştirin.

```js
class Saat extends React.Component {
  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.props.tarih.toLocaleTimeString()}/h2>
      </div>
    );
  }
}
```

CodePen'de Deneyin

<i>Fonksiyon component yerine class component kullanımına alışın.
Üst kısımdaki adımları anlamadıysanız tekrar tekrar okumanızda fayda var.</i>

`Saat` componenti bir fonksiyon yerine bir class olarak tanımlanmış oldu.

Bu, `state` ve `lifecycle` (yaşam döngüsü) gibi ek özellikleri kullanmamızı sağlar.

<h2>Bir Class'a State Eklemek</h2>

Bir class'a state eklemek için aşağıdaki 3 adımı dikkatlice inceleyiniz.

1. `this.props.tarih` satırını `this.state.tarih` olarak güncelleyin:

```js
class Saat extends React.Component {
  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.tarih.toLocaleTimeString()}</h2>
      </div>
    );
  }
}
```

2. Class componentimizin içerisine state'i ilk anda tanımlayan bir constructor oluşturalım.

<i>Constructor fonksiyonu, bir classla beraber oluşturulan, nesnenin oluşturulması ve başlatılması için özel bir fonskiyondur.
Bir classta "constructor" ismiyle yalnızca bir tane özel fonskiyon olabilir.
Class oluşturulduğu anda içerisindeki kodlar çalışır.</i>

```js
class Saat extends React.Component {
  constructor(props) {
    super(props);
    this.state = {tarih: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.tarih.toLocaleTimeString()}</h2>
      </div>
    );
  }
}
```

`props`un constructorden nasıl alındığına dikkat ediniz:

<i>`constructor`e parametre olarak `props` ekleyip, içerisine `super(props);` satırını ekliyoruz.</i>

```js
  constructor(props) {
    super(props);
    this.state = {tarih: new Date()};
  }
```

Class componenleri her zaman constructore `props` ile çağırmalıdır.
`<Saat/>` componentinden `tarih` attribute'ünü kaldırın:

```js
ReactDOM.render(
  //eski hali = <Saat tarih={new Date()} />
  <Saat />,
  document.getElementById("root")
);
```

Zamanlayıcı kodunu daha sonra componentin kendisine geri ekleyeceğiz.

Şu anda sonuç şöyle görünüyor:

```js
class Saat extends React.Component {
  constructor(props) {
    super(props);
    this.state = {tarih: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.tarih.toLocaleTimeString()}</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Saat />,
  document.getElementById("root")
);
```

CodePen'de Deneyin

Şimdi, `Saat`i kendi zamanlayıcısını oluşturup her saniyede bir güncelleyeceğiz.

<h2>Bir Classa Lifecycle Fonksiyonları Ekleme</h2>

Birçok componente sahip uygulamalarda, componentler yok edildiğinde alınan kaynakları boşaltmak çok önemlidir.

`Saat`, DOM'a ilk defa çağırıldığında bir zamanlayıcı ayarlamak istiyoruz. Buna React'te `mounting` denir.

Ayrıca, Saat componentinden üretilen DOM kaldırıldığında,
bu <a href="https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/clearInterval">zamanlayıcıyı temizlemek</a> istiyoruz.
Buna ise React'te `unmounting` denir.

Bir component DOM'a yazdırılıp kaldırıldığında bazı kod satırlarını çalıştırmak için class componente özel yöntemler ekleyebiliriz:

```js
class Saat extends React.Component {
  constructor(props) {
    super(props);
    this.state = {tarih: new Date()};
  }

  componentDidMount() {
    //Component oluşturulduğunda çalışacak fonksiyon
  }

  componentWillUnmount() {
    //Component kaldırıldığında çalışacak fonksiyon
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.tarih.toLocaleTimeString()}</h2>
      </div>
    );
  }
}
```
Bu fonksiyonlara `lifecycle hooks` (yaşam döngüsü kancaları) adı verilir.

Component çıktısı DOM'a aktarıldıktan sonra `componentDidMount()` fonksiyonu çalışır.
Bu, zamanlayıcı ayarlamak için iyi bir yerdir:

```js
  componentDidMount() {
    this.zamanlayici = setInterval(
      () => this.tiktak(),
      1000
    );
  }
```

<i>`() => this.tiktak()` kullanımı `ES6` ile gelen kısa fonksiyon kullanımıdır.
Bu kullanımlara daha hakim olmak için ilerleyen zamanda gerekli linkler eklenecektir.
`ES5`'teki kullanımı `function() { return this.tiktak();` }</i>

Zamanlayıcı `this`in üzerine nasıl kaydettiğimizi unutmayın.

Zamanlayıcıyı `componentWillUnmount()` fonksiyonunda temizleyeceğiz:


```js
  componentWillUnmount() {
    clearInterval(this.zamanlayici);
  }
```

Son olarak, `Saat` componentini her saniyede bir çalışacağı tiktak() adında bir fonksiyon oluşturacağız.

Bu fonksiyon state'eki tarihi `this.setState()` kullanarak güncelleyecektir.

<i>Daha önceki konularda `props`ların yalnızca okunabilir olduğunu ve güncellenmemesi gerektiğinin notunu düşmüştük.
Bizler (`this.setState()` ile) `state`'i değiştireceğiz, React ise o state'i kullanan yerleri (`props`ları) kendisi güncelleyecek.</i>

```js
class Saat extends React.Component {
  constructor(props) {
    super(props);
    this.state = {tarih: new Date()};
  }

  componentDidMount() {
    this.zamanlayici = setInterval(
      () => this.tiktak(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.zamanlayici);
  }
  
  //Fonksiyon tanımlarken başına "function" yazmadığımıza dikkat edin.
  //React componentleri içerisinde fonksiyon tanımlamak istediğimizde direkt isim vererek yazıyoruz.
  tiktak() {
    this.setState({
      tarih: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.tarih.toLocaleTimeString()}</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Saat />,
  document.getElementById("root")
);
```

CodePen'de Deneyin

Neler olup bittiğini hızla özetleyelim:

1) `ReactDOM.render()` içerisinde `<Saat />` componenti çağırıldığında, React `Saat` componentinin constructorünü çağırır.
`Saat` componentinin geçerli saati göstermesi gerektiği için `this.state`'i geçerli saat ile başlatır.
Daha sonra bu state güncellenecek.

2) React sonra `Saat` componentinin `render()` fonksiyonunu çağırır.
React, ekranda neyin görüntülenmesi gerektiğini öğrenir.
Daha sonra, `Saat` componentinin çıktısı ile eşleşecek şekilde DOM'u güncelleştirir.

3) `Saat` componentinin çıktısı DOM'a eklendiğinde, React, `componentDidMount()` fonksiyonunu çağırır.
Her saniye çalışacak olan `tiktak()` fonksiyonunu `zamanlayici`da tutar.

4) Her saniye tarayıcı `tiktak()` fonksiyonunu çağırır.
`Saat` componentinin içinde, geçerli saati içeren bir nesneyle `setState()`i çağırarak
bir UI güncellemesi için`setInterval()` fonksiyonunu hazırlar.
`setState()` çağrısı sayesinde React, statin değiştiğini bilir ve ekranda ne olması gerektiğini öğrenmek için tekrar `render()` eder.
Bu sefer `render()` yöntemindeki `this.state.tarih` güncellenmiş olacaktır. React DOM'u buna göre günceller.

5) `Saat` componenti DOM'dan kaldırıldıysa, React, `zamanlayici` durduğu anda `componentWillUnmount()` fonksiyonunu çağırır.

<h2>State'i Doğru Kullanmak</h2>

`setState()` hakkında bilmeniz gereken üç şey vardır.

<h5>State'i Doğrudan Değiştirmeyin</h5>

Örneğin, bu bir componenti yeniden oluşturmaz:

```js
// Yanlış Kullanım
this.state.yorum = 'Merhaba';
```

`setState()`i şu şekilde kullanın:

```js
// Doğru Kullanım
this.setState({yorum: 'Merhaba'});
```

`this.state`i atayabileceğiniz tek yer `constructor`dür.

<h5>State Güncellemeleri Asenkron Olabilir</h5>

React, birden fazla `setState()` çağrısını performans için tek bir güncelleme haline getirebilir.

Çünkü `this.props` ve `this.state` eşzamansız olarak güncellenebilir.

Örneğin, bu sayaç güncellemesi başarısız olabilir:

```js
// Yanlış Kullanım
this.setState({
  counter: this.state.sayac + this.props.artis,
});
```
Bunu düzeltmek için, bir objeden ziyade bir fonksiyonu kabul eden ikinci bir `setState()` formunu kullanın.
Bu işlev önceki durumu ilk argüman olarak, güncelleme ikinci argüman olarak uygulandığında sahne alacaktır:

```js
// Doğru Kullanım
this.setState((prevState, props) => ({
  counter: prevState.sayac + props.artis
}));
```

<i>Yukarıdaki örnekte ES6 ile gelen ok fonksiyonu kullandık fakat normal fonksiyonlarla da yapabilirdik:</i>

```js
// Doğru Kullanım
this.setState(function(prevState, props) {
  return {
    counter: prevState.sayac + props.artis
  };
});
```

<h5>State'leri Toplu Güncelleştirmek</h5>

`setState()` öğesini çağırdığınızda, React state'i birleştirir. Bu yüzden birden fazla state aynı anda güncellenebilir.


```js
  constructor(props) {
    super(props);
    this.state = {
      mesajlar: [],
      yorumlar: []
    };
  }
```

Ayrıca bunları ayrı `setState()` çağrılarıyla bağımsız olarakta güncelleyebilirsiniz:

```js
  componentDidMount() {
    fetchPosts().then(yanit => {
      this.setState({
        posts: yanit.mesajlar
      });
    });

    fetchComments().then(yanit => {
      this.setState({
        comments: yanit.yorumlar
      });
    });
  }
```

<i>`setState`i kullandığımızda tüm state'ler değiştirilmez. Yalnızca belirtilen state güncellenir.
Yani `this.setState({yorumlar})` şeklinde kullanıldığında sadece `this.state.yorumlar` güncellenir, `this.state.mesajlar` güncellenmez.</i>

<a href="https://omergulcicek.github.io/reactjs/click-ve-change-olaylari">Sıradaki Eğitim: Click ve Change Olayları</a>
