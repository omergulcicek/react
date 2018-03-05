<h1>Etkileşimli Component</h1>

`Square` componentine tıkladığınızda bir "X" işareti dolduracak şekilde güncelleyelim. `Square` componentinde `render()` fonksiyonunu şöyle değiştirmeyi deneyin:


```js
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={() => alert('tıklandı')}>
        {this.props.value}
      </button>
    );
  }
}
```

Bir kareye tıklarsanız, tarayıcınızda alert (<i>uyarı</i>) almanız gerekiyor.

Burada JavaScript ok fonksiyon syntaxı kullanılmıştır. Fonksiyonu `onClick` propsu olarak geçtiğimizi unutmayın.

<i>Normalde click change gibi olaylarda bind etmek gerekiyor fakat ok fonksiyonu ve bazı diğer yöntemleri kullanarak constructorde bind etmedende click ve change'i kullanabiliyoruz. Detaylar için <a href="https://omergulcicek.github.io/reactjs/click-ve-change-olaylari">click ve change olayları</a> başlığına bakabilirsiniz.</i>

`OnClick = {alert ('tıklandı')}` olarak yazsaydık, click yapmak yerine sadece uyarırdı.

React componentleri, constructorde `this.state`e sahip olabilirler; bu component için özel olarak düşünülmelidir. Kareye tıklatıldığında değişmesini sağlayalım.

İlk önce, state'i başlatmak için classa bir constructor ekleyin:

```js
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => alert('tıklandı')}>
        {this.props.value}
      </button>
    );
  }
}
```

JavaScript classlarında, bir alt clasın constructorünü tanımlarken, `super();`i çağırmanız gerekir.

Şimdi ise click yapıldığında karede X yazması için state'i güncelleyecek şekilde kodumuzu değiştirelim.

* `this.props.value`u `this.state.value` ile `<button>` etiketinin içinde değiştirin.

<i>Önceki halinde üst componentten parametre alıyorduk fakat artık state'teki değeri alacağımız için `props` yerine `state` kullanmalıyız.</i>

* `() => alert()`ı `() => this.setState({value: 'X'})` olacak şekilde değiştirin.

<i>Daha sonra X ve O yazması için gerekli kodları ekleyeceğiz. Şimdilik her click yapıldığında stateteki valueyu X olacak şekilde güncelliyoruz. State güncellendiğinde component tekrardan render edildiği için güncel değeri karenin içerisine yazacaktır.</i>

Şimdi `<button>` tagımız şu şekilde görünmelidir:

```js
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => this.setState({value: 'X'})}>
        {this.state.value}
      </button>
    );
  }
}
```

`this.setState` çağrıldığında, component için bir güncelleme planlanır ve componenti alt öğeleri ile birlikte yeniden render edilmesine neden olur. Component yeniden render edildiğinde, `this.state.value` `X` olur, böylece karede bir X görürsünüz.

Herhangi bir kareyi tıklarsanız, içinde bir X görünmelidir.

<a href="https://codepen.io/gaearon/pen/VbbVLg?editors=0010">Mevcut kodu görüntüleyin</a>

<a href="https://omergulcicek.github.io/reactjs/veriyi-korumanin-onemi">Sıradaki Eğitim: Veriyi Korumanın Önemi</a>
