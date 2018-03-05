<h1>Fragmentler</h1>

Bir componentin birden çok element return etmesi React'te yaygın olarak kullanılır. Fragmentler, DOM'a fazladan etiket eklemeden childları gruplanmasına izin verir.

<i>Normalde React'te bir componentin içeriği kapsayıcı bir element ile return edilirdi. Kapsayıcı element olmazsa hata veriyordu. Buda fazladan `<div>` tagı oluşturulmasına sebep oluyordu. Fakat `React v16.2.0` ile artık hayali bir kapsayıcı olan `Fragment`i oluşturabiliyoruz. Bu fragmentler çıktıyı kapsadığı için içerik return edilebilecek fakat çıktıda görünmeyeceklerdir. Böylece fazladan div oluşumu önlenmiş olacaktır.</i>

<i>Aşağıdaki içeriği React componentinde return etmek istediğimizi düşünelim.</i>

```html
Biraz yazı
<h2>Başlık</h2>
Daha fazla yazı
<h2>Diğer başlık</h2>
Daha fazla yazı
```

React versiyon 16.2.0'dan önce bunu gerçekleştirmenin tek yolu, childları `div`, `span` gibi bir tag ile aşağıdaki gibi sarmalamaktır:

```js
render() {
  return (
    // Fazladan bir div :(
    <div>
      Biraz yazı
      <h2>Başlık</h2>
      Daha fazla yazı
      <h2>Diğer başlık</h2>
      Daha fazla yazı
    </div>
  );
}
```

<h2>Kullanımı</h2>

<i>return edilecek değerleri `<React.Fragment>` componenti içerisine yerleştirmeniz yeterli.</i>

```jsx
class Columns extends React.Component {
  render() {
    return (
      <React.Fragment>
        <td>Merhaba</td>
        <td>Dünya</td>
      </React.Fragment>
    );
  }
}
```

<i>`React.Fragment` yerine sadece `Fragment` ile kapsamak isterseniz aşağıdaki gibi bir yol izleyebilirsiniz.</i>

```js
const Fragment = React.Fragment;

<Fragment>
  <ChildA />
  <ChildB />
  <ChildC />
</Fragment>

// Her ikiside aynı şeydir
<React.Fragment>
  <ChildA />
  <ChildB />
  <ChildC />
</React.Fragment>
```

<h3>Kısa Syntax</h3>

Fragmentler için yeni bir kısa syntaxta var ancak henüz tüm popüler toollar (<i>araçlar</i>) tarafından desteklenmemektedir.

```jsx
class Columns extends React.Component {
  render() {
    return (
      <>
        <td>Merhaba</td>
        <td>Dünya</td>
      </>
    );
  }
}
```

 `<></>` kullanabilirsiniz fakat keys yada attribute kullanımını desteklemez (<i>Sadece kapsayıcı olarak kullanılır</i>).

Birçok toolsun henüz kısa syntax kullanımını desteklemediğini unutmayın, bu nedenle destek gelene kadar açıkça `<React.Fragment>` yazın.

<h3>Keyli Fragmentler</h3>

`<React.Fragment>` syntaxı ile bildirilen parçaların keyleri olabilir. Örneğin bir açıklama listesi oluşturmak için:

```jsx
function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        // `key` olmazsa, React bir key uyarısı verecektir
        <React.Fragment key={item.id}>
          <dt>{item.term}</dt>
          <dd>{item.description}</dd>
        </React.Fragment>
      ))}
    </dl>
  );
}
```

`Fragment`e aktarılabilen tek attribute `key`dir. Gelecekte, click-change olayları gibi ek attributeler için destek ekleyebiliriz.

<a href="https://codepen.io/reactjs/pen/VrEbjE?editors=1000">CodePen'de Deneyin</a>

<a href="https://omergulcicek.github.io/reactjs/gelismis-kilavuzlar/lifecycle-fonksiyonlari">Sıradaki Gelişmiş Kılavuz: Lifecycle Fonksiyonları</a>
