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

We've learned that `useEffect` lets us express different kinds of side effects after a component renders. Some effects might require cleanup so they return a function:

```js
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```

Other effects might not have a cleanup phase, and don't return anything.

```js
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
```

The Effect Hook unifies both use cases with a single API.

-------------

**If you feel like you have a decent grasp on how the Effect Hook works, or if you feel overwhelmed, you can jump to the [next page about Rules of Hooks](/docs/hooks-rules.html) now.**

-------------

## Tips for Using Effects

We'll continue this page with an in-depth look at some aspects of `useEffect` that experienced React users will likely be curious about. Don't feel obligated to dig into them now. You can always come back to this page to learn more details about the Effect Hook.

### Tip: Use Multiple Effects to Separate Concerns

One of the problems we outlined in the [Motivation](/docs/hooks-intro.html#complex-components-become-hard-to-understand) for Hooks is that class lifecycle methods often contain unrelated logic, but related logic gets broken up into several methods. Here is a component that combines the counter and the friend status indicator logic from the previous examples:

```js
class FriendStatusWithCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0, isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
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

Note how the logic that sets `document.title` is split between `componentDidMount` and `componentDidUpdate`. The subscription logic is also spread between `componentDidMount` and `componentWillUnmount`. And `componentDidMount` contains code for both tasks.

So, how can Hooks solve this problem? Just like [you can use the *State* Hook more than once](/docs/hooks-state.html#tip-using-multiple-state-variables), you can also use several effects. This lets us separate unrelated logic into different effects:

```js{3,8}
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
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

**Hooks lets us split the code based on what it is doing** rather than a lifecycle method name. React will apply *every* effect used by the component, in the order they were specified.

### Explanation: Why Effects Run on Each Update

If you're used to classes, you might be wondering why the effect cleanup phase happens after every re-render, and not just once during unmounting. Let's look at a practical example to see why this design helps us create components with fewer bugs.

[Earlier on this page](#example-using-classes-1), we introduced an example `FriendStatus` component that displays whether a friend is online or not. Our class reads `friend.id` from `this.props`, subscribes to the friend status after the component mounts, and unsubscribes during unmounting:

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

**But what happens if the `friend` prop changes** while the component is on the screen? Our component would continue displaying the online status of a different friend. This is a bug. We would also cause a memory leak or crash when unmounting since the unsubscribe call would use the wrong friend ID.

In a class component, we would need to add `componentDidUpdate` to handle this case:

```js{8-19}
  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate(prevProps) {
    // Unsubscribe from the previous friend.id
    ChatAPI.unsubscribeFromFriendStatus(
      prevProps.friend.id,
      this.handleStatusChange
    );
    // Subscribe to the next friend.id
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

Forgetting to handle `componentDidUpdate` properly is a common source of bugs in React applications.

Now consider the version of this component that uses Hooks:

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

It doesn't suffer from this bug. (But we also didn't make any changes to it.)

There is no special code for handling updates because `useEffect` handles them *by default*. It cleans up the previous effects before applying the next effects. To illustrate this, here is a sequence of subscribe and unsubscribe calls that this component could produce over time:

```js
// Mount with { friend: { id: 100 } } props
ChatAPI.subscribeToFriendStatus(100, handleStatusChange);     // Run first effect

// Update with { friend: { id: 200 } } props
ChatAPI.unsubscribeFromFriendStatus(100, handleStatusChange); // Clean up previous effect
ChatAPI.subscribeToFriendStatus(200, handleStatusChange);     // Run next effect

// Update with { friend: { id: 300 } } props
ChatAPI.unsubscribeFromFriendStatus(200, handleStatusChange); // Clean up previous effect
ChatAPI.subscribeToFriendStatus(300, handleStatusChange);     // Run next effect

// Unmount
ChatAPI.unsubscribeFromFriendStatus(300, handleStatusChange); // Clean up last effect
```

This behavior ensures consistency by default and prevents bugs that are common in class components due to missing update logic.

### Tip: Optimizing Performance by Skipping Effects

In some cases, cleaning up or applying the effect after every render might create a performance problem. In class components, we can solve this by writing an extra comparison with `prevProps` or `prevState` inside `componentDidUpdate`:

```js
componentDidUpdate(prevProps, prevState) {
  if (prevState.count !== this.state.count) {
    document.title = `You clicked ${this.state.count} times`;
  }
}
```

This requirement is common enough that it is built into the `useEffect` Hook API. You can tell React to *skip* applying an effect if certain values haven't changed between re-renders. To do so, pass an array as an optional second argument to `useEffect`:

```js{3}
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```

In the example above, we pass `[count]` as the second argument. What does this mean? If the `count` is `5`, and then our component re-renders with `count` still equal to `5`, React will compare `[5]` from the previous render and `[5]` from the next render. Because all items in the array are the same (`5 === 5`), React would skip the effect. That's our optimization.

When we render with `count` updated to `6`, React will compare the items in the `[5]` array from the previous render to items in the `[6]` array from the next render. This time, React will re-apply the effect because `5 !== 6`. If there are multiple items in the array, React will re-run the effect even if just one of them is different.

This also works for effects that have a cleanup phase:

```js{6}
useEffect(() => {
  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
}, [props.friend.id]); // Only re-subscribe if props.friend.id changes
```

In the future, the second argument might get added automatically by a build-time transformation.

>Note
>
>If you use this optimization, make sure the array includes **any values from the outer scope that change over time and that are used by the effect**. Otherwise, your code will reference stale values from previous renders. We'll also discuss other optimization options in the [Hooks API reference](/docs/hooks-reference.html).
>
>If you want to run an effect and clean it up only once (on mount and unmount), you can pass an empty array (`[]`) as a second argument. This tells React that your effect doesn't depend on *any* values from props or state, so it never needs to re-run. This isn't handled as a special case -- it follows directly from how the inputs array always works. While passing `[]` is closer to the familiar `componentDidMount` and `componentWillUnmount` mental model, we suggest not making it a habit because it often leads to bugs, [as discussed above](#explanation-why-effects-run-on-each-update). Don't forget that React defers running `useEffect` until after the browser has painted, so doing extra work is less of a problem.

## Next Steps

Congratulations! This was a long page, but hopefully by the end most of your questions about effects were answered. You've learned both the State Hook and the Effect Hook, and there is a *lot* you can do with both of them combined. They cover most of the use cases for classes -- and where they don't, you might find the [additional Hooks](/docs/hooks-reference.html) helpful.

We're also starting to see how Hooks solve problems outlined in [Motivation](/docs/hooks-intro.html#motivation). We've seen how effect cleanup avoids duplication in `componentDidUpdate` and `componentWillUnmount`, brings related code closer together, and helps us avoid bugs. We've also seen how we can separate effects by their purpose, which is something we couldn't do in classes at all.

At this point you might be questioning how Hooks work. How can React know which `useState` call corresponds to which state variable between re-renders? How does React "match up" previous and next effects on every update? **On the next page we will learn about the [Rules of Hooks](/docs/hooks-rules.html) -- they're essential to making Hooks work.**


<i>Gelişmiş kılavuzlar sonlanmıştır. Bu aşamadan sonra <b>Uygulamalı Eğitime</b> geçiş yapılacaktır.</i>

<a href="https://omergulcicek.github.io/react/uygulamali-egitim/xox-oyunu">Sıradaki Eğitim: XOX Oyunu</a>
