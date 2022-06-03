# Proplar

> Ushbu sahifada siz [Komponentlar asoslari](/guide/essentials/component-basics) ni allaqachon o'qib chiqqansiz deb taxmin qilinadi. Agar siz komponentlar uchun yangi bo'lsangiz, avval [buni](/guide/essentials/component-basics) o'qing.
<div class="options-api">
  <VueSchoolLink href="https://vueschool.io/lessons/vue-3-reusable-components-with-props" title="Free Vue.js Props Lesson"/>
</div>

## Proplar deklaratsiyasi

Vue komponentlari aniq prop deklaratsiyasini talab qiladi, shuning uchun Vue komponentga qanday tashqi proplar yuborilganligi to'g'ridan-to'g'ri atributlar sifatida ko'rib chiqilishi kerakligini biladi (bu uning [maxsus bo'limida](/guide/components/attrs) muhokama qilinadi)

<div class="composition-api">

`<script setup>` qo'llanilgan SFC larda props, `defineProps()` makrosi yordamida e'lon qilish mumkin:

```vue
<script setup>
const props = defineProps(['foo'])

console.log(props.foo)
</script>
```

`<script setup>` bolmagan `component` larda [`props`](/api/options-state.html#props) quyidagicha qo'llaniladi:

```js
export default {
  props: ['foo'],
  setup(props) {
    // setup() birinchi argument sifatida proplarni oladi.
    console.log(props.foo)
  }
}
```

Eslatma: `defineProps()` ga uzatilgan argument `prop` opsiyalari uchun berilgan qiymat bir xil bo'lishiga e'tibor bering: 
bir xil `prop` options API ikki deklaratsiya uslubi o'rtasida taqsimlanadi.

</div>

<div class="options-api">

Proplar [`props`](/api/options-state.html#props) opsiyasi yordamida e'lon qilinadi:

```js
export default {
  props: ['foo'],
  created() {
    // proplarga `this` orqali erishish mumkin
    console.log(this.foo)
  }
}
```

</div>

Satrlar qatori yordamida proplarni e'lon qilishdan tashqari, biz obyekt sintaksisidan ham foydalanishimiz mumkin:

<div class="options-api">

```js
export default {
  props: {
    title: String,
    likes: Number
  }
}
```

</div>
<div class="composition-api">

```js
// <script setup> bo'lgan holda
defineProps({
  title: String,
  likes: Number
})
```

```js
// <script setup> bo'lmagan holda
export default {
  props: {
    title: String,
    likes: Number
  }
}
```

</div>

Obyekt deklaratsiyasi sintaksisidagi har bir xususiyat uchun kalit prop nomi, qiymat esa kutilgan turdagi konstruktor funksiyasi bo'lishi kerak.

Bu nafaqat komponentingizni hujjatlashtiribgina qolmay, balki brauzer konsolida komponentingizdan foydalanayotgan boshqa dasturchilarni, agar ular noto'g'ri turdan o'tgan bo'lsa, ogohlantiradi. [prop validation](#prop-validation) haqida batafsil maʼlumotlarni ushbu sahifada muhokama qilamiz.

<div class="options-api">

See also: [Typing Component Props](/guide/typescript/options-api.html#typing-component-props) 
<sup class="vt-badge ts" />

</div>

<div class="composition-api">

Agar siz TypeScript-da `<script setup>` bilan foydalanayotgan bo'lsangiz, faqat turdagi izohlar yordamida proplarni e'lon qilish ham mumkin:

```vue
<script setup lang="ts">
defineProps<{
  title?: string
  likes?: number
}>()
</script>
``` 

Batafsil ma'lumot: [Komponent proplarini yozish](/guide/typescript/composition-api.html#typing-component-props) <sup class="vt-badge ts" />

</div>

## Propga o'tish tafsilotlari

### Prop Nomlash

Biz camelCase yordamida uzun prop nomlarini e'lon qilamiz, chunki bu ularni xususiyat kalitlari sifatida ishlatishda qo'shtirnoqlardan foydalanishni oldini oladi va ularga to'g'ridan-to'g'ri shablon iboralarida havola qilish imkonini beradi, chunki ular haqiqiy JavaScript identifikatorlaridir:

<div class="composition-api">

```js
defineProps({
  greetingMessage: String
})
```

</div>
<div class="options-api">

```js
export default {
  props: {
    greetingMessage: String
  }
}
```

</div>

```vue-html
<span>{{ greetingMessage }}</span>
```

Texnik jihatdan siz CamelCase-dan bolalar komponentiga proplarni uzatishda ham foydalanishingiz mumkin ([DOM shablonlaridan tashqari](/guide/essentials/component-basics.html#dom-template-parsing-caveats)). Biroq, konventsiya barcha holatlarda HTML atributlari bilan moslashish uchun kabob-case ishlatadi:

```vue-html
<MyComponent greeting-message="hello" />
```

Iloji bo'lsa [komponent teglari uchun PascalCase](/guide/components/registration.html#component-name-casing) dan foydalanamiz , chunki u Vue komponentlarini mahalliy elementlardan farqlash orqali shablonni o'qishni yaxshilaydi. Biroq, proplarni uzatishda camelCase-dan foydalanishning amaliy foydalari unchalik katta emas, shuning uchun biz har bir tilning qoidalariga rioya qilishni tanlaymiz.

### Statik va dinamik Proplar

Hozirgacha siz proplarning statik qiymatlar sifatida uzatilganini ko'rdingiz, masalan:

```vue-html
<BlogPost title="Vue bilan sayohatim" />
```

Shuningdek, siz dinamik ravishda `v-bind` yoki `:` yorlig'i bilan tayinlangan proplarni ko'rgansiz, masalan:

```vue-html
<!-- O'zgaruvchining qiymatini dinamik ravishda tayinlang -->
<BlogPost :title="post.title" />

<!-- Murakkab ifoda qiymatini dinamik ravishda tayinlang -->
<BlogPost :title="post.title + ' by ' + post.author.name" />
```

### Turli xil qiymat turlarini o'tkazish

Yuqoridagi ikkita misolda biz satr qiymatlarini o'tkazamiz, lekin _har qanday_ turdagi qiymat propga o'tkazilishi mumkin.

#### Raqamlar

```vue-html
<!-- Garchi `42` statik bo'lsa ham, Vue-ga buni aytish uchun v-bind kerak -->
<!-- bu satr emas, balki JavaScript ifodasidir. -->
<BlogPost :likes="42" />

<!-- O'zgaruvchining qiymatini dinamik ravishda belgilash. -->
<BlogPost :likes="post.likes" />
```

#### Boolean

```vue-html
<!-- Hech qanday qiymatga ega bo'lmagan propni qo'shish `true`(togri) degan ma'noni anglatadi. -->
<BlogPost is-published />

<!-- Garchi `false` (yolg'on) statik bo'lsa ham, Vue-ga buni aytish uchun `v-bind` kerak -->
<!-- bu satr emas, balki JavaScript ifodasidir. -->
<BlogPost :is-published="false" />

<!-- O'zgaruvchining qiymatini dinamik ravishda belgilash. -->
<BlogPost :is-published="post.isPublished" />
```

#### Massiv

```vue-html
<!-- Massiv statik bo'lsa ham, Vue-ga buni aytish uchun bizga v-bind kerak -->
<!-- bu satr emas, balki JavaScript ifodasidir. -->
<BlogPost :comment-ids="[234, 266, 273]" />

<!-- O'zgaruvchining qiymatini dinamik ravishda belgilash. -->
<BlogPost :comment-ids="post.commentIds" />
```

#### Obyekt

```vue-html
<!-- Obyekt statik bo'lsa ham, Vue-ga buni --> aytish uchun bizga v-bind kerak
<!-- bu satr emas, balki JavaScript ifodasidir. -->
<BlogPost
  :author="{
    name: 'Veronica',
    company: 'Veridian Dynamics'
  }"
 />

<!-- O'zgaruvchining qiymatini dinamik ravishda belgilash. -->
<BlogPost :author="post.author" />
```

### Obyekt yordamida bir nechta xususiyatlarni bog'lash

Agar obyektning barcha xususiyatlarini prop sifatida o'tkazmoqchi bo'lsangiz [`v-bind` argumentsiz](/guide/essentials/template-syntax.html#dynamically-binding-multiple-attributes) ( `v-bind` o'rniga `:prop-name`) foydalanishingiz mumkin. Masalan, post obyekt berilgan:

<div class="options-api">

```js
export default {
  data() {
    return {
      post: {
        id: 1,
        title: 'My Journey with Vue'
      }
    }
  }
}
```

</div>
<div class="composition-api">

```js
const post = {
  id: 1,
  title: 'My Journey with Vue'
}
```

</div>

Quyidagi shablon:

```vue-html
<BlogPost v-bind="post" />
```

Quyidagiga teng bo'ladi:

```vue-html
<BlogPost :id="post.id" :title="post.title" />
```

## Bir tomonlama ma'lumotlar oqimi

Barcha proplar bolalar mulki va ota-ona o'rtasida **bir tomonlama pastga bog'lanish**ni tashkil qiladi: ota-ona xususiyati yangilanganda, u bolaga tushadi, lekin aksincha emas. Bu farzand komponentlarning ota-ona holatini tasodifan oʻzgartirishiga yoʻl qoʻymaydi, bu esa ilovangiz maʼlumotlarini tushunishni qiyinlashtirishi mumkin.

Bundan tashqari, har safar ota-komponent yangilanganda, asosiy komponentdagi barcha proplar eng so'nggi qiymat bilan yangilanadi. Bu degani, siz bolalar komponenti ichidagi tayanchni mutatsiyaga solishga **urinmasligingiz** kerak . Agar shunday qilsangiz, Vue sizni konsolda ogohlantiradi:

<div class="composition-api">

```js
const props = defineProps(['foo'])

// ❌ Ogohlantirish, proplar faqat o'qiladi!
props.foo = 'bar'
```

</div>
<div class="options-api">

```js
export default {
  props: ['foo'],
  created() {
    // ❌ Ogohlantirish, proplar faqat o'qiladi!
    this.foo = 'bar'
  }
}
```

</div>

Odatda propni mutatsiyaga olib keladigan ikkita holat mavjud:

1. **Prop boshlang'ich qiymatni o'tkazish uchun ishlatiladi; bola komponenti undan keyin mahalliy ma'lumotlar xususiyati sifatida foydalanishni xohlaydi.** 
Bunday holda, propni boshlang'ich qiymati sifatida ishlatadigan mahalliy ma'lumotlar xususiyatini aniqlash yaxshidir:

<div class="composition-api">

   ```js
   const props = defineProps(['initialCounter'])

  // hisoblagich dastlabki qiymat sifatida faqat props.initialCounter dan foydalanadi;
  // u kelajakdagi prop yangilanishlaridan uzilgan.
   const counter = ref(props.initialCounter)
  ```
</div>
<div class="options-api">

   ```js
   export default {
     props: ['initialCounter'],
     data() {
       return {
         // hisoblagich faqat this.initialCounter dan dastlabki qiymat sifatida foydalanadi;
         // u kelajakdagi prop yangilanishlaridan uzilgan.
         counter: this.initialCounter
       }
     }
   }
   ```
</div>

2. **Prop o'zgartirilishi kerak bo'lgan xom qiymat sifatida uzatiladi.** Bunday holda, prop qiymatidan foydalangan holda hisoblangan xususiyatni aniqlash yaxshidir:

<div class="composition-api">

   ```js
   const props = defineProps(['size'])

      // prop o'zgarganda avtomatik yangilanadigan hisoblangan xususiyat
   const normalizedSize = computed(() => props.size.trim().toLowerCase())
   ```

</div>
   <div class="options-api">

   ```js
   export default {
     props: ['size'],
     computed: {
       // prop o'zgarganda avtomatik yangilanadigan hisoblangan xususiyat
       normalizedSize() {
         return this.size.trim().toLowerCase()
       }
     }
   }
   ```

   </div>

### O'zgaruvchan obyekt / massiv proplari

Obyektlar va massivlar prop sifatida uzatilsa, bola komponent prop bog'lanishini o'zgartira olmasa, u obyekt yoki massivning ichki xususiyatlarini mutatsiyalashi **mumkin bo'ladi** . Buning sababi, JavaScript-da obyektlar va massivlar havola orqali uzatiladi va bunday mutatsiyalarning oldini olish Vue uchun asossiz qimmatga tushadi.

Bunday mutatsiyalarning asosiy kamchiligi shundaki, u bola komponentiga ota-ona holatiga ota-ona komponentiga aniq bo'lmagan tarzda ta'sir qilish imkonini beradi, bu esa kelajakda ma'lumotlar oqimi haqida fikr yuritishni qiyinlashtiradi. Eng yaxshi amaliyot sifatida, agar ota-ona va bola dizayn bilan mahkam bog'lanmagan bo'lsa, bunday mutatsiyalardan qochishingiz kerak. Ko'pgina hollarda, bola ota-onaga mutatsiyani amalga oshirishga imkon beradigan [hodisani chiqarishi](/guide/components/events.html) kerak.
## Propni Tasdiqlsh/Tekshiruvlar

Komponentlar o'z proplari uchun talablarni belgilashi mumkin, masalan, siz allaqachon ko'rgan turlar. Agar talab bajarilmasa, Vue sizni brauzerning JavaScript konsolida ogohlantiradi. Bu, ayniqsa, boshqalar tomonidan foydalanish uchun mo'ljallangan komponentni ishlab chiqishda foydalidir.

Prop tekshiruvlarni belgilash(miqdorini aniqlash) uchun, siz stringlardan tashkil topgan array o'rniga, <span class="composition-api">`defineProps()` makro</span><span class="options-api">`props` options</span> tekshiruv talablarini qoniqtirgan object(tekshiruv talablariga ega obyekt) bilan ta'minlashingiz mumkin

<div class="composition-api">

```js
defineProps({
  // Asosiy turdagi tekshirish
  //  (`null` va `undefined` qiymatlar har qanday turga ruxsat beradi)
  propA: Number,
  // Bir nechta mumkin bo'lgan turlar
  propB: [String, Number],
  // Majburiy qator
  propC: {
    type: String,
    required: true
  },
  // Standart qiymatga ega raqam
  propD: {
    type: Number,
    default: 100
  },
  // Standart qiymatga ega obyekt
  propE: {
    type: Object,
    // Obyekt yoki massivning standart qiymatlari dan qaytarilishi kerak
    // zavod funktsiyasi. Funktsiya xom ashyoni oladi
    // komponent tomonidan argument sifatida qabul qilingan proplar.
    default(rawProps) {
      return { message: 'hello' }
    }
  },
  // Maxsus tekshiruv funksiyasi
  propF: {
    validator(value) {
      // Qiymat ushbu satrlardan biriga mos kelishi kerak
      return ['success', 'warning', 'danger'].includes(value)
    }
  },
  // Standart qiymatga ega funksiya
  propG: {
    type: Function,
    // Obyekt yoki massivning sukut bo'yicha farqli o'laroq, bu komponent funksiyasi emas - bu standart qiymat sifatida xizmat qiladigan funksiya
    default() {
      return 'Default function'
    }
  }
})
```

:::tip
`defineProps()` argumenti ichidagi kod **`<script setup>` da e'lon qilingan boshqa o'zgaruvchilarga kira olmaydi**, chunki kompilyatsiya qilinganda butun ifoda tashqi funksiya doirasiga o'tkaziladi.
:::

</div>
<div class="options-api">

```js
export default {
  props: {
    // Asosiy turdagi tekshirish
    //  (`null` va `undefined` qiymatlar har qanday turga ruxsat beradi)
    propA: Number,
    // Bir nechta mumkin bo'lgan turlar
    propB: [String, Number],
    // Majburiy qator
    propC: {
      type: String,
      required: true
    },
    // Standart qiymatga ega raqam
    propD: {
      type: Number,
      default: 100
    },
    // Standart qiymatga ega obyekt
    propE: {
      type: Object,
      // Obyekt yoki massivning standart qiymatlari dan qaytarilishi kerak
      // zavod funktsiyasi. Funktsiya xom ashyoni oladi
      // komponent tomonidan argument sifatida qabul qilingan proplar.
      default(rawProps) {
        return { message: 'hello' }
      }
    },
    // Maxsus tekshiruv funksiyasi
    propF: {
      validator(value) {
        // Qiymat ushbu satrlardan biriga mos kelishi kerak
        return ['success', 'warning', 'danger'].includes(value)
      }
    },
    // Standart qiymatge ega funksiya
    propG: {
      type: Function,
      // Obyekt yoki massivning sukut bo'yicha farqli o'laroq, bu komponent funksiyasi emas - bu standart qiymat sifatida xizmat qiladigan funksiya
      default() {
        return 'Default function'
      }
    }
  }
}
```

</div>

Qo'shimcha tafsilotlar:


- Barcha proplar sukut boʻyicha ixtiyoriy, agar `required: true` belgilanmagan boʻlsa.

- `Boolean` dan boshqa mavjud boʻlmagan ixtiyoriy prop `undefined` qiymatga ega boʻladi. 
  
- `Boolean` mavjud bo'lmagan proplar `false` ga o'tkaziladi. Istalgan xatti-harakatni olish uchun siz unga `default` qiymatni o'rnatishingiz kerak.

- Agar `default` qiymat belgilangan boʻlsa, u hal qilingan asos qiymati `undefined` boʻlsa, foydalaniladi – bu prop yoʻq boʻlganda yoki aniq `undefined` qiymat uzatilganda ham kiradi.

Prop tekshiruvi muvaffaqiyatsiz tugagach, Vue konsol ogohlantirishini chiqaradi (agar ishlanma tuzilmasi ishlatilsa).

<div class="composition-api">

Agar [Turga asoslangan prop deklaratsiyasidan](/api/sfc-script-setup.html#typescript-only-features) foydalansangiz , Vue tur izohlarini ekvivalent ish vaqti proplari deklaratsiyasiga jamlashga harakat qiladi. Masalan, `defineProps<{ msg: string }>` ichiga kompilyatsiya qilinadi `{ msg: { type: String, required: true }}`.

</div>
<div class="options-api">

::: tip Eslatma
Esda tutingki, proplar komponent namunasi **yaratilgunga qadar** tekshiriladi, shuning uchun misol xususiyatlari (masalan, `data`, `computed` va h.k.) `default` yoki `validator` funksiyalarida mavjud boʻlmaydi.
:::

</div>

### Ish vaqti tipni tekshirish

Quyidagi `type`lar mahalliy konstruktorlardan biri bo'lishi mumkin:

- `String`
- `Number`
- `Boolean`
- `Array`
- `Object`
- `Date`
- `Function`
- `Symbol`

Bundan tashqari, `type` maxsus sinf yoki konstruktor funksiyasi ham bo'lishi mumkin va tekshirish `instanceof` tekshiruvi bilan amalga oshiriladi. Masalan, quyidagi sinf berilgan:

```js
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName
    this.lastName = lastName
  }
}
```

Siz uni prop turi sifatida ishlatishingiz mumkin:

<div class="composition-api">

```js
defineProps({
  author: Person
})
```

</div>
<div class="options-api">

```js
export default {
  props: {
    author: Person
  }
}
```

</div>

`author` propining qiymati `new Person` bilan yaratilganligini tasdiqlash uchun.

## Boolean Casting

`Boolean` turidagi proplarda mahalliy boolean atributlarning xatti-harakatlariga taqlid qilish uchun maxsus kasting qoidalari mavjud. Quyidagi deklaratsiyaga ega `<MyComponent>` berilgan:

<div class="composition-api">

```js
defineProps({
  disabled: Boolean
})
```

</div>
<div class="options-api">

```js
export default {
  props: {
    disabled: Boolean
  }
}
```

</div>

Komponentdan quyidagi tarzda foydalanish mumkin:

```vue-html
<!-- o'tishga teng :disabled="true" -->
<MyComponent disabled />

<!-- o'tishga teng :disabled="false" -->
<MyComponent />
```

Prop bir nechta turlarga ruxsat berish uchun e'lon qilinganida, masalan.

<div class="composition-api">

```js
defineProps({
  disabled: [Boolean, Number]
})
```

</div>
<div class="options-api">

```js
export default {
  props: {
    disabled: [Boolean, Number]
  }
}
```

</div>

`Boolean` uchun translatsiya qoidalari tashqi koʻrinish tartibidan qatʼiy nazar amal qiladi.
