<h1>Elementleri Render Etmek</h1>

Elementler React uygulamalarının en küçük yapı taşlarıdır.

Bir element, ekranda görmek istediğiniz şeyi tanımlar:

```js
const element = <h1>Merhaba Dünya</h1>;
```
Tarayıcı DOM elementlerinden farklı olarak, React elementleri düz nesnelerdir ve oluşturulması kolaydır.
React DOM, React elementleriyle eşleşecek şekilde DOM'u güncellemekle ilgilenir.

<i>Bu konu hakkında detaylı Türkçe bilgi için <a href="https://fatihacet.com/react-ve-virtual-dom-mimarisi-uzerine">Fatih Acet'in makalesi</a>ne göz atabilirsiniz.</i>

>**Not:**
>
>Daha yaygın olarak bilinen component kavramıyla elementler karıştırılabilir.
>Bir sonraki bölümde componentleri tanıtacağız.

<i>Elementleri birer değişken, componentleri ise fonksiyon olarak düşünebilirsiniz; birbirinden farklı şeylerdir.</i>

<h2>Bir Elementi DOM'a Render Etmek</h2>

HTML dosyanızda bir `<div>` olduğunu varsayalım:

```html
<div id="root"></div>
```

Buna root DOM düğümü diyoruz çünkü içindeki her şey React DOM tarafından yönetilecektir.

<i>DOM düğümü hakkında detaylı bilgi için <a href="https://www.w3schools.com/js/js_htmldom_navigation.asp">JavaScript HTML DOM Navigation</a> içeriğini inceleyenilirsiniz.</i>

Sadece React ile oluşturulmuş uygulamalar genellikle tek bir root DOM düğümüne sahiptir.

React'i mevcut bir uygulamaya entegre ediyorsanız, istediğiniz kadar çok sayıda ayrı root DOM düğümü olabilir.

React elementini bir root DOM düğümüne dönüştürmek için, her ikisini de `ReactDOM.render()` işlevine yerleştirin.

```js
const element = <h1>Merhaba Dünya!</h1>;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

<a href="http://codepen.io/gaearon/pen/rrpgNB?editors=1010">CodePen'de Deneyin</a>

Sayfanızda "Merhaba Dünya!" başlığı görüntülenecektir.

<h2>Oluşturulan Bir Elementi Güncellemek</h2>

React elementleri değişmez. Bir element oluşturduktan sonra, elementin alt elementlerini veya attributelerini değiştiremezsiniz.

<i>Konu hakkında detaylı bilgi için </i><a href="https://medium.com/codefiction/i%CC%87pin-ucunu-ka%C3%A7%C4%B1rmamak-redux-8d822da0d19b">Onur Aykaç'ın yazdığı makale</a><i>de <b>Javascript’te immutable ve mutable kavramı</b> bölümünü okuyabilirsiniz.</i>

Bildiğimiz kadarıyla UI'ı güncellemenin tek yolu yeni bir element oluşturmak ve `ReactDOM.render()` fonksiyonuna geçirmektir.

Aşağıdaki saat örneğini inceleyelim.

```js
function tick() {
  const element = (
    <div>
      <h1>Merhaba Dünya!</h1>
      <h2>Saat şu anda {new Date().toLocaleTimeString()}</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

<a href="http://codepen.io/gaearon/pen/gwoJZk?editors=0010">CodePen'de Deneyin</a>

`ReactDOM.render()` fonksiyonunu her saniye setInterval() içerisinden çağırır.

>**Not:**
>
>Pratikte React uygulamalarının çoğu, bir kez `ReactDOM.render()` elementini çağırır.
>
>Birbiriyle bağlantı kurduğu için konuları atlamadan okumaya devam edin.

<i>Yukarıdaki saat örneğinde `setInterval` fonksiyonu sayesinde her saniye fonksiyon çağırılır ve ReactDOM render edilir.
Fakat pratikte bu kodlar bu şekilde yazılmıyor. ReactDOM bir kez render edilir ve oluşturulan elementler `state`ler yardımıyla güncellenir.
İlerleyen konularda bunlara değineceğiz.</i>

React DOM, componenti ve child (<i>çocuk</i>) componentleri önceki componentle karşılaştırır ve DOM'u istenen duruma getirmek için gereken yerlerde DOM güncellemelerini uygular.

<i>Yani, React DOM tüm componentleri yeniden yüklemez. Değişiklik olan yeri algılar ve DOM üzerinde sadece o kısmı günceller, buda performansı olumlu yönde etkiler.</i>

Tarayıcı üzerinden bu örneği inceleyerek doğrulayabilirsiniz.

<img src="https://reactjs.org/granular-dom-updates-c158617ed7cc0eac8f58330e49e48224.gif" alt="react dom örneği">

<a href="https://omergulcicek.github.io/reactjs/component-ve-props">Sıradaki Eğitim: Component ve Props</a>
