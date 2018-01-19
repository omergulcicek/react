<h1>Lifecycle Fonksiyonları</h1>

`React.Component` soyut temel bir sınıftır, bu nedenle doğrudan React.Componente başvurmak mantıklı değildir. Bunun yerine, genellikle classın alt classını tanımlayıp, bir `render()` metodu tanımlarsınız.

Normalde bir React componentini düz bir JavaScript sınıfı olarak tanımlarsınız:

```js
class Greeting extends React.Component {
  render() {
    return <h1>Merhaba, {this.props.name}</h1>;
  }
}
```

ES6'yı henüz kullanmıyorsanız, bunun yerine `create-react-class` modülünü kullanabilirsiniz. Daha fazla bilgi edinmek için <a href="https://omergulcicek.github.io/reactjs/es6-olmadan-react">ES6 olmadan React</a> konusuna bakın.

Unutmayın, kendi temel component classlarınızı oluşturmanızı önermiyoruz. Kodun tekrar kullanımı React'te inheritancetan ziyade composition yoluyla elde edilir. Composition kullanma konusunda bir fikir edinmek için <a href="https://omergulcicek.github.io/reactjs/composition-ve-inheritance">composition ve inheritance</a> sayfasını inceleyin.

Her componentin, lifecycle  fonksiyonları vardır. İçerisinde `will` geçen fonksiyonlar component oluşturulmasından hemen önce çağrılırken, içerisinde `did` geçen fonksiyonlar component kaldırıldıktan sonra çağrılır.

<i>Şimdi tüm fonksiyonları bölümlendirip, ardından her birini açıklayacağız. Başlıklara çeviri yapılmamıştır, altlarına Türkçesi eklenmiştir.</i>

<h4>Mounting</h4>

<i>Oluşturmak</i>

Bu fonksiyonlar, bir component örneği oluşturulurken ve DOM'a eklendiğinde çağrılır:

- [`constructor()`](#constructor)
- [`componentWillMount()`](#componentwillmount)
- [`render()`](#render)
- [`componentDidMount()`](#componentdidmount)

<h4>Updating</h4>

<i>Güncellemek</i>

Bir güncelleme, props ya da state değişikliklerinden kaynaklanabilir. Bu fonksiyonlar, bir componentin güncellenmesiyle çağrılır.

- [`componentWillReceiveProps()`](#componentwillreceiveprops)
- [`shouldComponentUpdate()`](#shouldcomponentupdate)
- [`componentWillUpdate()`](#componentwillupdate)
- [`render()`](#render)
- [`componentDidUpdate()`](#componentdidupdate)

<h4>Unmounting</h4>

<i>Kaldırmak</i>

Bu fonksiyon, bir component DOM'dan kaldırıldığında çağrılır:

- [`componentWillUnmount()`](#componentwillunmount)

<h4>Error Handling</h4>

<i>Hata işleme</i>

Bu fonksiyon, render sırasında lifecycle fonksiyonlarında veya herhangi bir alt componentin constructoründe bir hata olduğunda çağrılır.

- [`componentDidCatch()`](#componentdidcatch)

<h3>Diğer API'ler</h3>

Her component aşağıdaki API'leride içerisinde barındırır:

- [`setState()`](#setstate)
- [`forceUpdate()`](#forceupdate)

<h3>Class Propertyleri</h3>

- [`defaultProps`](#defaultprops)
- [`displayName`](#displayname)

<h3>Instance Propertyleri</h3>

- [`props`](#props)
- [`state`](#state)

* * *

<i>Bu kısım güncellenecek...</i>

<a href="https://omergulcicek.github.io/reactjs/react-terimler-sozlugu">Sıradaki Gelişmiş Kılavuz: React Terimler Sözlüğü</a>
