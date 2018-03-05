<h1>Kazananı Bildirmek</h1>

Bir oyunun ne zaman kazanılacağını gösterelim. Bu fonksiyonu dosyanın sonuna ekleyin:

```js
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

Birisi oyunu kazanırsa, kimin kazanıp kazanmadığını kontrol etmek ve state metnini "Kazanan: [X/O]" gösterilmesini sağlamak için `Board` componentinin `render` fonksiyonuna gerekli kodları ekleyelim.

Board'un `render`ındaki `status` bildirimini şu kodla değiştirin:

```js
  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Kazanan: ' + winner;
    } else {
      status = 'Sıradaki Oyuncu: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      // geri kalanı değişmedi
```

Artık, oyunda birisi kazanmışsa veya bir kare zaten doldurulmuşsa tıklamayı erkenden return etmek için `Board`un `handleClick`ini değiştirebilirsin:

```js
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

Tebrik ederiz! Artık tic-tac-toe oyunu geliştirdiniz. Ve şimdi React'in temellerini uygulamalı olarak gördünüz. Burada asıl kazanan sizsiniz !

<a href="https://codepen.io/gaearon/pen/LyyXgK?editors=0010">Mevcut kodu görüntüleyin</a>

<a href="https://omergulcicek.github.io/reactjs/ornek-projeler/ornek-projeler">Örnek Projelere Göz Atın</a>
