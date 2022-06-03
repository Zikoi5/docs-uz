# Asinxron komponentlar

## Asosiy foydalanish

Katta ilovalarda ilovani kichikroq qismlarga ajratishimiz va serverdan komponentni faqat kerak bo'lganda yuklashimiz kerak bo'lishi mumkin. Buni amalga oshirish uchun Vue [`defineAsyncComponent`](/api/general.html#defineasynccomponent) funksiyasi mavjud:
```js
import { defineAsyncComponent } from 'vue'

const AsyncComp = defineAsyncComponent(() => {
  return new Promise((resolve, reject) => {
    // ...komponentni serverdan yuklash
    resolve(/* yuklangan komponent */)
  })
})
// ... `AsyncComp` dan oddiy komponent kabi foydalaning
```

Ko'rib turganingizdek, `defineAsyncComponent` Promise qaytaradigan yuklash funksiyasini qabul qiladi. Komponent taʼrifini serverdan olganingizdan soʻng, `Promise` ning `resolve` qayta qoʻngʻiroqlari chaqirilishi kerak. Shuningdek , yuklamaning bajarilmaganligini bildirish uchun `reject(reason)` ga qo'ng'iroq qilishingiz mumkin .

[ES modulining dinamik importi](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#dynamic_imports) ham `Promise` qaytaradi, shuning uchun ko'pincha biz uni `defineAsyncComponent` bilan birgalikda ishlatamiz . Vite va webpack kabi paketlar ham sintaksisni qo'llab-quvvatlaydi, shuning uchun biz Vue SFC-larini import qilish uchun foydalanishimiz mumkin:

```js
import { defineAsyncComponent } from 'vue'

const AsyncComp = defineAsyncComponent(() =>
  import('./components/MyComponent.vue')
)
```

Natijada `AsyncComp` faqat sahifada ko'rsatilganda yuklovchi funktsiyasini chaqiradigan o'rash komponenti paydo bo'ladi. Bundan tashqari, u har qanday rekvizitlar bo'ylab ichki komponentga o'tadi, shuning uchun siz dangasa yuklashga erishib, asl komponentni muammosiz almashtirish uchun asinxron qoplamadan foydalanishingiz mumkin.

<div class="options-api">

Shuningdek siz komponentni [mahalliy sifatida ro'yxatdan o'tkazishda](/guide/components/registration.html#local-registration) `defineAsyncComponent` ham foydalanishingiz mumkin :

```js
import { defineAsyncComponent } from 'vue'

export default {
  // ...
  components: {
    AsyncComponent: defineAsyncComponent(() =>
      import('./components/AsyncComponent.vue')
    )
  }
}
```

</div>

## Yuklash va xato holatlari

Asynchronous operations inevitably involve loading and error states - `defineAsyncComponent()` supports handling these states via advanced options:

```js
const AsyncComp = defineAsyncComponent({
  // yuklovchi funksiyasi
  loader: () => import('./Foo.vue'),

  // Asinxron komponent yuklanayotganda foydalanish uchun komponent
  loadingComponent: LoadingComponent,
  // Yuklash komponentini ko'rsatishdan oldin kechikish. Standart: 200ms.
  delay: 200,

  // Yuklash bajarilmasa, foydalanish uchun komponent
  errorComponent: ErrorComponent,
  // Vaqt tugashi bilan xato komponenti ko'rsatiladi
  // berilgan va oshib ketgan. Default: Infinity.
  timeout: 3000
})
```

Agar yuklash komponenti taqdim etilgan bo'lsa, u birinchi navbatda ichki komponent yuklanayotganda ko'rsatiladi. Yuklash komponenti ko'rsatilishidan oldin sukut bo'yicha 200 ms kechikish mavjud - bu tezkor tarmoqlarda tezkor yuklanish holati juda tez o'zgarishi va miltillash kabi ko'rinishi mumkin.

Agar xato komponenti taqdim etilsa, u yuklovchi funksiyasi tomonidan qaytarilgan va'da rad etilganda ko'rsatiladi. Shuningdek, so'rov juda uzoq davom etsa, xato komponentini ko'rsatish uchun kutish vaqtini belgilashingiz mumkin.

## Suspense bilan foydalanish

Async komponentlari o'rnatilgan komponent bilan `<Suspense>` ishlatilishi mumkin. `<Suspense>` va async komponentlari o'rtasidagi o'zaro ta'sir [`<Suspense>` uchun maxsus bobda](/guide/built-ins/suspense.html) hujjatlashtirilgan.
