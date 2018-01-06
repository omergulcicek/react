<h1>Listeler ve Keyler</h1>

Önce, JavaScript'te listeleri nasıl dönüştürdüğümüzü gözden geçirelim.
Aşağıdaki kod göz önüne alındığında, bir dizi sayı almak ve değerlerini ikiye katlamak için `map()` fonksiyonunu kullanıyoruz.
`map()` tarafından return edilen çift katlı değerleri kaydederiz:

```javascript
const sayilar = [1, 2, 3, 4, 5];
const ciftKati = sayilar.map((sayi) => sayi * 2);
console.log(ciftKati);
```

Konsola `[2, 4, 6, 8, 10]` yazacaktır.

<i>Google Chrome'da (diğer tarayıcılarda da benzer yada aynıdır) <b>F12</b>'ye basıp, 
"Console (yada Konsol)" sekmesine gelip bu kodları yapıştırarak test edebilirsiniz.

Ok fonksiyonları ile ilgili dokümantasyon hazırlandığında bu kısım güncellenecektir.
Kısaca özet geçmek gerekirse yukarıda map fonksiyonunun içerisinde yapılan işlem (`(sayi) => sayi * 2`) şudur:

`sayi` parametre alınır ve `sayi*2` return edilir.

Fonksiyonun kolay okunabilir hali ise şudur:
</i>

```javascript
function(sayi) {
  return sayi*2;
}
```

React'te, dizi elemanlarını listelere dönüştürmek neredeyse aynıdır.

<h2>Birden Çok Component Vermek</h2> 

Koleksiyonları oluşturabilir ve bunları JSX içine süslü parantez `{}` kullanarak ekleyebilirsiniz.

Aşağıda, JavaScript `map()` fonksiyonu kullanarak sayilar dizisinde döngü oluşturuyoruz.
Her liste için bir `<li>` return ediyoruz. Son olarak, elde edilen sonuç dizisini `itemler`e atayacağız:

```javascript
const sayilar = [1, 2, 3, 4, 5];
const itemler = sayilar.map((sayi) =>
  <li>{sayi}</li>
);
```

Bütün `itemler` dizesini `<ul>` elemanının içerisine dahil ediyoruz ve bunu DOM'a gönderiyoruz:

```javascript
ReactDOM.render(
  <ul>{itemler}</ul>,
  document.getElementById("root")
);
```

<a href="https://codepen.io/gaearon/pen/GjPyQr?editors=0011">CodePen'de Deneyin</a>

Bu kod, ekrana `ul` kapsayıcısı ve `li`ler içerisinde rakamları yazacaktır.

<h2>Temel Liste Componenti</h2>

Genellikle listeleri bir component içinde render ederiz.

Önceki örneği, `sayilar` adında bir dizi kabul eden ve liste çıktısı yapan bir componente dönüştürebiliriz.

```javascript
function NumaraListesi(props) {
  const sayilar = props.sayilar;
  const itemler = sayilar.map((sayi) =>
    <li>{sayi}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumaraListesi sayilar={sayilar} />,
  document.getElementById("root")
);
```

Bu kodu çalıştırdığınızda, liste için bir `key` (anahtar) verilmesi yönünde bir uyarı verilir.

<i>Burada key kelimesine (Türkçe'si anahtar demek olmasına rağmen) anahtar çevirisi tam olarak uymuyor.
Key denirken aslında benzersizi ifade etmektedir (ID, Kimlik numarası, parmak izi gibi)</i>.

Bir `key`, listeleri oluşturulurken eklenmesi gereken özel bir attribute'tür.
Bir sonraki bölümde bunun neden önemli olduğunu anlatacağız.
`sayilar.map()` içindeki listelere birer `key` atayalım.

```javascript
function NumaraListesi(props) {
  const sayilar = props.sayilar;
  const itemler = sayilar.map((sayi) =>
    <li key={sayi.toString()}>
      {sayi}
    </li>
  );
  return (
    <ul>{itemler}</ul>
  );
}

const sayilar = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumaraListesi sayilar={sayilar} />,
  document.getElementById("root")
);
```

<a href="https://codepen.io/gaearon/pen/jrXYRR?editors=0011">CodePen'de Deneyin</a>

<h2>Keyler</h2>

`Key`ler yardımı ile hangi listenin değiştiğini, eklendiğini veya kaldırıldığını belirleyebiliriz.
Elemanlara istikrarlı bir kimlik kazandırmak için dizideki listelere `key` verilmelidir:

```js
const sayilar = [1, 2, 3, 4, 5];
const itemler = sayilar.map((sayi) =>
  <li key={sayi.toString()}>
    {sayi}
  </li>
);
```

Bir `key` seçmenin en iyi yolu, kardeşleri (<i>diğer `li`ler</i>) arasında bir tanımlanan bir kimlik kullanmaktır.
Çoğu zaman, verilerinizdeki id'ler `key` olarak kullanılır:

```js
const yapilacaklar = yapilacaklar.map((yapilacak) =>
  <li key={yapilacak.id}>
    {yapilacak.yazi}
  </li>
);
```

Eğer bu tarzda bir yapınız yoksa benzersiz olacağı için `key`lere `index` verebiliriz:

```js
const yapilacaklar = yapilacaklar.map((yapilacak, index) =>
  // Listelerin benzersiz id'leri yoksa bu yöntemi kullanın.
  <li key={index}>
    {yapilacak.yazi}
  </li>
);
```

Listelerin sırası değişebilirse keyler için index kullanmanızı önermiyoruz.
Bu, performansı olumsuz etkileyebilir ve component state'i ile ilgili sorunlara neden olabilir.

Ayrıntılı bilgi için <a href="https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318">Robin Pokorny</a>'nin
makalesini inceleyebilirsiniz (<i>İngilizce</i>).

Listelere siz key atamazsanız React varsayılan olarak index'i atar.

<h2>Keyler Yalnızca Kardeşleri Arasında Benzersiz Olmalıdır</h2>

Dizilerde kullanılan keyler kardeşleri arasında benzersiz olmalıdır.
Bununla birlikte, global olarak benzersiz olması gerekmez.

İki farklı diziyi üretirken aynı keyleri kullanabiliriz:

```js
function Blog(props) {
  const yanMenu = (
    <ul>
      {props.mesajlar.map((mesaj) =>
        <li key={mesaj.id}>
          {mesaj.baslik}
        </li>
      )}
    </ul>
  );
  const icerik = props.mesajlar.map((mesaj) =>
    <div key={mesaj.id}>
      <h3>{mesaj.baslik}</h3>
      <p>{mesaj.icerik}</p>
    </div>
  );
  return (
    <div>
      {yanMenu}
      <hr />
      {icerik}
    </div>
  );
}

const mesajlar = [
  {id: 1, baslik: 'Merhaba Dünya', icerik: 'React Öğreniyoruz!'},
  {id: 2, baslik: 'Ömer Gülçiçek', icerik: 'React JS Türkçe Dokümantasyon'}
];
ReactDOM.render(
  <Blog mesajlar={mesajlar} />,
  document.getElementById("root")
);
```

<a href="https://codepen.io/gaearon/pen/NRZYGN?editors=0010">CodePen'de Deneyin</a>

Keyler React'te bir ipucu işlevi görür ancak componentlere aktarılmazlar.
Componentlerde aynı değere ihtiyacınız varsa, açıkça farklı bir ada sahip bir props olarak iletebilirsiniz:

```js
const icerik = mesajlar.map((mesaj) =>
  <Mesaj
    key={mesaj.id}
    id={mesaj.id}
    baslik={mesaj.baslik} />
);
```

Yukarıdaki örnekte, `Mesaj` componenti `props.id`yi okuyabilir, ancak `props.key`i okuyamaz.

<h2>map() Fonksiyonunu JSX İçine Karıştırmak</h2>

Yukarıdaki örneklerde hep farklı bir `itemler` değişkeni tanımlayıp ve JSX'e dahil ettik:

```js
function NumaraListesi(props) {
  const sayilar = props.sayilar;
  const itemler = sayilar.map((sayi) =>
    <Itemler key={sayi.toString()}
              value={sayi} />
  );
  return (
    <ul>
      {itemler}
    </ul>
  );
}
```

JSX, herhangi bir ifadeyi süslü parantez içine yerleştirmeye izin verir, böylece `map()` fonksiyonu ile sonucu sıralayabiliriz:

```js
function NumaraListesi(props) {
  const sayilar = props.sayilar;
  return (
    <ul>
      {sayilar.map((sayi) =>
        <Itemler key={sayi.toString()} value={sayi} />
      )}
    </ul>
  );
}
```

<a href="https://codepen.io/gaearon/pen/BLvYrB?editors=0010">CodePen'de Deneyin</a>

Bazen bu daha temiz koda neden olur, ancak bu stil de istismar edilebilir.
JavaScript'te olduğu gibi okunabilirlik açısından bir değişkenin çıkartılmaya değer olup olmadığına karar vermek size aittir.
Kod çok iç içe geçmişse, bir componenti ayıklamak için doğru zamanın geldiğini aklınızda bulundurun.

<a href="https://omergulcicek.github.io/reactjs/formlar">Sıradaki Eğitim: Formlar</a>
