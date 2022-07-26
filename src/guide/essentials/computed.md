# Computed Properties (Oldindan hisoblangan funksiyalar)

<div class="options-api">
  <VueSchoolLink href="https://vueschool.io/lessons/computed-properties-in-vue-3" title="Free Vue.js Computed Properties Lesson"/>
</div>

<div class="composition-api">
  <VueSchoolLink href="https://vueschool.io/lessons/vue-fundamentals-capi-computed-properties-in-vue-with-the-composition-api" title="Free Vue.js Computed Properties Lesson"/>
</div>

## Sodda misol

Template ifodalari ("moustache" sintaksisi ichida yoziladigan ifoda (`expression`)) juda qulay, lekin ular sodda operatsiyalar bajarishda e'tiborga olinadi. `Template`laringizga juda ko'p mantiq kiritish ularni noqulay holatga keltiradi va saqlashni qiyinlashtiradi. Misol uchun, bizda ichma-ich joylashgan arrayga ega obyekt bo'lsa:

<div class="options-api">

```js
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  }
}
```

</div>
<div class="composition-api">

```js
const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})
```

</div>

Va biz, `muallif`da allaqachon bir nechta kitoblar borligi yoki umuman yo'qligiga qarab, turli xil xabarlarni sahifada ko'rsatishni xohlaymiz:

```vue-html
<p>Chop etilgan kitoblar:</p>
<span>{{ author.books.length > 0 ? 'Yes' : 'No' }}</span>
```

Bu holatda, `template` tartibsiz bo'lishni boshlaydi. `author.books` bilan bog'liq hisoblash ishga tushishidan oldin, Biz bir oz muddatga unga nazar solishimiz kerak. Eng muhimi, agar `template` ichida bu hisoblashni bir martadan ortiq ishlatish zarur bo'lsa, O'zimizni qaytarishni xohlamasligimiz mumkin.

Reaktiv ma'lumotlar murakkab bo'lgan mantiqni o'z ichiga oladi, shuning uchun **computed property**dan foydalanish tavsiya qilinadi. Bu yerda ham bir xil misol, tartibga solingan:

<div class="options-api">

```js
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  },
  computed: {
    // a computed getter
    publishedBooksMessage() {
      // `this` points to the component instance
      return this.author.books.length > 0 ? 'Yes' : 'No'
    }
  }
}
```

```vue-html
<p>Chop etilgan kitoblar:</p>
<span>{{ publishedBooksMessage }}</span>
```

[Try it in the Playground](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdD5cbmV4cG9ydCBkZWZhdWx0IHtcbiAgZGF0YSgpIHtcbiAgICByZXR1cm4ge1xuICAgICAgYXV0aG9yOiB7XG4gICAgICAgIG5hbWU6ICdKb2huIERvZScsXG4gICAgICAgIGJvb2tzOiBbXG4gICAgICAgICAgJ1Z1ZSAyIC0gQWR2YW5jZWQgR3VpZGUnLFxuICAgICAgICAgICdWdWUgMyAtIEJhc2ljIEd1aWRlJyxcbiAgICAgICAgICAnVnVlIDQgLSBUaGUgTXlzdGVyeSdcbiAgICAgICAgXVxuICAgICAgfVxuICAgIH1cbiAgfSxcbiAgY29tcHV0ZWQ6IHtcbiAgICBwdWJsaXNoZWRCb29rc01lc3NhZ2UoKSB7XG4gICAgICByZXR1cm4gdGhpcy5hdXRob3IuYm9va3MubGVuZ3RoID4gMCA/ICdZZXMnIDogJ05vJ1xuICAgIH1cbiAgfVxufVxuPC9zY3JpcHQ+XG5cbjx0ZW1wbGF0ZT5cbiAgPHA+SGFzIHB1Ymxpc2hlZCBib29rczo8L3A+XG4gIDxzcGFuPnt7IGF1dGhvci5ib29rcy5sZW5ndGggPiAwID8gJ1llcycgOiAnTm8nIH19PC9zcGFuPlxuPC90ZW1wbGF0ZT4iLCJpbXBvcnQtbWFwLmpzb24iOiJ7XG4gIFwiaW1wb3J0c1wiOiB7XG4gICAgXCJ2dWVcIjogXCJodHRwczovL3NmYy52dWVqcy5vcmcvdnVlLnJ1bnRpbWUuZXNtLWJyb3dzZXIuanNcIlxuICB9XG59In0=)

Bu yerda biz `publishedBooksMessage` nomli computed property e'lon qildik.

Ilova ichidagi `books` arrayining qiymatini o'zgartirishga harakat qilib ko'ring va  `publishedBooksMessage`ning unga mos ravishda o'zgarayotganini ko'rasiz.

Normal `property`dek, `template`lar ichidagi `computed properties`ga ma'lumotlarni bog'lashingiz mumkin. Vue `this.publishedBooksMessage` `this.author.books`ga bog'liqligidan xabardor, shuning uchun u `this.author.books` o'zgarganda `this.publishedBooksMessage` bilan bog'liq bo'lgan har qanday bog'lanishlarni (bindings) yangilaydi.

Buni ham ko'ring: [Typing Computed Properties](/guide/typescript/options-api.html#typing-computed-properties) <sup class="vt-badge ts" />

</div>

<div class="composition-api">

```vue
<script setup>
import { reactive, computed } from 'vue'

const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

// a computed ref
const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No'
})
</script>

<template>
  <p>Chop etilgan kitoblar:</p>
  <span>{{ publishedBooksMessage }}</span>
</template>
```

[Try it in the Playground](https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHNjcmlwdCBzZXR1cD5cbmltcG9ydCB7IHJlYWN0aXZlLCBjb21wdXRlZCB9IGZyb20gJ3Z1ZSdcblxuY29uc3QgYXV0aG9yID0gcmVhY3RpdmUoe1xuICBuYW1lOiAnSm9obiBEb2UnLFxuICBib29rczogW1xuICAgICdWdWUgMiAtIEFkdmFuY2VkIEd1aWRlJyxcbiAgICAnVnVlIDMgLSBCYXNpYyBHdWlkZScsXG4gICAgJ1Z1ZSA0IC0gVGhlIE15c3RlcnknXG4gIF1cbn0pXG5cbi8vIGEgY29tcHV0ZWQgcmVmXG5jb25zdCBwdWJsaXNoZWRCb29rc01lc3NhZ2UgPSBjb21wdXRlZCgoKSA9PiB7XG4gIHJldHVybiBhdXRob3IuYm9va3MubGVuZ3RoID4gMCA/ICdZZXMnIDogJ05vJ1xufSlcbjwvc2NyaXB0PlxuXG48dGVtcGxhdGU+XG4gIDxwPkhhcyBwdWJsaXNoZWQgYm9va3M6PC9wPlxuICA8c3Bhbj57eyBwdWJsaXNoZWRCb29rc01lc3NhZ2UgfX08L3NwYW4+XG48L3RlbXBsYXRlPiIsImltcG9ydC1tYXAuanNvbiI6IntcbiAgXCJpbXBvcnRzXCI6IHtcbiAgICBcInZ1ZVwiOiBcImh0dHBzOi8vc2ZjLnZ1ZWpzLm9yZy92dWUucnVudGltZS5lc20tYnJvd3Nlci5qc1wiXG4gIH1cbn0ifQ==)

Bu yerda biz `publishedBooksMessage` nomli computed property e'lon qildik. `computed()` funksiyasi qabul qiluvchi funksiyani (getter function) uzatib yuborilishini va qaytgan qiymat **computed ref** bo'lishini kutadi. Normal reflarga o'xshab, siz  `publishedBooksMessage.value`ga bog'langaningiz kabi hisoblangan natijaga (`computed result`ga) ham bog'lana olasiz. `Computed ref`lar ham templatelar ichida avtomatik ochilgan bo'ladi (ya'ni `Proxy` obyektiga o'ralmaydi), shuning uchun siz temlate ifodalar ichida ulardan `.value`siz ham ma'lumot qabul qila olasiz.

`Computed property` avtomatik tarzda o'zining `reactive dependency`larini kuzatib boradi. `Vue` `publishedBooksMessage`ning hisoblanishi `author.books` bilan bog'liqligidan xabardor, shuning uchun u `author.books` o'zgarganda, `publishedBooksMessage` bilan bog'liq bo'lgan har qanday bog'lanishlarni (bindings) yangilaydi.

Buni ham ko'ring: [Typing Computed](/guide/typescript/composition-api.html#typing-computed) <sup class="vt-badge ts" />

</div>

## Computed Caching vs Methods

E'tibor bergan bo'lsangiz, biz metodni, ifoda (expression) ichida chaqirish orqali ham bir xil natijaga erisha olamiz:

```vue-html
<p>{{ calculateBooksMessage() }}</p>
```

<div class="options-api">

```js
// in component
methods: {
  calculateBooksMessage() {
    return this.author.books.length > 0 ? 'Yes' : 'No'
  }
}
```

</div>

<div class="composition-api">

```js
// in component
function calculateBooksMessage() {
  return author.books.length > 0 ? 'Yes' : 'No'
}
```

</div>

`Computed property` o'rniga, xuddi shunday funksiyani metod sifatida ko'rsatishimiz mumkin. So'nggi natija uchun, ikkala yondashuvlar haqiqatan ham bir xil. Ammo, farq shundaki **computed propertylar o'zining reactive dependencylariga asosan keshlanadi.** Computed property uning ba'zi reactive dependencylari o'zgargandagina qayta baholanadi. Bu shuni anglatadiki, `author.books` o'zgarmagunicha,
`publishedBooksMessage`ga bo'lgan bir nechta ulanishlar `getter` funksiyasini ishga tushirmasdan darhol oldingi hisoblangan natijani qaytaradi.

Bu kelayotgan `computed property` hech qachon yangilanmasligini ham anglatadi, chunki `Date.now()` reactive dependency emas:

<div class="options-api">

```js
computed: {
  now() {
    return Date.now()
  }
}
```

</div>

<div class="composition-api">

```js
const now = computed(() => Date.now())
```

</div>

Taqqoslanganda, qayta renderlash sodir bo'lganda metodni chaqirish, **har doim** funksiyani ishga tushiradi.

Bizga keshlash nima uchun kerak? Tasavvur qiling, bizda `list` nomli qimmat computed property bor va u katta arrayni aylanib chiqishni (looping) hamda ko'plab hisoblashlar amalga oshirishni talab qiladi. Keyin bizda o'z navbatida `list`ga bog'liq boshqa computed propertylar bo'lishi mumkin. Keshlashsiz, `list`ning oluvchi funksiyasini (getter) keragidan ortiq darajada yaratayotgan bo'lardik! Keshlashni xohlamagan holatlaringizda, uning o'rniga metoddan foydalaning.

Keyin bizda boshqa hisoblangan xususiyatlar bo'lishi mumkin, ular o'z navbatida "ro'yxat" ga bog'liq.

## Writable Computed

`Computed properties` dastlabki holatda faqat qabul qiluvchi hisoblanadi. Agar `computed property`ga yangi qiymat tayinlashga urinsangiz, ishga tushish vaqtida (runtime) ogohlantirish qabul qilib olasiz. Sizga "yoziladigan" `computed property` zarur bo'lgan kamdan-kam holatlarda, uni `getter` va `setter`ning ikkisi bilan ta'minlash orqali yaratishingiz mumkin:

<div class="options-api">

```js
export default {
  data() {
    return {
      firstName: 'John',
      lastName: 'Doe'
    }
  },
  computed: {
    fullName: {
      // getter
      get() {
        return this.firstName + ' ' + this.lastName
      },
      // setter
      set(newValue) {
        // Note: we are using destructuring assignment syntax here.
        [this.firstName, this.lastName] = newValue.split(' ')
      }
    }
  }
}
```

Endi, qachonki `this.fullName = 'John Doe'`ni ishga tushirganingizda, `setter` chaqirilgan bo'ladi va `this.firstName` hamda `this.lastName` unga mos ravishda yangilanadi.

</div>

<div class="composition-api">

```vue
<script setup>
import { ref, computed } from 'vue'

const firstName = ref('John')
const lastName = ref('Doe')

const fullName = computed({
  // getter
  get() {
    return firstName.value + ' ' + lastName.value
  },
  // setter
  set(newValue) {
    // Note: we are using destructuring assignment syntax here.
    [firstName.value, lastName.value] = newValue.split(' ')
  }
})
</script>
```

Endi, qachonki `fullName.value = 'John Doe'`,ni ishga tushirganingizda, `setter` chaqirilgan bo'ladi va `firstName` hamda `lastName` unga mos ravishda yangilanadi.

</div>

## Best Practices

### Qabul qiluvchi (getters) metodlar nojo'ya ta'sirlarsiz bo'lishi kerak

Buni yodda saqlash muhimki, `computed getter` funksiyalari faqat sof hisoblashni amalga oshirishi va nojo'ya ta'sirlardan xoli bo'lishi kerak. Misol uchun, asinxron so'rovlar qilmang yoki `computed getter` ichida DOMni o'zgartirmang! `Computed property`ni deklarativ tarzda boshqa qiymatlarga asoslangan qiymatni qanday olish kerakligini tasavvur qiling - uning yagona mas'uliyati bu qiymatni hisoblash va qaytarish bo'lishi kerak. Keyinchalik qo'llanmada biz [kuzatuchilar](./watchers) bilan holat o'zgarishiga tashqi tomondan qanday ta'sir qilishimiz mumkinligini muhokama qilamiz.

### Hisoblagan qiymatni o'zgartirishdan saqlaning

`Computed property`dan qaytarilgan qiymat olingan holat hisoblanadi. Buni vaqtinchalik surat sifatida tasavvur qiling - har safar manba holati o'zgarganda, yangi surat yaratiladi. Suratni o'zgartirish ma'nosiz, shuning uchun hisoblangan qaytuvchi qiymat faqat o‘qiladigan (read-only) deb hisoblanishi va hech qachon o'zgarmasligi kerak – buning o‘rniga yangi hisob-kitoblarni ishga tushirish uchun unga bog‘liq bo‘lgan manba holatini yangilang.

The returned value from a computed property is derived state. Think of it as a temporary snapshot - every time the source state changes, a new snapshot is created. It does not make sense to mutate a snapshot, so a computed return value should be treated as read-only and never be mutated - instead, update the source state it depends on to trigger new computations.
