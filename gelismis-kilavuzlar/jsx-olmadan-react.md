<h1>JSX Olmadan React</h1>

JSX, React'ı kullanmak için şart değildir.

JSX bizlere sadece yazım kolaylıkları sağlar. JSX ile yapabileceğiniz herhangi bir şeyi düz JavaScript ile yapılabiliriz.

Örneğin, bu kod JSX ile yazılmıştır:

```js
class Hello extends React.Component {
  render() {
    return <div>Merhaba {this.props.toWhat}</div>;
  }
}

ReactDOM.render(
  <Hello toWhat="Dünya" />,
  document.getElementById('root')
);
```

Yukarıdaki kod, JSX kullanmayan bu koda derlenebilir:

```js
class Hello extends React.Component {
  render() {
    return React.createElement('div', null, `Merhaba ${this.props.toWhat}`);
  }
}

ReactDOM.render(
  React.createElement(Hello, {toWhat: 'Dünya'}, null),
  document.getElementById('root')
);
```

JSX'in JavaScript'e dönüştürülmesiyle ilgili daha fazla örnek görmek istiyorsanız, <a href="https://babeljs.io/repl/#?presets=react&code_lz=GYVwdgxgLglg9mABACwKYBt1wBQEpEDeAUIogE6pQhlIA8AJjAG4B8AEhlogO5xnr0AhLQD0jVgG4iAXyJA">online Babel derleyicisi</a>ni deneyebilirsiniz.

Sürekli `React.createElement` yazmaktan sıkıldıysak, bir kısaltma kullanmak mantıklı olacaktır:

```js
const e = React.createElement;

ReactDOM.render(
  e('div', null, 'Merhaba Dünya'),
  document.getElementById('root')
);
```

Bu kısa formu `React.createElement` için kullanırsanız, JSX olmadan React'i kullanmak elverişli olabilir.

Alternatif olarak, daha kısa bir syntax sunan <a href="https://github.com/mlmorg/react-hyperscript">react-hyperscript</a> ve <a href="https://github.com/ohanhi/hyperscript-helpers">hyperscript-helpers</a> gibi projelere başvurabilirsiniz.

<a href="https://omergulcicek.github.io/reactjs/gelismis-kilavuzlar/fragmentler">Sıradaki Gelişmiş Kılavuz: Fragmentler</a>
