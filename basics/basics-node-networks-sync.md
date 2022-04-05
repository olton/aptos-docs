# Топологія мережі вузлів

Вузли перевірки (Validator Node) та повні вузли (Full Node) утворюють ієрархічну структуру з вузлами перевірки в корені та повними вузлами скрізь. Блокчейн Aptos розрізняє два типи повних вузлів: повні вузли перевірки та публічні повні вузли. Повні вузли Validator підключаються безпосередньо до вузлів валідатора і пропонують масштабованість разом із пом’якшенням DDoS. Публічні FullNodes підключаються до Validator FullNodes (або інших публічних FullNodes), щоб отримати доступ до мережі Aptos з низькою затримкою.

![](https://aptos.dev/assets/images/v-fn-network-20283e9f73bf516237c0979d969af1db.svg)

## Окремі мережеві стеки

Блокчейн Aptos підтримує різні мережеві стеки для різних мережевих топологій. Наприклад, мережа валідатора не залежить від мережі FullNode. Переваги наявності окремих мережевих стеків включають:
+ Чисте розділення між різними мережами.
+ Покращена підтримка налаштувань безпеки (наприклад, двонаправлена або серверна аутентифікація).
+ Допуск для ізольованих протоколів виявлення (тобто виявлення в ланцюжку для загальнодоступних кінцевих точок вузла перевірки порівняно з ручною конфігурацією для приватних організацій).

## Синхронізація вузлів

Вузли Aptos синхронізуються з останнім станом Aptos Blockchain за допомогою двох механізмів: консенсусу або синхронізації стану. Вузли перевірки будуть використовувати як консенсус, так і синхронізацію стану, щоб залишатися в курсі, тоді як FullNodes використовують лише синхронізацію стану.

Наприклад, вузол валідатора буде викликати синхронізацію стану, коли він вперше підключений до мережі або перезавантажиться (наприклад, після того, як деякий час перебував у автономному режимі). Як тільки валідатор оновить останній стан блокчейну, він почне брати участь у консенсусі та покладатися виключно на консенсус, щоб залишатися в курсі. Однак FullNodes постійно покладається на синхронізацію стану, щоб отримувати й залишатися в курсі по мірі зростання блокчейну.

## Синхронізатор стану

Кожен вузол Aptos містить компонент State Synchronizer, який використовується для синхронізації стану вузла з його аналогами. Цей компонент має однакову функціональність для всіх типів вузлів Aptos: він використовує виділену однорангову мережу для постійного запиту та поширення даних блокчейну. Вузли валідатора розподіляють дані блокчейну в мережі вузлів валідатора, тоді як повні вузли покладаються на інші повні вузли (тобто валідатори або публічні повні вузли).

## API синхронізації

Синхронізатор стану вузла Aptos взаємодіє з синхронізаторами стану інших вузлів, щоб отримувати та надсилати фрагменти транзакцій. Дізнайтеся більше про те, як це працює, у [специфікаціях](https://github.com/aptos-labs/aptos-core/tree/main/documentation/specifications/state_sync).