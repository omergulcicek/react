<h1>Sıradaki Oyuncu</h1>

Oyunumuzda bariz bir hata bulunmakta, sadece X hamle yapabiliyor; bunu düzeltelim.

Varsayılan ilk hareketin 'X' olacağına karar verelim. Başlangıç state'ini `Board` constructoründe değiştirelim:

```js
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }
```

Her hamle yapıldığında `xIsNext` değerini değiştirerek sıranın `X` ya da `O`ya geçmesini sağlayalım. Board'un `handleClick` fonksiyonunu` xIsNext` değerini değiştirmek için güncelleyin:

```js
  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

Şimdi X ve O sırayla hamle yapacak. Ardından, Board'un `render` fonksiyonu içindeki `status` stringini de değiştirip, sıradaki oyuncunun kim olduğunu gösterelim:

```js
  render() {
    const status = 'Sıradaki Oyuncu: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      // geri kalan kodlar değişmedi
```

Bu değişikliklerden sonra Board componentinin son hali şu şekilde olmalı:

```js
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Sıradaki Oyuncu: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

<a href="https://codepen.io/gaearon/pen/KmmrBy?editors=0010">Mevcut kodu görüntüleyin</a>

<a href="https://omergulcicek.github.io/react/uygulamali-egitim/kazanani-bildirmek">Sıradaki Eğitim: Kazananı Bildirmek</a>
