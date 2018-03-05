<h1>Listeler ve Keyler</h1>

Önce, JavaScript'te listeleri nasıl dönüştürdüğümüzü gözden geçirelim.
Aşağıdaki kod göz önüne alındığında, bir dizi sayı almak ve değerlerini ikiye katlamak için `map()` fonksiyonunu kullanıyoruz.
`map()` tarafından return edilen çift katlı değerleri kaydederiz:

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);
```

Konsola `[2, 4, 6, 8, 10]` yazacaktır.

<i>Google Chrome'da (diğer tarayıcılarda da benzer yada aynıdır) <b>F12</b>'ye basıp,
"Console (yada Konsol)" sekmesine gelip bu kodları yapıştırarak test edebilirsiniz.

Ok fonksiyonları ile ilgili dokümantasyon hazırlandığında bu kısım güncellenecektir.
Kısaca özet geçmek gerekirse yukarıda map fonksiyonunun içerisinde yapılan işlem (`(number) => number * 2`) şudur:

`number` parametre alınır ve `number*2` return edilir.

Fonksiyonun kolay okunabilir hali ise şudur:
</i>

```js
function(number) {
  return number*2;
}
```

React'te, dizi elemanlarını listelere dönüştürmek neredeyse aynıdır.

<h2>Birden Çok Component Vermek</h2>

Koleksiyonları oluşturabilir ve bunları JSX içine süslü parantez `{}` kullanarak ekleyebilirsiniz.

Aşağıda, JavaScript `map()` fonksiyonu kullanarak numbers dizisinde döngü oluşturuyoruz.
Her liste için bir `<li>` return ediyoruz. Son olarak, elde edilen sonuç dizisini `listItems`e atayacağız:

```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
```

Bütün `listItems` dizesini `<ul>` elemanının içerisine dahil ediyoruz ve bunu DOM'a gönderiyoruz:

```javascript
ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/GjPyQr?editors=0011">CodePen'de Deneyin</a>

Bu kod, ekrana `ul` kapsayıcısı ve `li`ler içerisinde rakamları yazacaktır.

<h2>Temel Liste Componenti</h2>

Genellikle listeleri bir component içinde render ederiz.

Önceki örneği, `numbers` adında bir dizi kabul eden ve liste çıktısı yapan bir componente dönüştürebiliriz.

```javascript
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

Bu kodu çalıştırdığınızda, liste için bir `key` (anahtar) verilmesi yönünde bir uyarı verilir.

<i>Burada key kelimesine (Türkçe'si anahtar demek olmasına rağmen) anahtar çevirisi tam olarak uymuyor.
Key denirken aslında benzersizi ifade etmektedir (ID, Kimlik numarası, parmak izi gibi)</i>.

Bir `key`, listeleri oluşturulurken eklenmesi gereken özel bir attribute'tür.
Bir sonraki bölümde bunun neden önemli olduğunu anlatacağız.
`numbers.map()` içindeki listelere birer `key` atayalım.

```js
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/jrXYRR?editors=0011">CodePen'de Deneyin</a>

<h2>Keyler</h2>

`Key`ler yardımı ile hangi listenin değiştiğini, eklendiğini veya kaldırıldığını belirleyebiliriz.
Elemanlara istikrarlı bir kimlik kazandırmak için dizideki listelere `key` verilmelidir:

```js
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

Bir `key` seçmenin en iyi yolu, kardeşleri (<i>diğer `li`ler</i>) arasında bir tanımlanan bir kimlik kullanmaktır.
Çoğu zaman, verilerinizdeki id'ler `key` olarak kullanılır:

```js
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

Eğer bu tarzda bir yapınız yoksa benzersiz olacağı için `key`lere `index` verebiliriz:

```js
const todoItems = todos.map((todo, index) =>
  // Listelerin benzersiz id'leri yoksa bu yöntemi kullanın.
  <li key={index}>
    {todo.text}
  </li>
);
```

Listelerin sırası değişebilirse keyler için index kullanmanızı önermiyoruz.
Bu, performansı olumsuz etkileyebilir ve component state'i ile ilgili sorunlara neden olabilir.

Ayrıntılı bilgi için <a href="https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318">Robin Pokorny</a>'nin makalesini inceleyebilirsiniz (<i>İngilizce</i>).

Listelere siz key atamazsanız React varsayılan olarak index'i atar.

<h2>Keyler Yalnızca Kardeşleri Arasında Benzersiz Olmalıdır</h2>

Dizilerde kullanılan keyler kardeşleri arasında benzersiz olmalıdır.
Bununla birlikte, global olarak benzersiz olması gerekmez.

İki farklı diziyi üretirken aynı keyleri kullanabiliriz:

```js
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Merhaba Dünya', content: 'React Öğreniyoruz!'},
  {id: 2, title: 'Ömer Gülçiçek', content: 'React JS Türkçe Dokümantasyon'}
];
ReactDOM.render(
    <Blog posts={posts} />,
    document.getElementById('root')
);
```

<a href="https://codepen.io/gaearon/pen/NRZYGN?editors=0010">CodePen'de Deneyin</a>

Keyler React'te bir ipucu işlevi görür ancak componentlere aktarılmazlar.
Componentlerde aynı değere ihtiyacınız varsa, açıkça farklı bir ada sahip bir props olarak iletebilirsiniz:

```js
const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);
```

Yukarıdaki örnekte, `Post` componenti `props.id`yi okuyabilir, ancak `props.key`i okuyamaz.

<h2>map() Fonksiyonunu JSX İçine Karıştırmak</h2>

Yukarıdaki örneklerde hep farklı bir `listItems` değişkeni tanımlayıp ve JSX'e dahil ettik:

```js
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

JSX, herhangi bir ifadeyi süslü parantez içine yerleştirmeye izin verir, böylece `map()` fonksiyonu ile sonucu sıralayabiliriz:

```js
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}
```

<a href="https://codepen.io/gaearon/pen/BLvYrB?editors=0010">CodePen'de Deneyin</a>

Bazen bu daha temiz koda neden olur, ancak bu stil de istismar edilebilir.
JavaScript'te olduğu gibi okunabilirlik açısından bir değişkenin çıkartılmaya değer olup olmadığına karar vermek size aittir.
Kod çok iç içe geçmişse, bir componenti ayıklamak için doğru zamanın geldiğini aklınızda bulundurun.

<a href="https://omergulcicek.github.io/reactjs/hizli-baslangic/formlar">Sıradaki Eğitim: Formlar</a>
