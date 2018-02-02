<h1>Verileri Props Üzerinden Geçirmek</h1>

`Board` componentinden `Square` componentine bazı verileri geçirmeyi deneyelim.

Board'un `renderSquare` fonksiyonunda, bir `value` propsu `Square`ye geçirmek için kodu değiştirin:

```js
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
```

Daha sonra `{/ * TODO * /}` yazan kısmı `{this.props.value}` ile Square'ın `render` fonksiyonunu değiştirin:

```js
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

Önce: <i>Kodun ilk halinde karelerin içi boştu.</i>

<img src="https://reactjs.org/static/tictac-empty-1566a4f8490d6b4b1ed36cd2c11fe4b6-a9336.png" height="200" />

Sonra: Render edilmiş çıktıda her karede bir sayı görmeniz gerekiyor.

<img src="https://reactjs.org/static/tictac-numbers-685df774da6da48f451356f33f4be8b2-be875.png" height="200" />

<a href="https://codepen.io/gaearon/pen/aWWQOG?editors=0010">Mevcut kodu görüntüleyin</a>

<i>`Board` componentinin render fonksiyonundan `this.renderSquare()` fonksiyonu çağırılıyor. Parametre olarak ise 0'dan 8'e kadar parametreler gönderilmiş. `this.renderSquare` fonksiyonu ise `Square` componentini return ediyordu. Fakat içerisinde herhangi bir içerik yoktu. `value={i}` yaparak `Square` componentine `value` değerleri gönderdik. `Square` componentinde ise gelen bu valueyu `this.props.value` ile yazdırdık. Böylece oyun alanımızda karelerde 0'dan 8'e kadar rakamlar yazdırarak verileri props üzerinden componente geçirmiş olduk.</i>

<a href="https://omergulcicek.github.io/reactjs/etkilesimli-component">Sıradaki Eğitim: Etkileşimli Component</a>

