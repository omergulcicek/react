<h1>XOX Oyunu</h1>

Uygulamalı olarak adım adım XOX oyununu geliştireceğiz, projenin bitmiş hali şudur: <a href="https://codepen.io/gaearon/pen/LyyXgK?editors=0010">XOX Oyunu<a>

CSS kodları hazır olarak verilmiş durumda, biz sadece JavaScript geliştirmesi yapacağız.

XOX oyunu için görseldeki gibi 3x3'lük bir oyun alanına ihtiyacımız vardır.

<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSakAazYLzTjHx9BcWWc2mcfuu7Lt9ZH2xU6ee-x0MojyNLYb3w" height="100">

Burada her bir kareyi oluşturan componentimizin adı `Square` olacak.

9 kareyi birleştirerek oyun alanını render eden componentimizin adı ise `Board` olacak.

`Game` componenti ise tüm içeriği kapsayan bir tablo render edecek.

Yani başlıca üç componente sahibiz:

- Square
- Board
- Game

Başlangıç için <a href="https://codepen.io/gaearon/pen/oWWQNa?editors=0010">XOX Başlangıç Kodu</a>nu kullanacağız.

Kod uzun ve karmaşık gelebilir, fakat incelediğinizde basit şeyler ile oluşturulduğunu ve aslında karmaşık olmadığını anlayacaksınız. Yeterli düzeyde olduğunuzu düşünmüyorsanız <a href="https://omergulcicek.github.io/reactjs/merhaba-dunya">react dokümanının en başına</a> dönerek bilgilerinizi tazeleyebilirsiniz.

<a href="https://omergulcicek.github.io/reactjs/verileri-props-uzerinden-gecirmek">Sıradaki Eğitim: Verileri Props Üzerinden Geçirmek</a>
