<h1>Derinlemesine JSX</h1>

Temel olarak, JSX sadece `React.createElement(component, props, ...children)` fonksiyonları için syntax sağlar.

JSX kodu:

```js
<MyButton color="blue" shadowSize={2}>
  Tıkla
</MyButton>
```

Yukarıdaki kodu, bu koda derler:

```js
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'Tıkla'
)
```

Hiçbir child yoksa etiketi direkt kapatarakta kullanabilirsiniz:

```js
<div className="sidebar" />
```

Yukarıdaki kodu, bu koda derler:

```js
React.createElement(
  'div',
  {className: 'sidebar'},
  null
)
```

JSX'in JavaScript'e nasıl dönüştürüldüğünü test etmek isterseniz, <a href="https://babeljs.io/repl/#?presets=react&code_lz=GYVwdgxgLglg9mABACwKYBt1wBQEpEDeAUIogE6pQhlIA8AJjAG4B8AEhlogO5xnr0AhLQD0jVgG4iAXyJA">online Babel derleyicisini</a> deneyebilirsiniz.

<h2>React'te Element Tipini Belirleme</h2>

Bir JSX etiketinin ilk harfi, React elementinin türünü belirler.

Büyük harfle başlayan bir JSX etiketi, bunun bir React componenti olduğunu belirtir. Bu etiketler, adlandırılmış değişkene doğrudan referans olarak derlenir; bu nedenle, JSX `<Foo />` ifadesini kullanırsanız, `Foo` scope (<i>kapsam</i>) dahilinde olmalıdır.

<h2>React Scope'ta Olmalı</h2>

JSX `React.createElement` çağrısına derlediğinden, `React` kitaplığı daima JSX kodunuzun scope'unda olmalıdır.

Örneğin, `React` ve `CustomButton` doğrudan JavaScript'te atıf yapılmamasına rağmen, bu kodda her iki importta gereklidir:

```js
import React from 'react';
import CustomButton from './CustomButton';

function WarningButton() {
  // return React.createElement(CustomButton, {color: 'red'}, null);
  return <CustomButton color="red" />;
}
```

Bir JavaScript paketleyicisi kullanmazsanız ve React'i  `<script>` etiketi ile yüklediyseniz, zaten `React` globali scopetadır.

<h2>Nokta Notasyonunu JSX Türü İçin Kullanma</h2>

JSX içinde nokta işareti kullanarak bir React componentine başvurabilirsiniz. Birçok React componenti ihraç eden bir modülünüz varsa bu uygundur. Örneğin, `MyComponents.DatePicker` bir component ise, bunu doğrudan JSX'den şu şekilde kullanabilirsiniz:

```js
import React from 'react';

const MyComponents = {
  DatePicker: function DatePicker(props) {  
    return <div>Buraya {props.color} geldiğini düşünün.</div>;
  }
}

function BlueDatePicker() {
  return <MyComponents.DatePicker color="blue" />;
}
```

<h2>Componentler Büyük Harf İle Başlamalıdır</h2>

Bir element türü küçük harfle başlarsa, `<div>` veya `<span>` gibi yerleşik bir componente atıfta bulunur ve `React.createElement` alanına aktarılan bir string `'div'` veya `'span'` ile sonuçlanır. `<Foo />` gibi büyük harfle başlayan türler `React.createElement(Foo)`'ya derlenir ve JavaScript dosyanızda tanımlanmış veya içe aktarılmış bir componente karşılık gelir.

Componentlerin ilk harfini büyük harfle isimlendirmenizi öneririz. Küçük harfle başlayan bir componente sahipseniz, JSX'de kullanmadan önce baş harfini büyük harfe dönüştürün.

Örneğin, bu kod beklendiği gibi çalışmaz:

```js
import React from 'react';

// Hata! Bu bir component ve baş harfi büyük yazılmış olmalıydı:
function hello(props) {
  // Doğru! Div, geçerli bir HTML etiketi olduğu için <div> kullanımının meşru olduğunu söyleyebiliriz.
  return <div>Merhaba {props.toWhat}</div>;
}

function HelloWorld() {
  // Yanlış! React <hello />'nun büyük harf kullanmadığından bunun bir HTML etiketi olduğunu düşünür.
  return <hello toWhat="World" />;
}
```

Bunu düzeltmek için, `hello` elementini `Hello` olarak yeniden adlandırıp, ona atıfta bulunmak için ise `<Hello />` kullanacağız:

```js
import React from 'react';

// Doğru! Bu bir component ve baş harfi büyük yazılmıştır:
function Hello(props) {
  // Doğru! Div, geçerli bir HTML etiketi olduğu için <div> kullanımının meşru olduğunu söyleyebiliriz.
  return <div>Merhaba {props.toWhat}</div>;
}

function HelloWorld() {
  // Doğru! React, <Hello />'nun component olduğunu bilir çünkü büyük harfle başlamıştır.
  return <Hello toWhat="World" />;
}
```

<h2>Runtime Olarak Tür Seçimi</h2>

React element türü olarak genel bir ifade kullanamazsınız. Elementin türünü belirtmek için genel bir ifade kullanmak istiyorsanız, önce önce baş harfi büyük bir değişkene atayın. Bu, genellikle bir pakete dayalı farklı bir component oluşturmak istediğinizde ortaya çıkar:

```js
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
  photo: PhotoStory,
  video: VideoStory
};

function Story(props) {
  // Yanlış! JSX türü bir obje olamaz.
  return <components[props.storyType] story={props.story} />;
}
```
Bunu düzeltmek için önce türü baş harfi büyük bir değişkene atayacağız:

```js
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
  photo: PhotoStory,
  video: VideoStory
};

function Story(props) {
  // Doğru! JSX türü baş harfi büyük yazılmış bir değişken olabilir.
  const SpecificStory = components[props.storyType];
  return <SpecificStory story={props.story} />;
}
```

<h2>JSX'te Propslar</h2>

Propsları JSX'de belirtmenin birkaç farklı yolu vardır.

<h3>JavaScript İfadeleri Olarak Props</h3>

Herhangi bir JavaScript ifadesini `{}` ile çevreleyerek yazabilirsiniz. Örneğin, bu JSX'de:

```js
<MyComponent foo={1 + 2 + 3 + 4} />
```

`MyComponent` için, `props.foo` değeri `1 + 2 + 3 + 4`  ifadesini hesaplar ve `10` olur.

`if` ifadelerini ve` for` döngülerini JSX'te doğrudan kullanamayız. Bunun yerine, bunları çevreleyen koda yerleştirebilirsiniz.

Örneğin:

```js
function NumberDescriber(props) {
  let description;
  if (props.number % 2 == 0) {
    description = <strong>even</strong>;
  } else {
    description = <i>odd</i>;
  }
  return <div>{props.number}, {description} sayıdır.</div>;
}
```

<a href="https://omergulcicek.github.io/reactjs/sartli-render">Şartlı render</a> ve <a href="https://omergulcicek.github.io/reactjs/listeler-ve-keyler">döngüler</a> hakkında ilgili bölümlerde daha fazla bilgi edinebilirsiniz.

<h3>String Literaller</h3>

Bir string ifadeyi props olarak geçirebilirsiniz. Bu iki JSX ifadesi aynıdır:

```js
<MyComponent message="Merhaba Dünya" />

<MyComponent message={'Merhaba Dünya'} />
```

Bir string gönderirken, değeri HTML-unescaped'dir. Dolayısıyla bu iki JSX ifadesi aynıdır:

```js
<MyComponent message="&lt;3" />

<MyComponent message={'<3'} />
```

<h3>Propslar Default Olarak True'dur</h3>

Değer girmezseniz, default (<i>varsayılan</i>) olarak propslar `true` olur. Bu iki JSX ifadesi aynıdır.

```js
<MyTextBox autocomplete />

<MyTextBox autocomplete={true} />
```

Genel olarak bunu kullanmanızı önermiyoruz çünkü `{foo: true}` yerine, `{foo: foo}` için kısa olan ES6 nesne kısayolu `{foo}` ile karıştırılabilir.

<h3>Spread Attributeler</h3>

Bir `props`unuz varsa ve bunu JSX'de geçirmek istiyorsanız, bütün props nesnesini geçmek için `...`yı spread bir operatör olarak kullanabilirsiniz. Bu iki component aynıdır:

```js
function App1() {
  return <Greeting firstName="Ömer" lastName="Gülçiçek" />;
}

function App2() {
  const props = {firstName: 'Ömer', lastName: 'Gülçiçek'};
  return <Greeting {...props} />;
}
```

Ayrıca, tüm propsları geçirirken componentinizin tüketeceği belirli propsu ayrı olarak seçebilirsiniz.

```js
const Button = props => {
  const { kind, ...other } = props;
  const className = kind === "primary" ? "PrimaryButton" : "SecondaryButton";
  return <button className={className} {...other} />;
};

const App = () => {
  return (
    <div>
      <Button kind="primary" onClick={() => console.log("Tıklandı!")}>
        Merhaba Dünya!
      </Button>
    </div>
  );
};
```

Yukarıdaki örnekte `kind` güvenli bir şekilde tüketilir ve DOM'da `<button>` elemanına geçirilmez.
Diğer tüm propslar, `...other` nesnesi aracılığıyla geçirilir ve bu component gerçekten esnek hale gelir. Bir `onClick` ve `children` propsundan geçtiğini görebilirsiniz.

Spread attributeleri kullanışlı olabilir, ancak gereksiz componentleri kendileri için önemsemeyen componentlere veya geçersiz HTML attributelerini DOM'a geçirmeyi kolaylaştırır. Bu syntaxı dikkatli kullanmanızı öneririz.

<h2>JSX'te Children</h2>

Hem bir açılış etiketi hem de bir kapanış etiketi içeren JSX ifadelerde, bu etiketler arasındaki içerik `props.children` olarak aktarılır. Childrenları geçmenin birkaç farklı yolu vardır:

<i>Bu konu ile ilgili olan <a href="https://omergulcicek.github.io/reactjs/composition-ve-inheritance">composition ve inheritance</a> konusunuda okuyabilirsiniz.</i>

<h3>String Literaller</h3>

Açılış ve kapanış etiketleri arasına bir string koyabiliriz, bu string `props.children` olacaktır. Örneğin:

```js
<MyComponent>Merhaba Dünya!</MyComponent>
```

Bu geçerli JSX'dir ve `MyComponent`deki `props.children`, basitçe "Merhaba Dünya!" stringi olacaktır.

JSX bir satırın başında ve sonunda olan boşlukları kaldırır. Boş satırları da kaldırır. Etiketlerin yanındaki yeni satırlar kaldırılır; string değişkenlerinin ortasında oluşan yeni satırlar tek bir alana yoğuşturulur. Yani aşağıdaki örneklerin hepsi aynı şeyi yapar:

```js
<div>Merhaba Dünya/div>

<div>
  Merhaba Dünya
</div>

<div>
  Merhaba
  Dünya
</div>

<div>

  Merhaba Dünya
</div>
```

<h3>JSX'te Children</h3>

İstediğiniz kadar componenti children (<i>çocuk</i>) olarak kullanabilirsiniz, iç içe geçmiş componentleri görüntülemek için kullanışlıdır:

```js
<MyContainer>
  <MyFirstComponent />
  <MySecondComponent />
</MyContainer>
```

Bir React componenti dizi return edebilir:

```js
render() {
  // Liste öğelerini fazladan bir element ile sarmanıza gerek yok!
  return [
    // Keyleri unutmayın
    <li key="A">First item</li>,
    <li key="B">Second item</li>,
    <li key="C">Third item</li>,
  ];
}
```

<i>Keyler hakkında detaylı bilgi için <a href="https://omergulcicek.github.io/reactjs/listeler-ve-keyler">listeler ve keyler</a> konusundan <b>keyler</b> başlığına bakabilirsiniz.</i>

<h3>Children JavaScript İfadeleri</h3>

JavaScript ifadesini childrena `{}`e koyarak geçirebilirsiniz. Örneğin, bu ifadeler aynıdır:

```js
<MyComponent>Örnek</MyComponent>

<MyComponent>{'Örnek'}</MyComponent>
```

Bu, keyfi uzunlukta JSX ifadelerinin bir listesini oluşturmak için genellikle yararlıdır. Örneğin, bu bir HTML listesi oluşturur:

```js
function Item(props) {
  return <li>{props.message}</li>;
}

function TodoList() {
  const todos = ['Ömer', 'Burak', 'Muhammed'];
  return (
    <ul>
      {todos.map((message) => <Item key={message} message={message} />)}
    </ul>
  );
}
```

JavaScript ifadeleri diğer children türleri ile birlikte kullanılabilir. Bu genellikle string şablonlarının yerine yararlıdır:

```js
function Hello(props) {
  return <div>Merhaba {props.addressee}!</div>;
}
```

<h3>Children Türünden Functions </h3>

Normalde, JSX'e eklenen JavaScript ifadeleri bir stringe, bir React elementi veya bu şeylerin bir listesine göre değerlendirilir. Bununla birlikte, `props.children`, yalnızca React'in nasıl yapılacağını bildiği türden değil, herhangi bir veri türünden geçebileceği için diğer herhangi bir `props` gibi çalışır. Örneğin, özel bir componente sahipseniz, bir callback'i `props.children` olarak almasını sağlayabilirsiniz:

```js
// Tekrarlanan bir component üretmek için childrenların callback'leri çağırır
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
    items.push(props.children(i));
  }
  return <div>{items}</div>;
}

function ListOfTenThings() {
  return (
    <Repeat numTimes={10}>
      {(index) => <div key={index}>Bu listede {index} olan öğedir.</div>}
    </Repeat>
  );
}
```

<h3>Booleans, Null ve Undefined Yok Sayılır</h3>

`false`, `null`, `undefined` ve `true` geçerli childrenlardır. Onlar sadece render yapılmazlar. Bu JSX ifadeleri hep aynı şeyi yapacak:

```js
<div />

<div></div>

<div>{false}</div>

<div>{null}</div>

<div>{undefined}</div>

<div>{true}</div>
```

Bu, koşullu olarak React elementlerini oluşturmak için yararlı olabilir. JSX yalnızca `showHeader` true ise `<Header />` componentini görür, false ise görmez:

```js
<div>
  {showHeader && <Header />}
  <Content />
</div>
```

Bir uyarı, '0' sayısı gibi bazı <b>falsy</b> değerleri React tarafından render edilir. Örneğin, bu kod, `props.messages` boş bir dizi olduğunda '0' yazdırılacağı için beklediğiniz gibi davranmayacaktır:

```js
<div>
  {props.messages.length &&
    <MessageList messages={props.messages} />
  }
</div>
```

<i>Falsy değeri, boolean bağlamında değerlendirildiğinde false değerine çeviren bir değerdir. JavaScript, if-else ve döngüler gibi herhangi bir değeri bir boolena gerektiren bağlamlarda zorlamak için tür tipi dönüştürme özelliğini kullanır.</i>

<i>JavaScript'teki false değerlerin örnekleri (false'a çevrilir ve böylece if bloğunu atlar):</i>

```js
if (false)
if (null)
if (undefined)
if (0)
if (NaN)
if ('')
if ("")
if (document.all) [1]
```

<i>Normalde `true && kod` olduğunda ilk ifade true olduğu için sağ kısımdaki kod çalışacaktır. `false && kod` olduğunda ise kod hiçbir çıktı vermeyecektir. JavaScript'te `1 && kod` olduğunda 1'i true olarak değerlendirip kodu çalıştırır fakat `0 && kod` olduğunda 0'ı false olarak değerlendirmez ve ekrana `0` yazar.</i>

Bunu düzeltmek için, `&&` önündeki ifadenin her zaman boolean olduğundan emin olun:

```js
<div>
  {props.messages.length > 0 &&
    <MessageList messages={props.messages} />
  }
</div>
```

Aksine, çıktıda `false`,` true`, `null` veya` undefined` gibi bir değerleri görmek istiyorsanız, önce bir string haline getirmeniz gerekir:

```js
<div>
  JavaScript değişkenim {String(myVariable)}.
</div>
```

<a href="https://omergulcicek.github.io/reactjs/gelismis-kilavuzlar/es6-olmadan-react">Sıradaki Gelişmiş Kılavuz: ES6 Olmadan React</a>
