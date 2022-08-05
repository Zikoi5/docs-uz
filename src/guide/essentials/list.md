# List Rendering (Ro'yxatni sahifada ko'rsatish)

<div class="options-api">
  <VueSchoolLink href="https://vueschool.io/lessons/list-rendering-in-vue-3" title="Free Vue.js List Rendering Lesson"/>
</div>

<div class="composition-api">
  <VueSchoolLink href="https://vueschool.io/lessons/vue-fundamentals-capi-list-rendering-in-vue" title="Free Vue.js List Rendering Lesson"/>
</div>

## `v-for`

Biz `v-for` ko'rsatuvchisini arrayga asoslangan holda elementlarning ro'yxatini sahifada ko'rsatish uchun ishlatishimiz mumkin. `items` array ma'lumotlarining manbasi va `item` bo'lsa takrorlanadigan array elementi uchun **taxallus** bo'lsa, `v-for` ko'rsatuvchisi `item in items` ko'rinishidagi maxsus sintaksisni talab qiladi:

<div class="composition-api">

```js
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])
```

</div>

<div class="options-api">

```js
data() {
  return {
    items: [{ message: 'Foo' }, { message: 'Bar' }]
  }
}
```

</div>

```vue-html
<li v-for="item in items">
  {{ item.message }}
</li>
```

`v-for` ichida, template iboralar ota qamrovining (scope) xususiyatlariga bog'lana oladi. Bundan tashqari, `v-for` joriy element indeksi uchun ixtiyoriy ikkinchi taxallusni ham qo'llab-quvvatlaydi:

<div class="composition-api">

```js
const parentMessage = ref('Parent')
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])
```

</div>
<div class="options-api">

```js
data() {
  return {
    parentMessage: 'Parent',
    items: [{ message: 'Foo' }, { message: 'Bar' }]
  }
}
```

</div>

```vue-html
<li v-for="(item, index) in items">
  {{ parentMessage }} - {{ index }} - {{ item.message }}
</li>
```

<script setup>
const parentMessage = 'Parent'
const items = [{ message: 'Foo' }, { message: 'Bar' }]
</script>
<div class="demo">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</div>

<div class="composition-api">

[Try it in the Playground](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdCBzZXR1cD5cbmltcG9ydCB7IHJlZiB9IGZyb20gJ3Z1ZSdcblxuY29uc3QgcGFyZW50TWVzc2FnZSA9IHJlZignUGFyZW50JylcbmNvbnN0IGl0ZW1zID0gcmVmKFt7IG1lc3NhZ2U6ICdGb28nIH0sIHsgbWVzc2FnZTogJ0JhcicgfV0pXG48L3NjcmlwdD5cblxuPHRlbXBsYXRlPlxuXHQ8bGkgdi1mb3I9XCIoaXRlbSwgaW5kZXgpIGluIGl0ZW1zXCI+XG4gIFx0e3sgcGFyZW50TWVzc2FnZSB9fSAtIHt7IGluZGV4IH19IC0ge3sgaXRlbS5tZXNzYWdlIH19XG5cdDwvbGk+XG48L3RlbXBsYXRlPiIsImltcG9ydC1tYXAuanNvbiI6IntcbiAgXCJpbXBvcnRzXCI6IHtcbiAgICBcInZ1ZVwiOiBcImh0dHBzOi8vc2ZjLnZ1ZWpzLm9yZy92dWUucnVudGltZS5lc20tYnJvd3Nlci5qc1wiXG4gIH1cbn0ifQ==)

</div>
<div class="options-api">

[Try it in the Playground](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdD5cbmV4cG9ydCBkZWZhdWx0IHtcbiAgZGF0YSgpIHtcbiAgXHRyZXR1cm4ge1xuXHQgICAgcGFyZW50TWVzc2FnZTogJ1BhcmVudCcsXG4gICAgXHRpdGVtczogW3sgbWVzc2FnZTogJ0ZvbycgfSwgeyBtZXNzYWdlOiAnQmFyJyB9XVxuICBcdH1cblx0fVxufVxuPC9zY3JpcHQ+XG5cbjx0ZW1wbGF0ZT5cblx0PGxpIHYtZm9yPVwiKGl0ZW0sIGluZGV4KSBpbiBpdGVtc1wiPlxuICBcdHt7IHBhcmVudE1lc3NhZ2UgfX0gLSB7eyBpbmRleCB9fSAtIHt7IGl0ZW0ubWVzc2FnZSB9fVxuXHQ8L2xpPlxuPC90ZW1wbGF0ZT4iLCJpbXBvcnQtbWFwLmpzb24iOiJ7XG4gIFwiaW1wb3J0c1wiOiB7XG4gICAgXCJ2dWVcIjogXCJodHRwczovL3NmYy52dWVqcy5vcmcvdnVlLnJ1bnRpbWUuZXNtLWJyb3dzZXIuanNcIlxuICB9XG59In0=)

</div>

`v-for` o'zgaruvchisining qamrovi (scope) quyidagi JavaScriptga o'xshaydi:

```js
const parentMessage = 'Parent'
const items = [
  /* ... */
]

items.forEach((item, index) => {
  // tashqi skopdagi `parentMessage`ga bog'lana oladi
  // lekin `item` va `index`lar faqat shu yerdagina mavjud
  console.log(parentMessage, item.message, index)
})
```
`v-for`ning qiymati `forEach` callback funksiyasiga qanday mos kelishiga e'tibor bering. Aslida, xuddi funksiya argumentlarini destructuring qilishga o'xshab, `v-for` elementi taxallusi ustida **destructuring**dan (`destructuring` - bu arraylardagi qiymatlarni yoki obyektlardagi xususiyatlarni alohida o'zgaruvchilarga ochish imkonini beruvchi JavaScript ifodasi) foydalanishingiz mumkin:

```vue-html
<li v-for="{ message } in items">
  {{ message }}
</li>

<!-- with index alias -->
<li v-for="({ message }, index) in items">
  {{ message }} {{ index }}
</li>
```

Ichma-ich joylashgan `v-for` uchun, o'rab turish (scoping) ham ichma-ich bo'lgan funksiyalarga o'xshab ishlaydi. Har bir `v-for` qamrovida otaning qamroviga (scope) bo'glanish - kirish huquqiga ega:

```vue-html
<li v-for="item in items">
  <span v-for="childItem in item.children">
    {{ item.message }} {{ childItem }}
  </span>
</li>
```

Shuningdek, takrorlanuvchilar uchun JavaScriptning sintaksisiga yaqinroq bo'lishi uchun `in` o'rniga `of` dan foydalanishingiz mumkin:

```vue-html
<div v-for="item of items"></div>
```

## `v-for`ning Obyekt bilan ishlatilishi

`v-for` obyektning xususiyatlari orqali aylanib chiqish uchun foydalanishingiz ham mumkin:

<div class="composition-api">

```js
const myObject = reactive({
  title: 'How to do lists in Vue',
  author: 'Jane Doe',
  publishedAt: '2016-04-10'
})
```

</div>
<div class="options-api">

```js
data() {
  return {
    myObject: {
      title: 'How to do lists in Vue',
      author: 'Jane Doe',
      publishedAt: '2016-04-10'
    }
  }
}
```

</div>

```vue-html
<ul>
  <li v-for="value in myObject">
    {{ value }}
  </li>
</ul>
```

Xususiyat (property) nomini ikkinchi taxallus (alias) bilan ta'minlash mumkin (a.k.a key):

```vue-html
<li v-for="(value, key) in myObject">
  {{ key }}: {{ value }}
</li>
```
Va boshqa indeks uchun:

```vue-html
<li v-for="(value, key, index) in myObject">
  {{ index }}. {{ key }}: {{ value }}
</li>
```

<div class="composition-api">

[Try it in the Playground](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdCBzZXR1cD5cbmltcG9ydCB7IHJlYWN0aXZlIH0gZnJvbSAndnVlJ1xuXG5jb25zdCBteU9iamVjdCA9IHJlYWN0aXZlKHtcbiAgdGl0bGU6ICdIb3cgdG8gZG8gbGlzdHMgaW4gVnVlJyxcbiAgYXV0aG9yOiAnSmFuZSBEb2UnLFxuICBwdWJsaXNoZWRBdDogJzIwMTYtMDQtMTAnXG59KVxuPC9zY3JpcHQ+XG5cbjx0ZW1wbGF0ZT5cblx0PHVsPlxuICAgIDxsaSB2LWZvcj1cIih2YWx1ZSwga2V5LCBpbmRleCkgaW4gbXlPYmplY3RcIj5cblx0XHQgIHt7IGluZGV4IH19LiB7eyBrZXkgfX06IHt7IHZhbHVlIH19XG5cdFx0PC9saT5cbiAgPC91bD5cbjwvdGVtcGxhdGU+IiwiaW1wb3J0LW1hcC5qc29uIjoie1xuICBcImltcG9ydHNcIjoge1xuICAgIFwidnVlXCI6IFwiaHR0cHM6Ly9zZmMudnVlanMub3JnL3Z1ZS5ydW50aW1lLmVzbS1icm93c2VyLmpzXCJcbiAgfVxufSJ9)

</div>
<div class="options-api">

[Try it in the Playground](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdD5cbmV4cG9ydCBkZWZhdWx0IHtcbiAgZGF0YSgpIHtcbiAgXHRyZXR1cm4ge1xuXHQgICAgbXlPYmplY3Q6IHtcbiAgXHQgICAgdGl0bGU6ICdIb3cgdG8gZG8gbGlzdHMgaW4gVnVlJyxcblx0ICAgICAgYXV0aG9yOiAnSmFuZSBEb2UnLFxuICAgICAgXHRwdWJsaXNoZWRBdDogJzIwMTYtMDQtMTAnXG4gICAgXHR9XG4gIFx0fVxuXHR9XG59XG48L3NjcmlwdD5cblxuPHRlbXBsYXRlPlxuXHQ8dWw+XG4gICAgPGxpIHYtZm9yPVwiKHZhbHVlLCBrZXksIGluZGV4KSBpbiBteU9iamVjdFwiPlxuXHRcdCAge3sgaW5kZXggfX0uIHt7IGtleSB9fToge3sgdmFsdWUgfX1cblx0XHQ8L2xpPlxuICA8L3VsPlxuPC90ZW1wbGF0ZT4iLCJpbXBvcnQtbWFwLmpzb24iOiJ7XG4gIFwiaW1wb3J0c1wiOiB7XG4gICAgXCJ2dWVcIjogXCJodHRwczovL3NmYy52dWVqcy5vcmcvdnVlLnJ1bnRpbWUuZXNtLWJyb3dzZXIuanNcIlxuICB9XG59In0=)

</div>

:::tip Yodda tuting!

Obyektni aylanib chiqayotganda, tartib `Object.keys()`ning ro'yxatga olishdagi tartibiga asoslanadi, bu JavaScript dvigateli ilovalarida izchil bo'lishi kafolatlanmaydi.
:::

## `v-for` bilan chegara

`v-for` butun sonni ham qabul qiladi. Bu holatda u `1...n`ning chegarasiga asoslanib, `template`ni ko'p marta takrorlaydi.

```vue-html
<span v-for="n in 10">{{ n }}</span>
```

Yodda tuting, bu yerda `n`ning boshlang'ich qiymati `0` o'rniga `1` bilan boshlanadi.

## `<template>`da `v-for`


`v-if` shabloniga o'xshab, bir nechta elementlar blokini ko'rsatish uchun `v-for` bilan `<template>` tegidan ham foydalanishingiz mumkin. Masalan:

```vue-html
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```

## `v-if` bilan `v-for`ning ishlatilishi

:::warning Yodda tuting!

`v-if` va `v-for`ni yashirin ustunlik tufayli bir element ichida ishlatish **tavsiya etilmaydi**. Ba'tafsil ma'lumot olish uchun [style guide](/style-guide/rules-essential.html#avoid-v-if-with-v-for)ga murojaat qiling.
:::

Qachonki ular bir elementda mavjud bo'lsa, `v-if`ning ustuvorligi `v-for`nikiga qaraganda balandroq bo'ladi. Bu shuni anglatadiki, `v-if` ko'rsatuchisi `v-for` `scope`ining o'zgaruvchilariga bog'lana olmaydi:

```vue-html
<!--
Bu yerda "todo" xususiyati komponent namunasida topilmagani uchun xatolik yuz beradi.
-->
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo.name }}
</li>
```

Bu `v-for` ni, ko'zga ko'rinmas qatlam sifatida xizmat qiluvchi `<template>` tegi ichiga ko'chirish bilan to'g'rilanishi mumkin:

```vue-html
<template v-for="todo in todos">
  <li v-if="!todo.isComplete">
    {{ todo.name }}
  </li>
</template>
```

## Holatni `key` bilan saqlab turish

Vue `v-for` bilan ko'rsatilgan elementlar ro'yxatini yangilayotganda, doimiy holat (default) bo'yicha u "in-place patch (joyida yamash)" strategiyasidan foydalanadi. Agar ma'lumotlar elementlarining tartibi o'zgargan bo'lsa, DOM elementlarini, elementlarning tartibiga mos ravishda siljitish o'rniga, Vue har bir elementni joyiga qo'yadi va u o'sha indeksda ko'rsatilishi kerak bo'lgan narsani aks ettiradi.

Bu doimiy holat samarali, lekin **faqat ro'yxatni ko'rsatish chiqishi, bola komponent holatiga yoki vaqtinchalik DOM holatiga (masalan, form input qiymatlari) tayanmasagina mos keladi**.

`Vue`ga har bir elementning identifikatorini kuzatishi va shu tariqa mavjud elementlarni qayta ishlatishi va tartiblashi uchun yo'nalish-yordam berish uchun har bir element uchun noyob `key` atributini ta'minlashingiz kerak:

```vue-html
<div v-for="item in items" :key="item.id">
  <!-- content -->
</div>
```

`<template v-for>`dan foydalanayotganda, `key` `template` konteynerida joylashgan bo'lishi kerak:

```vue-html
<template v-for="todo in todos" :key="todo.name">
  <li>{{ todo.name }}</li>
</template>
```

:::tip Yodda tuting!
Bu yerda `key` maxsus attribut bo'lgan `v-bind` bilan bog'langan bo'ladi. [`v-for` obyekt bilan ishlatilayotganda](#v-for-with-an-object) `key` o'zgaruvchisi bilan chalkashtirilmasligi kerak.
:::

DOMning takrorlangan (iterated) kontent oddiy bo'lmasa (masalan, hech qanday komponent yoki statistik DOM elementlarini o'z ichiga olmagan bo'lsa) yoki unumdorlikni oshirish uchun ataylab standart xatti-harakatlarga tayansangiz, imkoni boricha `v-for`ni `key` attributi bilan ta'minlash [tavsiya etiladi](/style-guide/rules-essential.html#use-keyed-v-for).

`key` o'zgarmas qiymatlariga bog'lanishni kutadi - masalan, `string` va `raqamlar`. Obyektlarni `v-for`ning `key`i sifatida ishlatmang. `key` attributining foydalanilishi haqidagi ba'tafsil ma'lumot uchun, iltimos [`key` API documentation](/api/built-in-special-attributes.html#key)ni ko'rib chiqing.

## `v-for`ning Componentlarda ishlatilishi

> Bu bo'lim [Komponentlar](/guide/essentials/component-basics) haqidagi bilimlarni o'z ichiga oladi. O'tkazib yuborishingiz va keyinroq qaytishingiz mumkin.

Komponentda `v-for`ni boshqa normal elementlarga o'xshab to'g'ridan-to'g'ri foydalanishingiz mumkin (`key` bilan ta'minlashni unutmang):

```vue-html
<my-component v-for="item in items" :key="item.id"></my-component>
```

Biroq, bu komponentga hech qanday ma'lumotni avtomatik ravishda uzatmaydi, chunki komponentlar o'zlarining izolyatsiyalangan doiralariga ega. Takrorlangan ma'lumotlarni komponentga o'tkazish uchun biz xususiyatlardan (props) ham foydalanishimiz kerak:

```vue-html
<my-component
  v-for="(item, index) in items"
  :item="item"
  :index="index"
  :key="item.id"
></my-component>
```

Komponentga avtomatik ravishda `item` kiritilmasligining sababi shundaki, bu komponentni `v-for` qanday ishlashi bilan chambarchas bog'laydi. Uning ma'lumotlari qayerdan kelganligi aniq bo'lishi komponentni boshqa holatlarda qayta foydalanishga imkon beradi.

<div class="composition-api">

`v-for`ning Komponentlar ro'yxatini qanday qilib sahifada ko'rsatish va har bir komponent namunasiga turli xil ma'lumotlarni o'tkazishni bilish uchun tekshirib ko'ring [`Todo List`ning oddiy misoli](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdCBzZXR1cD5cbmltcG9ydCB7IHJlZiB9IGZyb20gJ3Z1ZSdcbmltcG9ydCBUb2RvSXRlbSBmcm9tICcuL1RvZG9JdGVtLnZ1ZSdcbiAgXG5jb25zdCBuZXdUb2RvVGV4dCA9IHJlZignJylcbmNvbnN0IHRvZG9zID0gcmVmKFtcbiAge1xuICAgIGlkOiAxLFxuICAgIHRpdGxlOiAnRG8gdGhlIGRpc2hlcydcbiAgfSxcbiAge1xuICAgIGlkOiAyLFxuICAgIHRpdGxlOiAnVGFrZSBvdXQgdGhlIHRyYXNoJ1xuICB9LFxuICB7XG4gICAgaWQ6IDMsXG4gICAgdGl0bGU6ICdNb3cgdGhlIGxhd24nXG4gIH1cbl0pXG5cbmxldCBuZXh0VG9kb0lkID0gNFxuXG5mdW5jdGlvbiBhZGROZXdUb2RvKCkge1xuICB0b2Rvcy52YWx1ZS5wdXNoKHtcbiAgICBpZDogbmV4dFRvZG9JZCsrLFxuICAgIHRpdGxlOiBuZXdUb2RvVGV4dC52YWx1ZVxuICB9KVxuICBuZXdUb2RvVGV4dC52YWx1ZSA9ICcnXG59XG48L3NjcmlwdD5cblxuPHRlbXBsYXRlPlxuXHQ8Zm9ybSB2LW9uOnN1Ym1pdC5wcmV2ZW50PVwiYWRkTmV3VG9kb1wiPlxuICAgIDxsYWJlbCBmb3I9XCJuZXctdG9kb1wiPkFkZCBhIHRvZG88L2xhYmVsPlxuICAgIDxpbnB1dFxuICAgICAgdi1tb2RlbD1cIm5ld1RvZG9UZXh0XCJcbiAgICAgIGlkPVwibmV3LXRvZG9cIlxuICAgICAgcGxhY2Vob2xkZXI9XCJFLmcuIEZlZWQgdGhlIGNhdFwiXG4gICAgLz5cbiAgICA8YnV0dG9uPkFkZDwvYnV0dG9uPlxuICA8L2Zvcm0+XG4gIDx1bD5cbiAgICA8dG9kby1pdGVtXG4gICAgICB2LWZvcj1cIih0b2RvLCBpbmRleCkgaW4gdG9kb3NcIlxuICAgICAgOmtleT1cInRvZG8uaWRcIlxuICAgICAgOnRpdGxlPVwidG9kby50aXRsZVwiXG4gICAgICBAcmVtb3ZlPVwidG9kb3Muc3BsaWNlKGluZGV4LCAxKVwiXG4gICAgPjwvdG9kby1pdGVtPlxuICA8L3VsPlxuPC90ZW1wbGF0ZT4iLCJpbXBvcnQtbWFwLmpzb24iOiJ7XG4gIFwiaW1wb3J0c1wiOiB7XG4gICAgXCJ2dWVcIjogXCJodHRwczovL3NmYy52dWVqcy5vcmcvdnVlLnJ1bnRpbWUuZXNtLWJyb3dzZXIuanNcIlxuICB9XG59IiwiVG9kb0l0ZW0udnVlIjoiPHNjcmlwdCBzZXR1cD5cbmRlZmluZVByb3BzKFsndGl0bGUnXSlcbmRlZmluZUVtaXRzKFsncmVtb3ZlJ10pXG48L3NjcmlwdD5cblxuPHRlbXBsYXRlPlxuICA8bGk+XG4gICAge3sgdGl0bGUgfX1cbiAgICA8YnV0dG9uIEBjbGljaz1cIiRlbWl0KCdyZW1vdmUnKVwiPlJlbW92ZTwvYnV0dG9uPlxuICA8L2xpPlxuPC90ZW1wbGF0ZT4ifQ==)

</div>
<div class="options-api">

`v-for`ning Komponentlar ro'yxatini qanday qilib sahifada ko'rsatish va har bir komponent namunasiga turli xil ma'lumotlarni o'tkazishni bilish uchun tekshirib ko'ring [`Todo List`ning oddiy misoli](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdD5cbmltcG9ydCBUb2RvSXRlbSBmcm9tICcuL1RvZG9JdGVtLnZ1ZSdcbiAgXG5leHBvcnQgZGVmYXVsdCB7XG4gIGNvbXBvbmVudHM6IHsgVG9kb0l0ZW0gfSxcbiAgZGF0YSgpIHtcbiAgICByZXR1cm4ge1xuICAgICAgbmV3VG9kb1RleHQ6ICcnLFxuICAgICAgdG9kb3M6IFtcbiAgICAgICAge1xuICAgICAgICAgIGlkOiAxLFxuICAgICAgICAgIHRpdGxlOiAnRG8gdGhlIGRpc2hlcydcbiAgICAgICAgfSxcbiAgICAgICAge1xuICAgICAgICAgIGlkOiAyLFxuICAgICAgICAgIHRpdGxlOiAnVGFrZSBvdXQgdGhlIHRyYXNoJ1xuICAgICAgICB9LFxuICAgICAgICB7XG4gICAgICAgICAgaWQ6IDMsXG4gICAgICAgICAgdGl0bGU6ICdNb3cgdGhlIGxhd24nXG4gICAgICAgIH1cbiAgICAgIF0sXG4gICAgICBuZXh0VG9kb0lkOiA0XG4gICAgfVxuICB9LFxuICBtZXRob2RzOiB7XG4gICAgYWRkTmV3VG9kbygpIHtcbiAgICAgIHRoaXMudG9kb3MucHVzaCh7XG4gICAgICAgIGlkOiB0aGlzLm5leHRUb2RvSWQrKyxcbiAgICAgICAgdGl0bGU6IHRoaXMubmV3VG9kb1RleHRcbiAgICAgIH0pXG4gICAgICB0aGlzLm5ld1RvZG9UZXh0ID0gJydcbiAgICB9XG4gIH1cbn1cbjwvc2NyaXB0PlxuXG48dGVtcGxhdGU+XG5cdDxmb3JtIHYtb246c3VibWl0LnByZXZlbnQ9XCJhZGROZXdUb2RvXCI+XG4gICAgPGxhYmVsIGZvcj1cIm5ldy10b2RvXCI+QWRkIGEgdG9kbzwvbGFiZWw+XG4gICAgPGlucHV0XG4gICAgICB2LW1vZGVsPVwibmV3VG9kb1RleHRcIlxuICAgICAgaWQ9XCJuZXctdG9kb1wiXG4gICAgICBwbGFjZWhvbGRlcj1cIkUuZy4gRmVlZCB0aGUgY2F0XCJcbiAgICAvPlxuICAgIDxidXR0b24+QWRkPC9idXR0b24+XG4gIDwvZm9ybT5cbiAgPHVsPlxuICAgIDx0b2RvLWl0ZW1cbiAgICAgIHYtZm9yPVwiKHRvZG8sIGluZGV4KSBpbiB0b2Rvc1wiXG4gICAgICA6a2V5PVwidG9kby5pZFwiXG4gICAgICA6dGl0bGU9XCJ0b2RvLnRpdGxlXCJcbiAgICAgIEByZW1vdmU9XCJ0b2Rvcy5zcGxpY2UoaW5kZXgsIDEpXCJcbiAgICA+PC90b2RvLWl0ZW0+XG4gIDwvdWw+XG48L3RlbXBsYXRlPiIsImltcG9ydC1tYXAuanNvbiI6IntcbiAgXCJpbXBvcnRzXCI6IHtcbiAgICBcInZ1ZVwiOiBcImh0dHBzOi8vc2ZjLnZ1ZWpzLm9yZy92dWUucnVudGltZS5lc20tYnJvd3Nlci5qc1wiXG4gIH1cbn0iLCJUb2RvSXRlbS52dWUiOiI8c2NyaXB0PlxuZXhwb3J0IGRlZmF1bHQge1xuXHRwcm9wczogWyd0aXRsZSddLFxuICBlbWl0czogWydyZW1vdmUnXVxufVxuPC9zY3JpcHQ+XG5cbjx0ZW1wbGF0ZT5cbiAgPGxpPlxuICAgIHt7IHRpdGxlIH19XG4gICAgPGJ1dHRvbiBAY2xpY2s9XCIkZW1pdCgncmVtb3ZlJylcIj5SZW1vdmU8L2J1dHRvbj5cbiAgPC9saT5cbjwvdGVtcGxhdGU+In0=).

</div>

## Array O'zgarishini aniqlash

### O'zgartiruvchi methodlar

Vue kuzatilgan arrayning o'zgartiruvchi metodlarini o‘rab oladi, shuning uchun ular yangilanishlarini ham ishga tushiradi. O'ralgan metodlar quyidagilardir:

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

### Arrayni almashtirish

O'zgartiruvchi metodlar, nomidan ko'rinib turibdiki, ular chaqirilgan original arrayni o'zgartiradi. Taqqoslash uchun, o'zgartirmaydigan metodlar ham mavjud. Masalan, `filter()`, `concat()` va `slice()`, ular original arrayni o`zgartirmaydi, lekin **har doim yangi arrayni qaytaradi**. O'zgartirmaydigan metodlar bilan ishlashda biz eski arrayni yangisiga almashtirishimiz kerak:

<div class="composition-api">

```js
// `items` is a ref with array value
items.value = items.value.filter((item) => item.message.match(/Foo/))
```

</div>
<div class="options-api">

```js
this.items = this.items.filter((item) => item.message.match(/Foo/))
```

</div>

Bu `Vue`ning, mavjud DOMni otib yuborishiga va butun ro'yxatni qayta ko'rsatishiga olib keladi deb o'ylashingiz mumkin - xayriyatki, unday emas. `Vue` DOM elementidan qayta foydalanishni maksimal darajada oshirish uchun ba'zi aqlli yechimlarni amalga oshiradi, shuning uchun arrayni, bir-biriga o'xshash obyektlarni o'z ichiga olgan boshqa array bilan almashtirish juda samarali operatsiya hisoblanadi.

## Filtrlangan/Saralangan natijalarni ko'rsatish

Ba'zida biz arrayning, original ma'lumotlarni o'zgartirishsiz yoki qayta yozishsiz, filtrlangan yoki saralangan versiyasini ko'rsatishni xohlaymiz.

Misol uchun:

<div class="composition-api">

```js
const numbers = ref([1, 2, 3, 4, 5])

const evenNumbers = computed(() => {
  return numbers.value.filter((n) => n % 2 === 0)
})
```

</div>
<div class="options-api">

```js
data() {
  return {
    numbers: [1, 2, 3, 4, 5]
  }
},
computed: {
  evenNumbers() {
    return this.numbers.filter(n => n % 2 === 0)
  }
}
```

</div>

```vue-html
<li v-for="n in evenNumbers">{{ n }}</li>
```

`Computed property` ishlatilishi mumkin bo'lmagan holatlarda (masalan, ichma-ich joylashgan `v-for` looplari ichida), metoddan foydalanishingiz mumkin:

<div class="composition-api">

```js
const sets = ref([
  [1, 2, 3, 4, 5],
  [6, 7, 8, 9, 10]
])

function even(numbers) {
  return numbers.filter((number) => number % 2 === 0)
}
```

</div>
<div class="options-api">

```js
data() {
  return {
    sets: [[ 1, 2, 3, 4, 5 ], [6, 7, 8, 9, 10]]
  }
},
methods: {
  even(numbers) {
    return numbers.filter(number => number % 2 === 0)
  }
}
```

</div>

```vue-html
<ul v-for="numbers in sets">
  <li v-for="n in even(numbers)">{{ n }}</li>
</ul>
```

`reverse()` va `sort()` metodlarini `Computed property` ichida ishlatishda ehtiyot bo'ling! Bu ikki metodlar original arrayni o'zgartirib yuboradi. Bu metodlarni chaqirishdan oldin, original arrayning nusxasini yaratib oling: 

```diff
- return numbers.reverse()
+ return [...numbers].reverse()
```
