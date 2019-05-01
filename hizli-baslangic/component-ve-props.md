<h1>Component ve Props</h1>

Componentler, uygulamanızı tekrar kullanılabilir parçalara ayırmanıza ve her bir parçayı ayrı ayrı düşünmenize izin verir.

Kavramsal olarak, componentler JavaScript fonksiyonlarına benzemektedir.

Bunlar rasgele girdileri (`props` olarak adlandırılır) kabul eder ve ekranda neler görüneceğini açıklayan React elementleri return ederler.

<i>Sitenizi büyük bir puzzle olarak düşünün. React ile önce teker teker puzzle parçalarını oluşturup ardından bunları birleştirerek büyük resmi oluşturacaksınız.</i>

<h2>Fonksiyonel ve Class Componentleri</h2>

Bir componenti tanımlamanın en basit yolu, bir JavaScript fonksiyonu yazmaktır:

```js
function Welcome(props) {
  return <h1>Merhaba {props.name}</h1>;
}
```
Bu fonksiyon geçerli bir React componenti olduğundan, tek bir `props` parametresini obje olarak alır ve bir React componenti return eder.

Bu componenti "fonksiyonel" olarak adlandırırız çünkü tam anlamıyla JavaScript fonksiyonudur.

Bir componenti tanımlamak için bir ES6 sınıfı da kullanabilirsiniz:
(<i>ES6 hakkında detaylar eklenecektir.</i>)

```js
class Welcome extends React.Component {
  render() {
    return <h1>Merhaba {this.props.name}</h1>;
  }
}
```

Yukarıdaki iki component, React'in bakış açısından eşittir.

Class'ların sonraki bölümlerde göreceğimiz bazı ek özellikleri var.
O zamana kadar componentleri en saf hallerini kullanacağız.

<i>İlerleyen konularda class'lar içerisine constructor, props, state ve çeşitli fonksiyonlar dahil olacak.
Fakat konuyu dağıtmamak adına class'ları yukarıdaki en saf halleriyle kullanmaya devam edelim.</i>

<h2>Componentleri Render Etmek</h2>

Daha önce yalnızca DOM etiketlerini temsil eden React elementleriyle karşılaştık:

```js
const element = <div />;
```

Bununla birlikte, elementler componentleri de temsil edebilir:

```js
const element = <Welcome name="Ömer" />;
```

React, kullanıcı tanımlı bir componenti temsil eden bir element görürse, JSX attributelerini tek bir obje olarak bu componente aktarır. Bu objeye `props` diyoruz.

<i>Yani bir componente `<Welcome name="Ömer" surname="Gülçiçek" job="Yazılım Mühendisi" />` gibi
birden çok attribute eklediğimiz zaman, React bunları aşağıdaki gibi tek bir objede toplar, buna `props` denir.
Ardından bu props objesini `Welcome` componentine parametre olarak gönderir.
`Hosgeldin` componentinde `props.name` kullanım şekli ile "Ömer" değerini çekebiliriz.</i>

```html
<Welcome name="Ömer" surname="Gülçiçek" job="Yazılım Mühendisi" />

props = {
   name: "Ömer",
   surname: "Gülçiçek",
   job: "Yazılım Mühendisi"
}
```

Örneğin, bu kod sayfaya "Merhaba Ömer" başlığını yazar:

```js
function Welcome(props) {
  return <h1>Merhaba {props.name}</h1>;
}

const element = <Welcome name="Ömer" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

<a href="https://reactjs.org/redirect-to-codepen/components-and-props/rendering-a-component">CodePen'de Deneyin</a>

Bu örnekteki olayları aşama aşama inceleyelim:

1. `ReactDOM.render()` fonksiyonundan `<Welcome name='Ömer' />` elementini çağırırız.

2. React, `Welcome` componentine parametre olarak `{name: 'Ömer'}` objesini alır.

3. `Welcome` componenti `<h1>Merhaba Ömer</h1>` elementini return eder.

4. React DOM, DOM'u `<h1>Merhaba Ömer</h1>` olacak şekilde günceller.

>**Uyarı:**
>
>Component adlarını daima büyük harfle başlatın.
>
>Örneğin, `<div />` bir DOM etiketini temsil eder ama `<Welcome />` bir componenti temsil eder.

<h2>Componentleri Oluşturmak</h2>

Component çıktılarında başka componentlere başvurabilir.
Bu, herhangi bir componenti farklı şekillerde kullanmamızı sağlar.
Bir buton, bir form, bir diyalog, bir ekran: React uygulamalarında, hepsi genel olarak component olarak ifade edilir.

Örneğin, `Welcome`'i birçok kez çağıran bir `App` componenti oluşturabiliriz:

```js
function Welcome(props) {
  return <h1>Merhaba {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Ömer" />
      <Welcome name="Muhammed" />
      <Welcome name="Burak" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

<a href="https://reactjs.org/redirect-to-codepen/components-and-props/composing-components">CodePen'de Deneyin</a>

Genelde, React uygulamalarında tek bir `App` componenti çağrılır.
Bununla birlikte, React'ı varolan bir uygulamaya entegre ederseniz,
`Buton` gibi küçük bir component ile iç componentten dışa doğru kodlamaya başlayabilir ve görünüm hiyerarşisinin en üst noktasına yavaş yavaş ilerleyebilirsiniz.

Bu örnekteki olaylarıda aşama aşama inceleyelim:

1. `ReactDOM.render()` ilk olarak `<App />` componentini çağırdı.

2. `<App />` componenti ise 3 tane `<Welcome />` componenti return edecek. Fakat `<Welcome />` componentine parametre olarak farklı objeler yollanmış.

3. İlk `<Welcome />` componenti ekrana `Merhaba Ömer` yazacak. Ardından tekrar `<Welcome />` componenti çağrılacak fakat bu sefer objedeki ad Muhammed, son olarakta Burak olacak.

4. Sonuç olarak ekranda bir `div` içerisinde `Merhaba Ömer`, `Merhaba Muhammed` ve `Merhaba Burak` yazan başlıklar yazdırılacaktır.

<h2>Componentleri Parçalamak</h2>

Componentleri daha küçük componentleri bölmekten korkmayın.

Örneğin, bu `Yorum` componentini düşünün:

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

<a href="https://reactjs.org/redirect-to-codepen/components-and-props/extracting-components">CodePen'de Deneyin</a>

`author` (obje), `text` (string) ve `date` (date) props olarak kabul eder ve bir yorum divi return eder.

Bu component, iç içe birçok componenti olduğu için değiştirilmesi zor olabilir, bu yüzden componenti parçalayarak küçük componentler oluşturalım.

İlk olarak `Avatar` componentini oluşturalım:

```js
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```

Ardından `Comment` componentinin içerisinden, yeni oluşturduğumuz `Avatar` componentini çağıralım.

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

Ardından, `UserInfo` componentini ayıklayacağız:

```js
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}
```

Şimdide `Comment` componentinin nasıl görüldüğüne bakalım.

```js
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

<a href="https://reactjs.org/redirect-to-codepen/components-and-props/extracting-components-continued">CodePen'de Deneyin</a>

Componentleri küçük parçalara bölmek başlangıçta gereksiz bir iş ya da zaman kaybı gibi gözükebilir, ancak daha büyük uygulamalarda tekrar kullanılabilir component paletine sahip olmak önemlidir.

<h2>Propslar Yalnızca Okunabilir</h2>

Bir component (fonksiyon veya class) oluşturduğunuzda, kendi propslarını hiçbir zaman değiştirmemelisiniz.
Bir `sum` fonksiyonu düşünün:

```js
function sum(a, b) {
  return a + b;
}
```

Bu fonksiyonlara `pure` (saf) denir çünkü parametrelerini değiştirmeye çalışmazlar ve aynı parametreler için aynı sonuca her zaman return edilir.

Buna karşın, bu fonksiyon kendi parametresini değiştirdiği için saf değildir:

```js
function withdraw(account, amount) {
  account.total -= amount;
}
```

React oldukça esnektir fakat tek bir katı kuralı vardır:

Tüm React componentleri, propslar ile ilgili olarak saf fonksiyonlar gibi hareket etmelidir.

Elbette uygulama arayüzü dinamiktir ve zaman içinde değişecektir.
Bir sonraki bölümde `state` kavramı tanıtılacaktır.
State, React componentlerine, kullanıcı eylemlerine ve diğer herhangi bir şeye bu kuralı ihlal etmeden değerlerin değiştirmesine izin verir.

<i>Özet olarak, propsları asla değiştirmeye kalkmıyoruz. Propslar sadece okunabilir. Bir sonraki bölümde state kavramı işlenecektir.
Propslar state'lerden değeri çekecek, değeri değiştirmek istediğimizde state'i değiştireceğiz. Haliyle propsta değişmiş olacak.</i>

<a href="https://omergulcicek.github.io/react/hizli-baslangic/state-ve-lifecycle">Sıradaki Eğitim: State ve Lifecyle</a>
