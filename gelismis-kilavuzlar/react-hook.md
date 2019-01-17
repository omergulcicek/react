# React Hook

Hooklar, bir class yazmadan state ve diğer React özelliklerini kullanmanıza izin veren yeni bir özellik önerisidir. Şu anda React v16.7.0-alpha'da ve [açık bir RFC](https://github.com/reactjs/rfcs/pull/68)'de tartışılıyor.

```js
import { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // componentDidMount ve componentDidUpdate'e benzer:
  useEffect(() => {
    // Sayfa başlığını günceller.
    document.title = `${count} kere tıkladınız`;
  });

  return (
    <div>
      <p>{count} kere tıkladınız.</p>
      <button onClick={() => setCount(count + 1)}>
        Tıkla
      </button>
    </div>
  );
}
```

Verilerin getirilmesi, bir abonelik oluşturulması ve React componentlerinde DOM'un manuel olarak değiştirilmesi, tüm yan efektlere örnektir.

>İpucu
>
> React class lifecyle fonksiyonlarına aşina iseniz, `useEffect` fonksiyonunu `componentDidMount`, `componentDidUpdate` ve `componentWillUnmount` birleşimi olarak düşünebilirsiniz.
>
> `useEffect` = `componentDidMount` + `componentDidUpdate` + `componentWillUnmount`

[Lifecyle Fonksiyonları hakkında detaylı bilgi için tıklayınız.](https://omergulcicek.github.io/react/gelismis-kilavuzlar/lifecycle-fonksiyonlari)

## Temizleme Yapmadan Efektler

Bazen, React DOM'u güncelledikten sonra bazı kodlar çalıştırmak isteriz. Network istekleri, manuel DOM mutasyonları ve log kaydı, temizleme gerektirmeyen efektlere genel örneklerdir. Bunu söylüyoruz çünkü onları çalıştırabilir ve hemen onları unutabiliriz. Classların ve Hooks'un bu gibi yan efektleri nasıl ifade edeceğimizi karşılaştıralım.

### Classları Kullanan Örnek

React class componentlerinde, `render` fonksiyonunun kendisi yan efektlere neden olmamalıdır. Çok erken olurdu - genellikle efektleri React DOM'u güncelledikten sonra gerçekleşmesini istiyoruz.

Bu nedenle, React classlarında, `componentDidMount` ve `componentDidUpdate` componentlerine yan etkiler koyarız. Örneğimize geri dönersek, burada React, DOM'da değişiklikler yaptıktan hemen sonra belge başlığını güncelleyen bir sayaç class componentidir:

```js
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  componentDidMount() {
    document.title = `${this.state.count} kere tıkladınız`;
  }

  componentDidUpdate() {
    document.title = `${this.state.count} kere tıkladınız`;
  }

  render() {
    return (
      <div>
        <p>${this.state.count} kere tıkladınız.</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Tıkla
        </button>
      </div>
    );
  }
}
```

Classlardaki bu iki lifecyle fonksiyonu arasında gördüğünüz gibi aynı kodu kopyaladık.

Bunun nedeni, birçok durumda componentlerin yeni render edilmiş olup olmadığına veya güncellenip güncellenmediğine bakılmaksızın, aynı yan efekti gerçekleştirmek istiyoruz. Kavramsal olarak, her renderdan sonra olmasını isteriz - ancak React class componentlerin böyle bir fonksiyonu yoktur. Ayrı bir fonksiyon yazabilirdik ama yine de iki lifecyle fonksiyonunda bu oluşturduğumuz fonksiyonu çağırmak zorundayız.

Şimdi `useEffect` hook ile aynın şeyi nasıl yapacağımıza bakalım.

### Hook Kullanımına Örnek

Bu örneği zaten üstte gördük fakat tekrar yakından bakalım:

```js
import { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `${count} kere tıkladınız`;
  });

  return (
    <div>
      <p>{count} kere tıkladınız.</p>
      <button onClick={() => setCount(count + 1)}>
        Tıkla
      </button>
    </div>
  );
}
```

**`useEffect` ne yapar?** Bu hook'u kullanarak, componentin render edildikten sonra bir şeyler yapması gerektiğini React'a söylemiş olursunuz. React, bu fonksiyonu hatırlayacaktır (buna "effect" diyeceğiz) ve DOM güncellemelerini gerçekleştirdikten sonra bu effect'te sayfa title'ını belirledik, ancak veri getirmeyi veya başka bir API'ye çağrı yapabiliriz.

**Neden `useEffect`  bir componentin içerisinde çağrılır?** Componentin içine `useEffect` yerleştirmek, effectten `count` state değişkenine (veya herhangi bir propsa) erişmemize izin verir. Okumak için özel bir API'ye ihtiyacımız yok (çünkü zaten fonksiyon scope kapsamında). Hooklar, JavaScript kapanışlarını benimserler ve JavaScript'in zaten çözüm sağladığı React-Specifis API'lerini tanıtmaktan kaçınırlar.

**`useEffect` her renderdan sonra çalışır mı** Evet! Varsayılan olarak her güncellemeden sonra ilk render ve sonrasında da çalışır (daha sonradan bunu nasıl özelleştireceğimizi konuşacağız). Mounting ve updating terimleriyle düşünmek yerine, bunu düşünmek daha kolay olabilir. Effectler render edildikten sonra olur. React, DOM'un etkileri çalıştırdığı zaman güncellenediğini garanti eder.

### Detaylı Açıklama

Artık effectler hakkında daha fazla bilgi sahibi olduğumuza göre, bu kodlar mantıklı olmalı:

```js
function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `${count} kere tıkladınız.`;
  });
```

`count` state değişkenini alırız ve sonra React'a bir effect kullanmamız gerektiğini söyleriz. `useEffect` hookuna bir fonksiyon iletiyoruz (`setCount`); bu fonksiyon bizim effectimizdir. Effectimizin içine sayfa title'ını `document.title` tarayıcı API'sini kullanarak değiştirdik. Effectin içinde en son `count`u okuyabiliriz çünkü bu bizim fonksiyon scope'undadır. React, componentimizi oluşturduğunda, kullandığımız effecti hatırlar ve DOM'u güncelledikten sonra effectimizi çalıştırır. Bu ilk render dahil olmak üzere her render için geçerlidir.

Deneyimli JavaScript geliştiricileri, `useEffect` fonksiyonuna iletilen fonksiyonun her renderdan sonra farklı olacağını fark edebilir, bu kasıtlıdır. Aslında bu, `count` değerini effectin içinden okumamızı sağlar. Her yeniden render edildiğinde bir öncekinin yerine farklı bir effecti programlıyoruz. Bir bakıma bu, effectlerin render sonucunun bir parçası gibi davrandığını gösterir. Bunun neden yararlı olduğunu daha sonra göreceğiz.

>İpucu
>
>`componentDidMount` veya `componentDidUpdate` fonksiyonlarının aksine `useEffect` ile planlanan effectler, tarayıcıyı ekranın güncellemesini engellemez. Bu uygulamanızı daha duyarlı hissettirir. Effectlerin çoğunun senkronie olmasına gerek yoktur. Yaptıkları nadir durumlarda (layout'un ölçülmesi gibi) `useEffect` ile aynı API'ye sahip ayrı bir `useLayoutEffect` vardır.

## Temizleme ile Efektler

Daha önce, temizleme gerektirmeyen yan etkilerin nasıl oluşturulduğunu inceledik. **bazı hari veri kaynaklarına bir abonelik ayarlamak isteyebiliriz.** Bu durumda, bellek sızıntısına neden olmamak için temizlik yapılması önemlidir. Bunu sınıflarla ve hook ile yapabileceğimi inceleyelim.

### Sınıfları Kullanarak Örnek

React sınıflarında, `ComponentDidMount` içinde bir abonelik kurarsanız, bunu `ComponentWillUnmount` içinde temizlersiniz. Örneğin, bir arkadaşının çevrimiçi durumuna abone olmamızı sağlayan bir `ChatAPI` modülümüz olduğunu varsayalım. Bir sınıf kullanarak nasıl yazabileceğini aşağıda bulabilirsiniz.

```js
class FriendStatus extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }

  render() {
    if (this.state.isOnline === null) {
      return 'Loading...';
    }
    return this.state.isOnline ? 'Online' : 'Offline';
  }
}
```

`componentDidMount` ve `componentWillunmount` birbirlerini yansıtmaları gerektiğine dikkat edin. Lifecyle fonskiyonları, ikisininde kavramsal olarak aynı etkiyle ilişki olmasına rağmen, bunu iki kere yazmamızı sağlar.

>Not
>
>Eagle-eyed okuyucular, bu örneğin tamamen doğru olması için bir `componentDidUpdate` fonksiyonuna ihtiyaç duyduklarını fark edebilirler. Şimdilik bunu görmezden geleceğiz (sonradan bahsedilecek).

### Hooks Kullanarak Örnek

Aynı bileşeni Hooks ile nasıl yazabileceğimize bir bakalım.

Temizliği gerçekleştirmek için ayrı bir efekte ihtiyacımız olacağını düşünüyor olabilirsiniz. Ancak bir abonelik ekleme ve kaldırma kodu, o kadar sıkı bir şekilde ilişkilidir ki `useEffect` onu bir arada tutmak için tasarlanmıştır. Efektiniz bir fonksiyon return ederse, temizleme zamanı geldiğinde React onu çalıştıracaktır.

```js
import { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // Bu kısımda nasıl temizleneceğini belirtin:
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

**Neden efektimizden bir fonskiyon return ettik?** Bu, efektler için isteğe bağlı temizleme mekanizmasıdır. Her efekt, ondan sonra temizleyen bir fonksiyon return edebilir. Bu, abonelik ekleme ve kaldırma mantığını korumamızı sağlar. Onlar aynı efektin bir parçası!

**React tam olarak ne zaman bir efekte neden oluyor?** React, component unmounts olduğunda React temizleme işlemini gerçekleştiriyor. Ancak, daha önce öğrendiğimiz gibi efektler sadece bir kez değil, her render için çalışır. Bu yüzden React *ayrıca* efektleri bir dahaki sefere çalıştırmadan önce önceki renderdeki efektleri temizler. Bunun neden hatalardan kaçınmaya yardımcı olduğunu ve daha sonra performans sorunları yaratması durumunda bu davranıştan nasıl vazgeçileceğini ilerleyen kısımlarda göreceğiz.

>Not
>
>İsimlendirilmiş bir fonksiyonu efekkten döndürmek zorunda değiliz. Amacını netleştirmek için buraya `cleanup` diyoruz, ancak bir arrow fonksiyonu return edebilir veya farklı bir şey diyebilirsiniz.

## Recap

`useEffect` öğresinin bir component render edildikten sonra yan efektleri ifade etmemize izin verdiğini öğrendik. Bazı efektler temizleme gerektirebilir, bu nedenli bir fonksiyon return ederler:

```js
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```

Diğer efektler temizleme aşamasına sahip olmayabilir ve hiçbir şey return etmezler.

```js
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
```

Efekt Hook, her iki kullanım durumunu da tek bir API ile birleştirir.

-------------

## Efektleri Kullanma İpuçları

Bu kısımda, deneyimli React kullanıcılarının muhtemelen merak edeceği `useEffect`in bazı yönlerine derinlemesine bakacağız.

### İpucu: Endişeleri Ayırmak İçin Birden Çok Efekt Kullanma

One of the problems we outlined in the Motivation for Hooks is that class lifecycle methods often contain unrelated logic, but related logic gets broken up into several methods. Here is a component that combines the counter and the friend status indicator logic from the previous examples:

Hooks motivasyonunda ana hatlarıyla anlattığımız sorunlardan biri, class lifecycle fonksiyonlarının çoğu zaman ilgisiz bir mantık içermesi, ancak ilgili mantığın çeşitli yöntemlere bölünmesidir. Sayaç ile arkadaş durumu gösterge mantığını önceki örneklerden birleştiren bir component:

```js
class FriendStatusWithCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0, isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    document.title = `${this.state.count} kez tıkladın`;
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate() {
    document.title = `${this.state.count} kez tıkladın`;
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }
  // ...
```

Yukarıda görüldüğü gibi, aynı kodlar gereksiz yere tekrar etmiştir.

Peki, Hook bu sorunu nasıl çözebilir? *State* hook'u bir kereden fazla kullanabildiğiniz gibi, çeşitli efektler de kullanabilirsiniz. Bu, ilgisiz mantığı farklı efektlere ayırmamızı sağlar:

```js
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `${this.state.count} kez tıkladın`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }
  // ...
}
```

**Hook, lifecycke fonksiyon isimlerinden ziyade**, yaptıklarına göre kodu bölmemize olanak sağlar. React, component tarafından kullanılan *her* efekti, belirtilen sırada uygular.

### Açıklama: Neden Her Güncellemede Efektler Çalışıyor?

Classlara alışkınsanız, efekt temizleme aşamasının neden her bir render işleminden sonra gerçekleştiğini değil, unmounting işlemi sırasında yalnızca bir kez olduğunu merak ediyor olabilirsiniz. Bu tasarımın neden daha az hata içeren component oluşturmamıza yardımcı olduğunu görmek için pratik bir örneğe bakalım.

Bu sayfada daha önce bir arkadaşın çevrimiçi olup olmadığını gösteren bir `FriendStatus` componenti yazıldı. Sınıfımız, `this.props` `friend.id` okur, component mounts edildikten sonra arkadaş durumuna abone olur ve unmounting işlemi sırasında aboneliği kaldırır:

```js
  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
```

Ancak, component ekranda iken **`friend` propsu değişirse ne olur?** Componentimiz, farklı bir arkadaşın çevrimiçi durumunu göstermeye devam edecek. Bu bir hatadır. Abonelikten çıkma çağrısının yanlış arkadaş kimliğini kullanması nedeniyle bağlantıyı keserken de bellek sızıntısına veya çökmesine neden oluruz.

Bir class componentinde, bu durumu ele almak için `componentDidUpdate` eklememiz gerekir:

```js
  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate(prevProps) {
    // Önceki friend.id aboneliğinden çık
    ChatAPI.unsubscribeFromFriendStatus(
      prevProps.friend.id,
      this.handleStatusChange
    );
    // Sonraki friend.id aboneliğini başlat
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
```

`ComponentDidUpdate` kodunu doğru bir şekilde işlemeyi unutmak, React uygulamalarındaki yaygın bir hata kaynağıdır.

Şimdi bu componenti Hooks kullanan sürümünü düşünün:

```js
function FriendStatus(props) {
  // ...
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```

Bu bug muzdarip değil. (Ama aynı zamanda hiçbir değişiklik yapmadık.)

Güncelleştirmeler için özel bir kod yoktur çünkü `useEffect` bunları *varsayılan olarak* kullanır. Bir sonraki efektleri uygulamadan önce önceki efektleri temizler. Bunu göstermek için, işte bu componenti zaman içinde üretebileceği abone olma ve abonelikten çıkma çağrıları dizisini inceleyelim:

```js
// { friend: { id: 100 } } propsu ile mount
ChatAPI.subscribeToFriendStatus(100, handleStatusChange);     // İlk efekt çalışır

// { friend: { id: 200 } } propsu ile güncelleme
ChatAPI.unsubscribeFromFriendStatus(100, handleStatusChange); // Önceki efekt temizlenir
ChatAPI.subscribeToFriendStatus(200, handleStatusChange);     // Sonraki efekti çalıştır

// { friend: { id: 300 } } propsu ile güncelleme
ChatAPI.unsubscribeFromFriendStatus(200, handleStatusChange); // Önceki efekt temizlenir
ChatAPI.subscribeToFriendStatus(300, handleStatusChange);     // Sonraki efekti çalıştır

// Unmount
ChatAPI.unsubscribeFromFriendStatus(300, handleStatusChange); // Son efekti temizle
```

Bu davranış varsayılan olarak tutarlılığı sağlar ve eksik güncelleme mantığı nedeniyle class componentlerinde yaygın olan hataları önler.

### İpucu: Efektleri Atlayarak Performansı İyileştirme

Bazı durumlarda her render işleminden sonra efekti temizlemek veya uygulamak performans sorunu oluşturabilir. Class componentlerinde bunu `componenetDidUpdate` içinde `prevProps` veya `prevState` ile fazladan bir karşılaştırma yaparak çözebiliriz:

```js
componentDidUpdate(prevProps, prevState) {
  if (prevState.count !== this.state.count) {
    document.title = `${this.state.count} kez tıkladın`;
  }
}
```

Bu gereksinim, `useEffect` Hook API'sine yerleşik olması için yeterince yaygındır. Yeni renderlar arasında belirli değerler değişmemişse React'a *atla (skip)* komutunu verebilirsiniz. Bunu yapmak için bir arrayi `useEffect` seçeneğine isteğe bağlı ikinci bir argüman olarak iletin:

```js{3}
useEffect(() => {
  document.title = `${count} kez tıkladın`;
}, [count]); // Yalnızca sayı değiştiğinde efekti yeniden çalıştır
```

Yukarıdaki örnekte, ikinci argüman olarak `[count]` yazıyoruz. Bu ne anlama geliyor? Eğer `count` hala 5'e eşit olan `count` ile yeniden renderlanırsa, React önceki renderdan `[5]` ve bir sonraki `[5]`'i karşılaştırır. Arraydeki tüm elemanlar aynı olduğundan (`5 === 5`) React efekti atlar. Böylece performansa olumlu etki etmiş oluruz.

`count` 6 ile güncellendiğinde, React değişimi farkedecek (`5 !== 6`). Arrayde birden fazla öğe varsa, React biri farklı olsa bile efekti yeniden render eder.

Bu ayrıca temizleme aşaması olan efektler içinde çalışır:

```js{6}
useEffect(() => {
  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
}, [props.friend.id]); // Yalnızca props.friend.id değişirse yeniden abone ol
```

Gelecekte, ikinci argüman otomatik olarak eklenebilir.

<i>Gelişmiş kılavuzlar sonlanmıştır. Bu aşamadan sonra <b>Uygulamalı Eğitime</b> geçiş yapılacaktır.</i>

<a href="https://omergulcicek.github.io/react/uygulamali-egitim/xox-oyunu">Sıradaki Eğitim: XOX Oyunu</a>
