<h1>Veriyi Korumanın Önemi</h1>

Önceki kod örneğinde, `.slice()` fonksiyonunu kullanarak `squares` dizisinde değişiklik yapmadan önce kopyalamayı ve varolan dizinin orijinal halini korumanızı öneririz. Bunun ne anlama geldiğini ve neden önemli bir konu olduğunu konuşalım.

Verileri değiştirmek için genellikle iki yol vardır. İlk yöntem, bir değişkenin değerlerini doğrudan değiştirmek. İkinci yöntem ise veriyi istenen değişiklikleri de içeren yeni bir kopyasını oluşturmaktır.

<h3>Veriyi Doğrudan Değiştirmek</h3>

```js
var player = {score: 1, name: 'Ömer'};
player.score = 2;
// player objesinin son hali: {score: 2, name: 'Ömer'}
```

<h3>Verinin Kopyasını Oluşturmak</h3>

```js
var player = {score: 1, name: 'Ömer'};

var newPlayer = Object.assign({}, player, {score: 2});
// player objesi değişmedi ve kopyası oluşuturup score değerinde güncelleme yapıldı.
// newPlayer objesinin son hali: {score: 2, name: 'Ömer'}

// Veya obje yayılım syntax kullanıyorsanız, şu şekilde de yazabilirsiniz:
// var newPlayer = {...player, score: 2};
```

<h4>Daha Kolay Geri Alma / Yeniden Yapmak</h4>

Değişmezlik ayrıca bazı karmaşık özelliklerin uygulanmasını çok daha kolay hale getirir. Örneğin, bu eğitimde oyunun farklı aşamaları arasında zaman yolculuğu yapacağız.

<i>XOX oynarken önceki adımlara gidebilmek için adım adım aşamaları kayıt altına almak gerekiyor. Daha sonra uygulamamızın sağ tarafına, önceki adımlara gidebilmek için butonlar ekleyeceğiz.</i>

Değişmezlik ayrıca bazı karmaşık özelliklerin uygulanmasını çok daha kolay hale getirir. Örneğin, bu eğitimde oyunun farklı aşamaları arasında zaman yolculuğu yapacağız.

<h4>Track Değişiklikleri</h4>

Değişikliğe uğrayan bir objenin değişip değişmediğini belirlemek zordur, çünkü değişiklikler doğrudan objeye yapılır. Bu daha sonra, geçerli objeyi önceki bir kopyayla karşılaştırma, tüm obje ağacını çaprazlama ve her değişkeni ve değeri karşılaştırmayı gerektirir. Bu süreç giderek daha karmaşık hale gelebilir.

Değiştirilebilir bir objenin nasıl değiştiğini belirlemek oldukça kolay. Objenin son hali daha öncekinden farklıysa obje değişmiş demektir, bu kadar.

<h4>Reactın Ne Zaman Yeniden Render Edileceğini Belirleme</h4>

React'te değiştirilemezliğin en büyük yararı, saf componentleri oluşturduğunuzda gelir. Değişmez veriler, değişikliklerin yapılıp yapılamadığını daha kolay belirleyebildiğinden, bir componentin ne zaman yeniden oluşturulmasını istediğini belirlemeye yardımcı olur.

<h3>Fonksiyonel Componentler</h3>

Constructorü kaldırdık ve aslında React, fonksiyonel component olarak adlandırılan yalnızca bir `render` fonksiyonundan oluşan Square gibi component türleri için daha basit bir syntax destekliyor. `extends React.Component` gibi uzunca class tanımlamak yerine props alan ve render edilecek olanı return eden bir fonksiyon yazın.

Tüm Square classını bu fonksiyonla değiştirin:

```js
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```

Uygulamalarınızdaki birçok component fonksiyonel component olarak yazılabilir. Bu componentleri yazmak daha kolaydır ve React tarafından optimize edilirler.

`onClick={() => props.onClick()}`i de yalnızca `onClick={props.onClick()}` olarak değiştirdik. `onClick={props.onClick()}` işe yaramayacağına dikkat edin, çünkü onu aşağıya aktarmak yerine `props.onClick`i çağırırdı.

<a href="https://codepen.io/gaearon/pen/QvvJOv?editors=0010">Mevcut kodu görüntüleyin</a>

<a href="https://omergulcicek.github.io/reactjs/siradaki-oyuncu">Sıradaki Eğitim: Sıradaki Oyuncu</a>
