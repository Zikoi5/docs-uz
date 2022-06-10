# "Event" yoki Hodisalar bilan ishlash

<div class="options-api">
  <VueSchoolLink href="https://vueschool.io/lessons/user-events-in-vue-3" title="Free Vue.js Events Lesson"/>
</div>

<div class="composition-api">
  <VueSchoolLink href="https://vueschool.io/lessons/vue-fundamentals-capi-user-events-in-vue-3" title="Free Vue.js Events Lesson"/>
</div>

## "Event"larni "eshitish"

"Event"larni "eshitish" deganda biz "event"ni har safar yangi natija kelishi bilan uni olib biron amal qilishni nazarda tutamiz.

:::tip Atama
**Event** bu hodisa. Misol uchun sichqoncha bilan rasmga o'ng tugmasini bosganiz bu bir hodisa, chap tugma bu boshqa.

Ushbu holatda javascript bizga "a" elementda "b" hodisa sodir bo'ldi deb "c" funksiyaga "d" obyekt jo'natadi.

Bizning misolda "a" bu rasm, "b" bu chap tugma bosilganligi haqida, "c" funksiyaga "d" [`MouseEvent`](https://developer.mozilla.org/ru/docs/Web/API/MouseEvent) obyekti ni uzatadi. `MouseEvent` obyektda qaysi elementga bosganimiz, sichqonchaning bosilgan vaqtdagi kordinatlari va h.k. ma'lumotlar saqlanadi.
:::

Biz `v-on` direktivani ishlatishimiz mumkin. Ko'pincha bu `@` belgisi bilan boshlanadi. Ushbu direktiva bizga, tepada aytib o'tilganidek "a" elementda "b" hodisa uchraganda qaysi "c" funksiyani chaqirishini belgilaydi. Misol uchun `v-on:click="handler"` yoki qisqa qilib yozganda `@click="handler"`.

Quyidagi misolda `click` bu "b" hodisa, `handler` esa "c" funksiyadir.

`handler` yoki "c" funksiya o'rniga biz to'g'ridan to'g'ri javascript ifodasini berishimiz mumkin.

"c" funksiyani, aytib o'tganimizdek 2 hil turi mavjud:

1. **Inline handler**, yoki javascript ifoda

2. **Method handler**, yoki usul, funksiya orqali

## "Inline Handlers" yoki javascript ifodalar

**Inline handler**lar odatda oddiy holatda ishlatiladi, misol uchun:

<div class="composition-api">

```js
const count = ref(0)
```

</div>
<div class="options-api">

```js
data() {
  return {
    count: 0
  }
}
```

</div>

```vue-html
<button @click="count++">1 qo'shish</button>
<p>Tugma {{ count }} marotada bosildi</p>
```

<div class="composition-api">

[Tekshirib ko'rish](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdD5cbmV4cG9ydCBkZWZhdWx0IHtcbiAgZGF0YSgpIHtcblx0ICByZXR1cm4ge1xuICAgIFx0Y291bnQ6IDBcbiAgXHR9XG5cdH1cbn1cbjwvc2NyaXB0PlxuXG48dGVtcGxhdGU+XG5cdDxidXR0b24gQGNsaWNrPVwiY291bnQrK1wiPjEgcW8nc2hpc2g8L2J1dHRvbj5cbiAgPHA+VHVnbWEge3sgY291bnQgfX0gbWFyb3RhZGEgYm9zaWxkaTwvcD5cbjwvdGVtcGxhdGU+IiwiaW1wb3J0LW1hcC5qc29uIjoie1xuICBcImltcG9ydHNcIjoge1xuICAgIFwidnVlXCI6IFwiaHR0cHM6Ly9zZmMudnVlanMub3JnL3Z1ZS5ydW50aW1lLmVzbS1icm93c2VyLmpzXCIsXG4gICAgXCJ2dWUvc2VydmVyLXJlbmRlcmVyXCI6IFwiaHR0cHM6Ly9zZmMudnVlanMub3JnL3NlcnZlci1yZW5kZXJlci5lc20tYnJvd3Nlci5qc1wiXG4gIH1cbn0ifQ==)

</div>
<div class="options-api">

[Tekshirib ko'rish](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdD5cbmltcG9ydCB7IHJlZiB9IGZyb20gJ3Z1ZSdcblxuZXhwb3J0IGRlZmF1bHQge1xuICBzZXR1cCgpIHtcbiAgICBjb25zdCBjb3VudCA9IHJlZigwKVxuICAgIFxuICAgIHJldHVybiB7IGNvdW50IH1cbiAgfVxufVxuPC9zY3JpcHQ+XG5cbjx0ZW1wbGF0ZT5cblx0PGJ1dHRvbiBAY2xpY2s9XCJjb3VudCsrXCI+MSBxbydzaGlzaDwvYnV0dG9uPlxuICA8cD5UdWdtYSB7eyBjb3VudCB9fSBtYXJvdGFkYSBib3NpbGRpPC9wPlxuPC90ZW1wbGF0ZT4iLCJpbXBvcnQtbWFwLmpzb24iOiJ7XG4gIFwiaW1wb3J0c1wiOiB7XG4gICAgXCJ2dWVcIjogXCJodHRwczovL3NmYy52dWVqcy5vcmcvdnVlLnJ1bnRpbWUuZXNtLWJyb3dzZXIuanNcIixcbiAgICBcInZ1ZS9zZXJ2ZXItcmVuZGVyZXJcIjogXCJodHRwczovL3NmYy52dWVqcy5vcmcvc2VydmVyLXJlbmRlcmVyLmVzbS1icm93c2VyLmpzXCJcbiAgfVxufSJ9)

</div>

## "Method Handlers" yoki usul, funksiyalar

Ilova logikasi qiyinroq bo'lgan holatda, "Inline handler" orqali yozishimiz qiyin bo'lishi mumkin. Shuning uchun oddiy va qisqa javascript ifoda o'rniga usul yoki funksiya nomini yozishimiz mumkin.

Misol uchun:

<div class="composition-api">

```js
const name = ref('Vue.js')

// `greet` bu yuqorida aytib o'tganimizdek "c" funksiya hisoblanadi
function greet(event) {
  alert(`Salom ${name.value}!`)
  // `event` bu yuqorida aytib o'tganimizdek "d" obyekt hisoblanadi
  if (event) {
    alert(event.target.tagName)
  }
}
```

</div>
<div class="options-api">

```js
data() {
  return {
    name: 'Vue.js'
  }
},
methods: {
  // `greet` bu yuqorida aytib o'tganimizdek "c" funksiya hisoblanadi
  greet(event) {
    // `this` bu quyidagi `Vue component` ga yo'naltiruvchi hisoblanadi
    alert(`Salom ${this.name}!`)
    // `event` bu yuqorida aytib o'tganimizdek "d" obyekt hisoblanadi
    if (event) {
      alert(event.target.tagName)
    }
  }
}
```

</div>

```vue-html
<!-- `greet` bu yuqorida belgilagan usul, funksiyamiz -->
<button @click="greet">Salom!</button>
```

<div class="composition-api">

[Tekshirib ko'rish](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdCBzZXR1cD5cbmltcG9ydCB7IHJlZiB9IGZyb20gJ3Z1ZSdcblxuY29uc3QgbmFtZSA9IHJlZignVnVlLmpzJylcblxuLy8gYGdyZWV0YCBidSB5dXFvcmlkYSBheXRpYiBvJ3RnYW5pbWl6ZGVrIFwiY1wiIGZ1bmtzaXlhIGhpc29ibGFuYWRpXG5mdW5jdGlvbiBncmVldChldmVudCkge1xuICBhbGVydChgU2Fsb20gJHtuYW1lLnZhbHVlfSFgKVxuICAvLyBgZXZlbnRgIGJ1IHl1cW9yaWRhIGF5dGliIG8ndGdhbmltaXpkZWsgXCJkXCIgb2J5ZWt0IGhpc29ibGFuYWRpXG4gIGlmIChldmVudCkge1xuICAgIGFsZXJ0KGV2ZW50LnRhcmdldC50YWdOYW1lKVxuICB9XG59XG48L3NjcmlwdD5cblxuPHRlbXBsYXRlPlxuXHQ8YnV0dG9uIEBjbGljaz1cImdyZWV0XCI+U2Fsb20hPC9idXR0b24+XG48L3RlbXBsYXRlPiIsImltcG9ydC1tYXAuanNvbiI6IntcbiAgXCJpbXBvcnRzXCI6IHtcbiAgICBcInZ1ZVwiOiBcImh0dHBzOi8vc2ZjLnZ1ZWpzLm9yZy92dWUucnVudGltZS5lc20tYnJvd3Nlci5qc1wiLFxuICAgIFwidnVlL3NlcnZlci1yZW5kZXJlclwiOiBcImh0dHBzOi8vc2ZjLnZ1ZWpzLm9yZy9zZXJ2ZXItcmVuZGVyZXIuZXNtLWJyb3dzZXIuanNcIlxuICB9XG59In0=)

</div>
<div class="options-api">

[Tekshirib ko'rish](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdD5cbmV4cG9ydCBkZWZhdWx0IHtcbiAgZGF0YSgpIHtcbiAgICByZXR1cm4ge1xuICAgICAgbmFtZTogJ1Z1ZS5qcydcbiAgICB9XG4gIH0sXG4gIG1ldGhvZHM6IHtcbiAgICAvLyBgZ3JlZXRgIGJ1IHl1cW9yaWRhIGF5dGliIG8ndGdhbmltaXpkZWsgXCJjXCIgZnVua3NpeWEgaGlzb2JsYW5hZGlcbiAgICBncmVldChldmVudCkge1xuICAgICAgLy8gYHRoaXNgIGJ1IHF1eWlkYWdpIGBWdWUgY29tcG9uZW50YCBnYSB5byduYWx0aXJ1dmNoaSBoaXNvYmxhbmFkaVxuICAgICAgYWxlcnQoYFNhbG9tICR7dGhpcy5uYW1lfSFgKVxuICAgICAgLy8gYGV2ZW50YCBidSB5dXFvcmlkYSBheXRpYiBvJ3RnYW5pbWl6ZGVrIFwiZFwiIG9ieWVrdCBoaXNvYmxhbmFkaVxuICAgICAgaWYgKGV2ZW50KSB7XG4gICAgICAgIGFsZXJ0KGV2ZW50LnRhcmdldC50YWdOYW1lKVxuICAgICAgfVxuICAgIH1cbiAgfVxufVxuPC9zY3JpcHQ+XG5cbjx0ZW1wbGF0ZT5cblx0PGJ1dHRvbiBAY2xpY2s9XCJncmVldFwiPlNhbG9tITwvYnV0dG9uPlxuPC90ZW1wbGF0ZT4iLCJpbXBvcnQtbWFwLmpzb24iOiJ7XG4gIFwiaW1wb3J0c1wiOiB7XG4gICAgXCJ2dWVcIjogXCJodHRwczovL3NmYy52dWVqcy5vcmcvdnVlLnJ1bnRpbWUuZXNtLWJyb3dzZXIuanNcIixcbiAgICBcInZ1ZS9zZXJ2ZXItcmVuZGVyZXJcIjogXCJodHRwczovL3NmYy52dWVqcy5vcmcvc2VydmVyLXJlbmRlcmVyLmVzbS1icm93c2VyLmpzXCJcbiAgfVxufSJ9)

</div>

Yuqorida ko'rsatilgan misolda `click` "b" hodisani Vue avtomatik tarzda mavjud hodisalar ro'yxatidan tekshirib "eshitishni" boshlaydi.

Undan tashqari misolda ko'rsatilgan funksiyaga aytib o'tganimizdek "d" obyekt avtomatik tarzda uzatiladi, va ushbu "d" obyekt orqali biz "a" elementni **teg**'ini `event.target.tagName` orqali ko'rishimiz mumkin.

<div class="composition-api">

Yanada batafsilroq: [Typing Event Handlers](/guide/typescript/composition-api.html#typing-event-handlers) <sup class="vt-badge ts" />

</div>
<div class="options-api">

Yanada batafsilroq: [Typing Event Handlers](/guide/typescript/options-api.html#typing-event-handlers) <sup class="vt-badge ts" />

</div>

### "Method" va "Inline" aniqlanish uslubi

Vue dagi "template compiler", ya'ni shablon kompilyatori yoki qo'pol qilib aytganda HTML kompilyator avtomatik tarzda siz uzatgan kod bo'yicha uni "Method"(usul, funksiya) yoki "Inline"(javascript ifoda) ligini uning tuzulishi bo'yicha aniqlaydi.

Misol uchun `foo`, `foo.bar` va `foo['bar']` lar `foo` bu usul, funksiya nomi. Yoki `foo.bar` va `foo['bar']` `foo` obyektning `bar` usuli, funksiyasi. Kompilyator uni aniqlab "Method" deb belgilaydi.

Agar berilgan kod to'g'ri yozilgan javascript ifoda bo'lsa, uni "Inline" deb belgilaydi. Misol uchun `count++`.

## Calling Methods in Inline Handlers

Instead of binding directly to a method name, we can also call methods in an inline handler. This allows us to pass the method custom arguments instead of the native event:

<div class="composition-api">

```js
function say(message) {
  alert(message)
}
```

</div>
<div class="options-api">

```js
methods: {
  say(message) {
    alert(message)
  }
}
```

</div>

```vue-html
<button @click="say('hello')">Say hello</button>
<button @click="say('bye')">Say bye</button>
```

<div class="composition-api">

[Try it in the Playground](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdCBzZXR1cD5cbmZ1bmN0aW9uIHNheShtZXNzYWdlKSB7XG4gIGFsZXJ0KG1lc3NhZ2UpXG59XG48L3NjcmlwdD5cblxuPHRlbXBsYXRlPlxuXHQ8YnV0dG9uIEBjbGljaz1cInNheSgnaGknKVwiPlNheSBoaTwvYnV0dG9uPlxuICA8YnV0dG9uIEBjbGljaz1cInNheSgnd2hhdCcpXCI+U2F5IHdoYXQ8L2J1dHRvbj5cbjwvdGVtcGxhdGU+IiwiaW1wb3J0LW1hcC5qc29uIjoie1xuICBcImltcG9ydHNcIjoge1xuICAgIFwidnVlXCI6IFwiaHR0cHM6Ly9zZmMudnVlanMub3JnL3Z1ZS5ydW50aW1lLmVzbS1icm93c2VyLmpzXCJcbiAgfVxufSJ9)

</div>
<div class="options-api">

[Try it in the Playground](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdD5cbmV4cG9ydCBkZWZhdWx0IHtcbiAgbWV0aG9kczoge1xuXHQgIHNheShtZXNzYWdlKSB7XG4gICAgXHRhbGVydChtZXNzYWdlKVxuICBcdH1cblx0fVxufVxuPC9zY3JpcHQ+XG5cbjx0ZW1wbGF0ZT5cblx0PGJ1dHRvbiBAY2xpY2s9XCJzYXkoJ2hpJylcIj5TYXkgaGk8L2J1dHRvbj5cbiAgPGJ1dHRvbiBAY2xpY2s9XCJzYXkoJ3doYXQnKVwiPlNheSB3aGF0PC9idXR0b24+XG48L3RlbXBsYXRlPiIsImltcG9ydC1tYXAuanNvbiI6IntcbiAgXCJpbXBvcnRzXCI6IHtcbiAgICBcInZ1ZVwiOiBcImh0dHBzOi8vc2ZjLnZ1ZWpzLm9yZy92dWUucnVudGltZS5lc20tYnJvd3Nlci5qc1wiXG4gIH1cbn0ifQ==)

</div>

## Accessing Event Argument in Inline Handlers

Sometimes we also need to access the original DOM event in an inline handler. You can pass it into a method using the special `$event` variable, or use an inline arrow function:

```vue-html
<!-- using $event special variable -->
<button @click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>

<!-- using inline arrow function -->
<button @click="(event) => warn('Form cannot be submitted yet.', event)">
  Submit
</button>
```

<div class="composition-api">

```js
function warn(message, event) {
  // now we have access to the native event
  if (event) {
    event.preventDefault()
  }
  alert(message)
}
```

</div>
<div class="options-api">

```js
methods: {
  warn(message, event) {
    // now we have access to the native event
    if (event) {
      event.preventDefault()
    }
    alert(message)
  }
}
```

</div>

## Event Modifiers

It is a very common need to call `event.preventDefault()` or `event.stopPropagation()` inside event handlers. Although we can do this easily inside methods, it would be better if the methods can be purely about data logic rather than having to deal with DOM event details.

To address this problem, Vue provides **event modifiers** for `v-on`. Recall that modifiers are directive postfixes denoted by a dot.

- `.stop`
- `.prevent`
- `.self`
- `.capture`
- `.once`
- `.passive`

```vue-html
<!-- the click event's propagation will be stopped -->
<a @click.stop="doThis"></a>

<!-- the submit event will no longer reload the page -->
<form @submit.prevent="onSubmit"></form>

<!-- modifiers can be chained -->
<a @click.stop.prevent="doThat"></a>

<!-- just the modifier -->
<form @submit.prevent></form>

<!-- only trigger handler if event.target is the element itself -->
<!-- i.e. not from a child element -->
<div @click.self="doThat">...</div>
```

::: tip
Order matters when using modifiers because the relevant code is generated in the same order. Therefore using `@click.prevent.self` will prevent **clicks default action on the element itself and its children** while `@click.self.prevent` will only prevent clicks default action on the element itself.
:::

The `.capture`, `.once`, and `.passive` modifiers mirror the [options of the native `addEventListener` method](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#options):

```vue-html
<!-- use capture mode when adding the event listener -->
<!-- i.e. an event targeting an inner element is handled here before being handled by that element -->
<div @click.capture="doThis">...</div>

<!-- the click event will be triggered at most once -->
<a @click.once="doThis"></a>

<!-- the scroll event's default behavior (scrolling) will happen -->
<!-- immediately, instead of waiting for `onScroll` to complete  -->
<!-- in case it contains `event.preventDefault()`                -->
<div @scroll.passive="onScroll">...</div>
```

The `.passive` modifier is typically used with touch event listeners for [improving performance on mobile devices](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#improving_scrolling_performance_with_passive_listeners).

::: tip
Do not use `.passive` and `.prevent` together, because `.passive` already indicates to the browser that you _do not_ intend to prevent the event's default behavior, and you will likely see a warning from the browser if you do so.
:::

## Key Modifiers

When listening for keyboard events, we often need to check for specific keys. Vue allows adding key modifiers for `v-on` or `@` when listening for key events:

```vue-html
<!-- only call `vm.submit()` when the `key` is `Enter` -->
<input @keyup.enter="submit" />
```

You can directly use any valid key names exposed via [`KeyboardEvent.key`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key/Key_Values) as modifiers by converting them to kebab-case.

```vue-html
<input @keyup.page-down="onPageDown" />
```

In the above example, the handler will only be called if `$event.key` is equal to `'PageDown'`.

### Key Aliases

Vue provides aliases for the most commonly used keys:

- `.enter`
- `.tab`
- `.delete` (captures both "Delete" and "Backspace" keys)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

### System Modifier Keys

You can use the following modifiers to trigger mouse or keyboard event listeners only when the corresponding modifier key is pressed:

- `.ctrl`
- `.alt`
- `.shift`
- `.meta`

::: tip Note
On Macintosh keyboards, meta is the command key (⌘). On Windows keyboards, meta is the Windows key (⊞). On Sun Microsystems keyboards, meta is marked as a solid diamond (◆). On certain keyboards, specifically MIT and Lisp machine keyboards and successors, such as the Knight keyboard, space-cadet keyboard, meta is labeled “META”. On Symbolics keyboards, meta is labeled “META” or “Meta”.
:::

For example:

```vue-html
<!-- Alt + Enter -->
<input @keyup.alt.enter="clear" />

<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```

::: tip
Note that modifier keys are different from regular keys and when used with `keyup` events, they have to be pressed when the event is emitted. In other words, `keyup.ctrl` will only trigger if you release a key while holding down `ctrl`. It won't trigger if you release the `ctrl` key alone.
:::

### `.exact` Modifier

The `.exact` modifier allows control of the exact combination of system modifiers needed to trigger an event.

```vue-html
<!-- this will fire even if Alt or Shift is also pressed -->
<button @click.ctrl="onClick">A</button>

<!-- this will only fire when Ctrl and no other keys are pressed -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- this will only fire when no system modifiers are pressed -->
<button @click.exact="onClick">A</button>
```

## Mouse Button Modifiers

- `.left`
- `.right`
- `.middle`

These modifiers restrict the handler to events triggered by a specific mouse button.
