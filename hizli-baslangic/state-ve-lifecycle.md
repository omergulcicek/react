<h1>State ve Lifecycle</h1>

<a href="https://github.com/omergulcicek/reactjs/blob/master/elementleri-render-etmek.md">Önceki konularda</a> gördüğümüz
saat örneğini düşünün.

Şu ana kadar UI'ı güncellemenin tek bir yolunu öğrendik.

Görüntülenen çıktıyı değiştirmek için `ReactDOM.render()` fonksiyonunu her saniye çağırıyorduk:

```js
function tick() {
  const element = (
    <div>
      <h1>Merhaba Dünya!</h1>
      <h2>Saat şu anda {new Date().toLocaleTimeString()}</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

<a href="http://codepen.io/gaearon/pen/gwoJZk?editors=0010">CodePen'de Deneyin</a>

Bu bölümde, `Clock` componentini yeniden kullanımının doğru yöntemini öğreneceğiz.

Zamanlayıcıyı kendisi ayarlayacak ve her saniyede bir güncelleme yapacaktır.

`Clock` componentinin nasıl göründüğünü yazmakla başlayabiliriz:

```js
function Clock(props) {
  return (
    <div>
      <h1>Merhaba Dünya!</h1>
      <h2>Saat şu anda {props.date.toLocaleTimeString()}</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

<a href="http://codepen.io/gaearon/pen/dpdoYR?editors=0010">CodePen'de Deneyin</a>

<i>Daha önce anlatılmıştı fakat tekrar etmekte fayda var.
`Clock` componenti çağrılırken attribute olarak `date={new Date()}` gönderiliyor.
Bu attribute, `Clock` componentine parametre olarak gelir ve adı `props`tur.
`Clock` componentine bu tarihi yazdırmak içinde `props.date` şeklinde kullanıyoruz.</i>

Bunu bir kez yazmak ve `Clock` component güncellemesini kendisi gerçekleştirsin isteriz:

```js
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

Bunu uygulamak için `Clock` componentine `state` eklemeliyiz.
Stateler propslara benzer, ancak tamamen component tarafından kontrol edilir.
Daha önce belirttiğimiz gibi, class olarak tanımlanan componentlerin bazı ilave özellikler var.
State yalnızca classlar için kullanılabilen bir özelliktir.

<h2>Bir Fonksiyonun Class'a Dönüştürülmesi</h2>

<i>Bu kısıma kadar componentleri fonksiyon olarak tanımlamıştık.
Fakat React'ta class olarak oluşturmaya alışmak daha doğru olacaktır.
Şimdi adım adım bir fonksiyonun class'a çevrilme işlemini inceleyelim.</i>

`Clock` fonksiyon componentini aşağıdaki adımlarla class componentine dönüştürebiliriz.

1. `React.Component`ine extend eden aynı ada sahip bir ES6 classı oluşturalım. (<i>`class Clock extends React.Component`</i>)

2. Buna `render()` adı verilen boş bir fonksiyon ekleyin.

3. Fonksiyonun içerisindeki kodları `render()`ın içerisine taşıyın.

4. `props`un adını `this.props` olarak değiştirin.

```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.props.date.toLocaleTimeString()}</h2>
      </div>
    );
  }
}
```

<a href="http://codepen.io/gaearon/pen/zKRGpo?editors=0010">CodePen'de Deneyin</a>

<i>Fonksiyon component yerine class component kullanımına alışın.
Üst kısımdaki adımları anlamadıysanız tekrar tekrar okumanızda fayda var.</i>

`Clock` componenti bir fonksiyon yerine bir class olarak tanımlanmış oldu.

Bu, `state` ve `lifecycle` (yaşam döngüsü) gibi ek özellikleri kullanmamızı sağlar.

<h2>Bir Class'a State Eklemek</h2>

Bir class'a state eklemek için aşağıdaki 3 adımı dikkatlice inceleyiniz.

1. `this.props.date` satırını `this.state.date` olarak güncelleyin:

```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.date.toLocaleTimeString()}</h2>
      </div>
    );
  }
}
```

2. Class componentimizin içerisine state'i ilk anda tanımlayan bir constructor oluşturalım.

<i>Constructor fonksiyonu, bir classla beraber oluşturulan, nesnenin oluşturulması ve başlatılması için özel bir fonskiyondur. Bir classta "constructor" ismiyle yalnızca bir tane özel fonskiyon olabilir. Class oluşturulduğu anda içerisindeki kodlar çalışır.</i>

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.date.toLocaleTimeString()}</h2>
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
    this.state = {date: new Date()};
  }
```

Class componenleri her zaman constructore `props` ile çağırmalıdır.
`<Clock />` componentinden `date` attribute'ünü kaldırın:

```js
ReactDOM.render(
  //eski hali = <Clock date={new Date()} />
  <Clock />,
  document.getElementById('root')
);
```

Zamanlayıcı kodunu daha sonra componentin kendisine geri ekleyeceğiz.

Şu anda sonuç şöyle görünüyor:

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.date.toLocaleTimeString()}</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

<a href="http://codepen.io/gaearon/pen/KgQpJd?editors=0010">CodePen'de Deneyin</a>

Şimdi, `Clock`i kendi zamanlayıcısını oluşturup her saniyede bir güncelleyeceğiz.

<h2>Bir Classa Lifecycle Fonksiyonları Ekleme</h2>

Birçok componente sahip uygulamalarda, componentler yok edildiğinde alınan kaynakları boşaltmak çok önemlidir.

`Clock`, DOM'a ilk defa çağırıldığında bir zamanlayıcı ayarlamak istiyoruz. Buna React'te `mounting` denir.

Ayrıca, Saat componentinden üretilen DOM kaldırıldığında,
bu <a href="https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/clearInterval">zamanlayıcıyı temizlemek</a> istiyoruz.
Buna ise React'te `unmounting` denir.

Bir component DOM'a yazdırılıp kaldırıldığında bazı kod satırlarını çalıştırmak için class componente özel yöntemler ekleyebiliriz:

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
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
        <h2>Saat şu anda {this.state.date.toLocaleTimeString()}</h2>
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
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
```

<i>`() => this.tick()` kullanımı `ES6` ile gelen kısa fonksiyon kullanımıdır.

`ES5`'teki kullanımı `function() { return this.tick();` }</i>

Zamanlayıcı `this`in üzerine nasıl kaydettiğimizi unutmayın.

Zamanlayıcıyı `componentWillUnmount()` fonksiyonunda temizleyeceğiz:


```js
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
```

Son olarak, `Clock` componentini her saniyede bir çalışacağı `tick()` adında bir fonksiyon oluşturacağız.

Bu fonksiyon state'eki tarihi `this.setState()` kullanarak güncelleyecektir.

<i>Daha önceki konularda `props`ların yalnızca okunabilir olduğunu ve güncellenmemesi gerektiğinin notunu düşmüştük.
Bizler (`this.setState()` ile) `state`'i değiştireceğiz, React ise o state'i kullanan yerleri (`props`ları) kendisi güncelleyecek.</i>

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  //Fonksiyon tanımlarken başına "function" yazmadığımıza dikkat edin.
  //React componentleri içerisinde fonksiyon tanımlamak istediğimizde direkt isim vererek yazıyoruz.
  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Merhaba Dünya!</h1>
        <h2>Saat şu anda {this.state.date.toLocaleTimeString()}</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

<a href="http://codepen.io/gaearon/pen/amqdNA?editors=0010">CodePen'de Deneyin</a>

Neler olup bittiğini hızla özetleyelim:

1) `ReactDOM.render()` içerisinde `<Clock />` componenti çağırıldığında, React `Clock` componentinin constructorünü çağırır.
`Clock` componentinin geçerli saati göstermesi gerektiği için `this.state`'i geçerli saat ile başlatır.
Daha sonra bu state güncellenecek.

2) React sonra `Clock` componentinin `render()` fonksiyonunu çağırır.
React, ekranda neyin görüntülenmesi gerektiğini öğrenir.
Daha sonra, `Clock` componentinin çıktısı ile eşleşecek şekilde DOM'u güncelleştirir.

3) `Clock` componentinin çıktısı DOM'a eklendiğinde, React, `componentDidMount()` fonksiyonunu çağırır.
Her saniye çalışacak olan `tick()` fonksiyonunu `timerID`de tutar.

4) Her saniye tarayıcı `tick()` fonksiyonunu çağırır.
`Clock` componentinin içinde, geçerli saati içeren bir nesneyle `setState()`i çağırarak bir UI güncellemesi için`setInterval()` fonksiyonunu hazırlar.
`setState()` çağrısı sayesinde React, statin değiştiğini bilir ve ekranda ne olması gerektiğini öğrenmek için tekrar `render()` eder.
Bu sefer `render()` yöntemindeki `this.state.date` güncellenmiş olacaktır. React DOM'u buna göre günceller.

5) `Clock` componenti DOM'dan kaldırıldıysa, React, `timerID` durduğu anda `componentWillUnmount()` fonksiyonunu çağırır.

<h2>State'i Doğru Kullanmak</h2>

`setState()` hakkında bilmeniz gereken üç şey vardır.

<h5>State'i Doğrudan Değiştirmeyin</h5>

Örneğin, bu bir componenti yeniden oluşturmaz:

```js
// Yanlış Kullanım
this.state.comment = 'Merhaba';
```

`setState()`i şu şekilde kullanın:

```js
// Doğru Kullanım
this.setState({comment: 'Merhaba'});
```

`this.state`i atayabileceğiniz tek yer `constructor`dür.

<h5>State Güncellemeleri Asenkron Olabilir</h5>

React, birden fazla `setState()` çağrısını performans için tek bir güncelleme haline getirebilir.

Çünkü `this.props` ve `this.state` eşzamansız olarak güncellenebilir.

Örneğin, bu sayaç güncellemesi başarısız olabilir:

```js
// Yanlış Kullanım
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

Bunu düzeltmek için, bir objeden ziyade bir fonksiyonu kabul eden ikinci bir `setState()` formunu kullanın.
Bu işlev önceki durumu ilk argüman olarak, güncelleme ikinci argüman olarak uygulandığında sahne alacaktır:

```js
// Doğru Kullanım
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
```

<i>Yukarıdaki örnekte ES6 ile gelen ok fonksiyonu kullandık fakat normal fonksiyonlarla da yapabilirdik:</i>

```js
// Doğru Kullanım
this.setState(function(prevState, props) {
  return {
    counter: prevState.counter + props.increment
  };
});
```

<h5>State'leri Toplu Güncelleştirmek</h5>

`setState()` öğesini çağırdığınızda, React state'i birleştirir. Bu yüzden birden fazla state aynı anda güncellenebilir.


```js
constructor(props) {
  super(props);
  this.state = {
    posts: [],
    comments: []
  };
}
```

Ayrıca bunları ayrı `setState()` çağrılarıyla bağımsız olarakta güncelleyebilirsiniz:

```js
componentDidMount() {
  fetchPosts().then(response => {
    this.setState({
      posts: response.posts
    });
  });

  fetchComments().then(response => {
    this.setState({
      comments: response.comments
    });
  });
}
```

<i>`setState`i kullandığımızda tüm state'ler değiştirilmez. Yalnızca belirtilen state güncellenir.
Yani `this.setState({comments})` şeklinde kullanıldığında sadece `this.state.comments` güncellenir, `this.state.posts` güncellenmez.</i>

<a href="https://omergulcicek.github.io/react/hizli-baslangic/click-ve-change-olaylari">Sıradaki Eğitim: Click ve Change Olayları</a>
