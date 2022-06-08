# Conditional Rendering

<div class="options-api">
  <VueSchoolLink href="https://vueschool.io/lessons/conditional-rendering-in-vue-3" title="Free Vue.js Conditional Rendering Lesson"/>
</div>

<div class="composition-api">
  <VueSchoolLink href="https://vueschool.io/lessons/vue-fundamentals-capi-conditionals-in-vue" title="Free Vue.js Conditional Rendering Lesson"/>
</div>

<script setup>
import { ref } from 'vue'
const awesome = ref(true)
</script>

## `v-if`

`v-if` ko'rsatuvchisi (directive) blok kodni shartli ko'rsatish uchun ishlatiladi. Blok kod `v-if` ko'rsatuvchisining ifodasi(expression) rost qiymat qaytargandagina sahifada ko'rinadi.

```vue-html
<h1 v-if="awesome">Vue is awesome!</h1>
```

## `v-else`

Siz `v-else`dan `v-if`ning "boshqa blok kod"ini ko'rsatishda ishlatishingiz mumkin:

```vue-html
<button @click="awesome = !awesome">Toggle</button>

<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```

<div class="demo">
  <button @click="awesome = !awesome">Toggle</button>
  <h1 v-if="awesome">Vue is   !</h1>
  <h1 v-else>Oh no 😢</h1>
</div>

<div class="composition-api">

[Try it in the Playground](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdCBzZXR1cD5cbmltcG9ydCB7IHJlZiB9IGZyb20gJ3Z1ZSdcblxuY29uc3QgYXdlc29tZSA9IHJlZih0cnVlKVxuPC9zY3JpcHQ+XG5cbjx0ZW1wbGF0ZT5cbiAgPGJ1dHRvbiBAY2xpY2s9XCJhd2Vzb21lID0gIWF3ZXNvbWVcIj50b2dnbGU8L2J1dHRvbj5cblxuXHQ8aDEgdi1pZj1cImF3ZXNvbWVcIj5WdWUgaXMgYXdlc29tZSE8L2gxPlxuXHQ8aDEgdi1lbHNlPk9oIG5vIPCfmKI8L2gxPlxuPC90ZW1wbGF0ZT4iLCJpbXBvcnQtbWFwLmpzb24iOiJ7XG4gIFwiaW1wb3J0c1wiOiB7XG4gICAgXCJ2dWVcIjogXCJodHRwczovL3NmYy52dWVqcy5vcmcvdnVlLnJ1bnRpbWUuZXNtLWJyb3dzZXIuanNcIlxuICB9XG59In0=)

</div>
<div class="options-api">

[Try it in the Playground](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdD5cbmV4cG9ydCBkZWZhdWx0IHtcbiAgZGF0YSgpIHtcbiAgXHRyZXR1cm4ge1xuXHQgICAgYXdlc29tZTogdHJ1ZVxuICBcdH1cblx0fVxufVxuPC9zY3JpcHQ+XG5cbjx0ZW1wbGF0ZT5cbiAgPGJ1dHRvbiBAY2xpY2s9XCJhd2Vzb21lID0gIWF3ZXNvbWVcIj50b2dnbGU8L2J1dHRvbj5cblxuXHQ8aDEgdi1pZj1cImF3ZXNvbWVcIj5WdWUgaXMgYXdlc29tZSE8L2gxPlxuXHQ8aDEgdi1lbHNlPk9oIG5vIPCfmKI8L2gxPlxuPC90ZW1wbGF0ZT4iLCJpbXBvcnQtbWFwLmpzb24iOiJ7XG4gIFwiaW1wb3J0c1wiOiB7XG4gICAgXCJ2dWVcIjogXCJodHRwczovL3NmYy52dWVqcy5vcmcvdnVlLnJ1bnRpbWUuZXNtLWJyb3dzZXIuanNcIlxuICB9XG59In0=)

</div>

`v-else` elementi `v-if` yoki `v-else-if` elementining ortidan kelishi shart - aks holda kod ishga tushmaydi.

## `v-else-if`

`v-else-if`, nomidan ko'rinib turganidek, `v-if` uchun "yana boshqa shart"ni bajarishda xizmat qiladi. U bir necha marotaba zanjirlanib kelishi mumkin:

```vue-html
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

`v-else` ga o'xshab, `v-else-if` elementi ham `v-if` yoki `v-else-if` elementining ortidan kelishi shart.

## `<template>`dagi `v-if`

`v-if` ko'rsatuvchi (directive) bo'lgani uchun, u yolg'iz elementga biriktirilishi shart. Ammo bir nechta elementni almashtirmoqchi bo'lsak-chi? Bu holatda biz `v-if`ni "ko'rinmas o'rab turadigan" - "qobiq" bo'lib xizmat qiluvchi `<template>` elementida ishlatishimiz mumkin. Sahifada ko'rinadigan so'nggi natija `<template>` elementini o'z ichiga olmaydi.

```vue-html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

`v-else` va `v-else-if` ham `<template>`da ishlatilishi mumkin.

## `v-show`

Shartli ravishda ko'rsatishning boshqa bir varianti bu `v-show` ko'rsatuvchisi hisoblanadi. Foydalanish asosan bir xil:

```vue-html
<h1 v-show="ok">Hello!</h1>
```

Farq shundaki, `v-show` bilan ishlatilgan element doim sahifaga render bo'ladi va DOMda qoladi; `v-show` faqat elementning `display` CSS xususiyatini almashtiradi.

`v-show` xuddi `v-else` bilan ishlamaganidek, `<template>` elementini ham qo'llab-quvvatlamaydi.

## `v-if` `v-show`ga qarshi

`v-if` bu "haqiqiy - real" shartli renderlash ko'rsatuvchisi hisoblanadi, chunki u shartli blok ichidagi hodisa eshituvchilari (event listeners) va bola komponentlarning to'g'ri yo'q qilinishi va almashinishlar davomida qayta yaratilishini ta'minlaydi.

**P.S.** Ya'ni, agarda `v-if` ning qiymati `yolg'on` (falsy) qiymatga o'zgarsa, bu holatda `v-if` bilan bog'langan komponent butun sahifadan o'chib ketadi, DOMdan ham, `rost` (truthy) qiymatga o'zgarganda, yana yangidan yaratiladi.

`v-if` yana **lazy** ham hisoblanadi: agar shart dastlabki renderda `yolg'on` qiymatda bo'lsa, u hech narsa qilmaydi - shart birinchi marta to'g'ri bo'lmaguncha shartli blok ko'rsatilmaydi.

Taqqoslaganda, `v-show` ancha soddaroq - element har doim, boshlang'ich holatidan qat'iy nazar, CSSga asoslangan almashtirish bilan ko'rsatiladi.

Umumiy qilib aytganda, `v-if` almashtirishda ko'p kuch sarflasa, `v-show` boshlang'ich renderda ko'p kuch ketkazadi. Shuning uchun siz biror narsani tez-tez almashtirmoqchi bo'lsangiz `v-show`ni afzal tuting, agar `shart` ishlab turgan (`runtime`) vaqtida o'zgarishi mumkin bo'lmasa `v-if`ni tanlang.

## `v-if` bilan `v-for`

::: warning Yodda tuting
`v-if` va `v-for`ni bitta element ichida ishlatish **tavsiya qilinmaydi**. Batafsil ma'lumot uchun [style guide](/style-guide/rules-essential.html#avoid-v-if-with-v-for) ga murojaat qiling.
:::

`v-if` va `v-for`ni bir element ichida ishlatilganda, `v-if` birinchi bo'lib baholanadi. Batafsil ma'lumot uchun [list rendering guide](list#v-for-with-v-if) ni ko'ring.
