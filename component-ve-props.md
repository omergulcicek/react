<h1>Component ve Props</h1>

Componentler, uygulamanızı tekrar kullanılabilir parçalara ayırmanıza ve her bir parçayı ayrı ayrı düşünmenize izin verir.

Kavramsal olarak, componentler JavaScript fonksiyonlarına benzemektedir.

Bunlar rasgele girdileri (`props` olarak adlandırılır) kabul eder ve
ekranda neler görüneceğini açıklayan React elementleri return ederler.

<i>Sitenizi büyük bir puzzle olarak düşünün.
React ile önce teker teker puzzle parçalarını oluşturup ardından bunları birleştirerek büyük resmi oluşturacaksınız.</i>

<h2>Fonksiyonel ve Class Componentleri</h2>

Bir componenti tanımlamanın en basit yolu, bir JavaScript fonksiyonu yazmaktır:

```js
function Hosgeldin(props) {
  return <h1>Merhaba {props.ad}</h1>;
}
```
Bu fonksiyon geçerli bir React componenti olduğundan, tek bir `props` parametresini obje olarak alır ve
bir React componenti return eder.

Bu componenti "fonksiyonel" olarak adlandırırız çünkü tam anlamıyla JavaScript fonksiyonudur.

Bir componenti tanımlamak için bir ES6 sınıfı da kullanabilirsiniz:
(<i>ES6 hakkında detaylar eklenecektir.</i>)

```js
class Hosgeldin extends React.Component {
  render() {
    return <h1>Merhaba {this.props.ad}</h1>;
  }
}
```

Yukarıdaki iki component, React'in bakış açısından eşittir.

Class'ların sonraki bölümlerde göreceğimiz bazı ek özellikleri var.
O zamana kadar componentleri en saf hallerini kullanacağız.

<i>İlerleyen konularda class'lar içerisine constructor, props, state ve çeşitli fonksiyonlar dahil olacak.
Fakat konuyu dağıtmamak adına class'ları yukarıdaki en saf halleriyle kullanmaya devam edelim.</i>

<h2>Componentleri Render Etmek</h2>

Daha önce yalnızca DOM etiketleri temsil eden React elementleriyle karşılaştık:

```js
const element = <div />;
```

Bununla birlikte, elementler componentleri de temsil edebilir:

```js
const element = <Hosgeldin ad="Ömer" />;
```

React, kullanıcı tanımlı bir componenti temsil eden bir element görürse, JSX attributelerini tek bir obje olarak bu componente aktarır.
Bu objeye `props` diyoruz.

<i>Yani bir componente `<Hosgeldin ad="Ömer" soyad="Gülçiçek" meslek="Yazılım Mühendisi" />` gibi
birden çok attribute eklediğimiz zaman, React bunları aşağıdaki gibi tek bir objede toplar, buna `props` denir.
Ardından bu props objesini `Hosgeldin` componentine parametre olarak gönderir.
`Hosgeldin` componentinde `props.ad` kullanım şekli ile "Ömer" değerini çekebiliriz.

```html
<Hosgeldin ad="Ömer" soyad="Gülçiçek" meslek="Yazılım Mühendisi" />

props = {
ad: "Ömer",
soyad: "Gülçiçek",
meslek: "Yazılım Mühendisi"
}
```
</i>

Örneğin, bu kod sayfaya "Merhaba Ömer" başlığını yazar:

```js
function Hosgeldin(props) {
  return <h1>Merhaba {props.ad}</h1>;
}

const element = <Hosgeldin ad="Ömer" />;
ReactDOM.render(
  element,
  document.getElementById("root")
);
```

CodePen'de Deneyin

Bu örnekteki olayları aşama aşama inceleyelim:

1. `ReactDOM.render()` öğesini `<Hosgeldin ad="Ömer" />` elementiyle çağırırız.

2. React, `Hosgeldin` componentine parametre olarak `{ad: 'Ömer'}` objesini alır.

3. `Hosgeldin` componenti `<h1>Merhaba Ömer</h1>` elementini return eder.

4. React DOM, DOM'u `<h1>Merhaba Ömer</h1>` olacak şekilde günceller.

>**Uyarı:**
>
>Component adlarını daima büyük harfle başlatın.
>
>Örneğin, `<div />` bir DOM etiketini temsil eder ama `<Hosgeldiniz />` bir componenti temsil eder.

<h2>Componentleri Oluşturmak</h2>

Component çıktılarında başka componentlere başvurabilir.
Bu, herhangi bir componenti farklı şekillerde kullanmamızı sağlar.
Bir buton, bir form, bir diyalog, bir ekran: React uygulamalarında, hepsi genel olarak component olarak ifade edilir.

Örneğin, `Hosgeldin`'i birçok kez çağıran bir `Uygulama` componenti oluşturabiliriz:

```js
function Hosgeldin(props) {
  return <h1>Merhaba {props.ad}</h1>;
}

function Uygulama() {
  return (
    <div>
      <Hosgeldin ad="Ömer" />
      <Hosgeldin ad="Muhammed" />
      <Hosgeldin ad="Burak" />
    </div>
  );
}

ReactDOM.render(
  <Uygulama />,
  document.getElementById("root")
);
```

CodePen'de Deneyin

Genelde, React uygulamalarında tek bir `Uygulama` componenti çağrılır.
Bununla birlikte, React'ı varolan bir uygulamaya entegre ederseniz,
`Buton` gibi küçük bir component ile iç componentten dışa doğru kodlamaya başlayabilir ve
görünüm hiyerarşisinin en üst noktasına yavaş yavaş ilerleyebilirsiniz.

Bu örnekteki olaylarıda aşama aşama inceleyelim:

1. `ReactDOM.render()` ilk olarak `<Uygulama />` componentini çağırdı.

2. `<Uygulama />` componenti ise 3 tane `<Hosgeldin />` componenti return edecek.
Fakat `<Hosgeldin />` componentine parametre olarak farklı objeler yollanmış.

3. İlk `<Hosgeldin />` componenti ekrana `Merhaba Ömer` yazacak.
Ardından tekrar `<Hosgeldin />` componenti çağrılacak fakat bu sefer objedeki ad Muhammed, son olarakta Burak olacak.

4. Sonuç olarak ekranda bir `div` içerisinde `Merhaba Ömer`, `Merhaba Muhammed` ve `Merhaba Burak` yazan başlıklar yazdırılacaktır.

<h2>Componentleri Parçalamak</h2>

Componentleri daha küçük componentleri bölmekten korkmayın.

Örneğin, bu `Yorum` bileşenini düşünün:


```js
function Yorum(props) {
  return (
    <div className="Yorum">
      <div className="KullaniciBilgisi">
        <img className="Profil"
          src={props.kullanici.profilURL}
          alt={props.kullanici.ad}
        />
        <div className="KullaniciBilgisi-ad">
          {props.kullanici.ad}
        </div>
      </div>
      <div className="Yorum-yazi">
        {props.yazi}
      </div>
      <div className="Yorum-tarih">
        {tarihFormati(props.tarih)}
      </div>
    </div>
  );
}
```

CodePen'de Deneyin

`kullanici` (obje), `yazi` (string) ve `tarih` (tarih) props olarak kabul eder ve bir yorum divi return eder.

Bu component, iç içe birçok componenti olduğu için değiştirilmesi zor olabilir,
bu yüzden componenti parçalayarak küçük componentler oluşturalım.

İlk olarak `Profil` componentini oluşturalım:

```js
function Profil(props) {
  return (
    <img className="Profil"
      src={props.kullanici.profilURL}
      alt={props.kullanici.ad}
    />
  );
}
```

Ardından `Yorum` componentinin içerisinden, yeni oluşturduğumuz `Profil` componentini çağıralım.

```js
function Yorum(props) {
  return (
    <div className="Yorum">
      <div className="KullaniciBilgisi">
        <Profil kullanici={props.kullanici} />
        <div className="KullaniciBilgisi-ad">
          {props.kullanici.ad}
        </div>
      </div>
      <div className="Yorum-yazi">
        {props.yazi}
      </div>
      <div className="Yorum-tarih">
        {tarihFormati(props.tarih)}
      </div>
    </div>
  );
}
```

Ardından, `KullaniciBilgisi` componentini ayıklayacağız:

```js
function KullaniciBilgisi(props) {
  return (
    <div className="KullaniciBilgisi">
      <Profil user={props.kullanici} />
      <div className="KullaniciBilgisi-ad">
        {props.kullanici.ad}
      </div>
    </div>
  );
}
```

Şimdide `Yorum` componentinin nasıl görüldüğüne bakalım.

```js
function Yorum(props) {
  return (
    <div className="Yorum">
      <KullaniciBilgisi user={props.kullanici} />
      <div className="Yorum-yazi">
        {props.yazi}
      </div>
      <div className="Yorum-tarih">
        {tarihFormati(props.tarih)}
      </div>
    </div>
  );
}
```

CodePen'de Deneyin

Componentleri küçük parçalara bölmek başlangıçta gereksiz bir iş yada zaman kaybı gibi gözükebilir,
ancak daha büyük uygulamalarda tekrar kullanılabilir component paletine sahip olmak önemlidir.

<h2>Propslar Yalnızca Okunabilir</h2>

Bir component (fonksiyon veya class) oluşturduğunuzda, kendi propslarını hiçbir zaman değiştirmemelisiniz.
Bir `topla` fonksiyonu düşünün:

```js
function topla(a, b) {
  return a + b;
}
```

Bu fonksiyonlara `pure` (saf) denir çünkü parametrelerini değiştirmeye çalışmazlar ve
aynı parametreler için aynı sonuca her zaman return edilir.

Buna karşın, bu fonksiyon kendi parametresini değiştirdiği için saf değildir:

```js
function hesapla(hesap, tutar) {
  hesap.toplam -= tutar;
}
```

React oldukça esnektir fakat tek bir katı kuralı vardır:

Tüm React componentleri, propslar ile ilgili olarak saf fonksiyonlar gibi hareket etmelidir.

Elbette uygulama arayüzü dinamiktir ve zaman içinde değişecektir.
Bir sonraki bölümde `state` kavramı tanıtılacaktır.
State, React componentlerine, kullanıcı eylemlerine ve
diğer herhangi bir şeye bu kuralı ihlal etmeden değerlerin değiştirmesine izin verir.

<i>Özet olarak, propsları asla değiştirmeye kalkmıyoruz. Propslar sadece okunabilir. Bir sonraki bölümde state kavramı işlenecektir.
Propslar state'lerden değeri çekecek, değeri değiştirmek istediğimizde state'i değiştireceğiz. Haliyle propsta değişmiş olacak.</i>

<a href="https://github.com/omergulcicek/reactjs/blob/master/state-ve-lifecycle.md">Sıradaki Eğitim: State ve Lifecyle</a>
