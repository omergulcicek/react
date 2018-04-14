<h1>Ajax Kullanımı</h1>

React ile istediğiniz herhangi bir AJAX kütüphanesini kullanabilirsiniz.

Popüler olanlar <a href="https://github.com/axios/axios">Axios</a>, <a href="https://api.jquery.com/jQuery.ajax/">jQuery AJAX</a> ve tarayıcıda yerleşik olarak bulunan <a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API">window.fetch</a>.

<h2>Lifecycleda AJAX isteğini nerede yapmalıyım?</h2>

AJAX isteklerini `componentDidMount` fonksiyonunda kullanmalısınız. AJAX isteğinden gelen veriyi `setState` yardımıyla state'e atarak componentin içerisinde kullanabilirsiniz.

Aşağıdaki component, `state`i doldurmak için `componentDidMount`ta bir AJAX çağrısının nasıl yapılacağını gösterir:

```js
{
  items: [
    { id: 1, name: 'Apples', price: '$2' },
    { id: 2, name: 'Peaches', price: '$5' }
  ] 
}
```

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      error: null,
      isLoaded: false,
      items: []
    };
  }

  componentDidMount() {
  //AJAX isteğini burada başlatıyoruz.
    fetch("https://api.example.com/items")
      .then(res => res.json())
      .then(
        (result) => {
        //AJAX'tan gelen veri ile state'imizi güncelliyoruz.
          this.setState({
            isLoaded: true,
            items: result.items
          });
        },
        (error) => {
          this.setState({
            isLoaded: true,
            error
          });
        }
      )
  }

  render() {
    const { error, isLoaded, items } = this.state;
    if (error) {
      return <div>Error: {error.message}</div>;
    } else if (!isLoaded) {
      return <div>Yükleniyor...</div>;
    } else {
      return (
        <ul>
          {items.map(item => (
            <li key={item.name}>
              {item.name} {item.price}
            </li>
          ))}
        </ul>
      );
    }
  }
}
```

<i>Gelişmiş kılavuzlar sonlanmıştır. Bu aşamadan sonra <b>Uygulamalı Eğitime</b> geçiş yapılacaktır.</i>

<a href="https://omergulcicek.github.io/reactjs/uygulamali-egitim/xox-oyunu">Sıradaki Eğitim: XOX Oyunu</a>
