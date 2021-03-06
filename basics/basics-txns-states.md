# Транзакції та стани

Дві фундаментальні концепції, що лежать в основі блокчейна Aptos, — це транзакції та стани:
+ Транзакції: трансакції представляють обмін даними (наприклад, Aptos Coins або NFT) між обліковими записами на блокчейні Aptos.
+ Стан: стан (тобто, поточний стан реєстру блокчейну) являє собою знімок блокчейну в його теперішньому вигляді.

Коли транзакція виконується, стан блокчейна Aptos змінюється.

## Транзакції

Коли клієнт Aptos Blockchain надсилає транзакцію, він вимагає оновлення стану книги разом із їхньою транзакцією.

Підписана транзакція в блокчейні містить таку інформацію:

+ Підпис (Signature): відправник використовує цифровий підпис, щоб підтвердити, що він підписав транзакцію (тобто, аутентифікація).
+ Адреса відправника (Sender address): адреса облікового запису відправника.
+ Відкритий ключ відправника (Sender public key): відкритий ключ аутентифікації, який відповідає приватному ключу автентифікації, який використовується для підписання транзакції.
+ Програма (Program): Програма включає:
    + Ім'я модуля та функції Move або сценарій транзакції байт-коду переміщення.
    + Додатковий список введених даних для сценарію. Для однорангової транзакції ці вхідні дані містять інформацію про одержувача та суму, яку йому перераховують.
    + Додатковий список модулів переміщення байт-коду для публікації.
+ Ціна газу (Gas price) (у визначеній валюті/газових одиницях): це сума, яку відправник готовий сплатити за одиницю газу для виконання транзакції. Газ – це спосіб оплати обчислень і зберігання. Газова одиниця — це абстрактне вимірювання обчислень, яке не має притаманної реальної величини.
+ Максимальна кількість газу (Maximum gas amount): максимальна кількість газу – це максимальна кількість газу, яку дозволяється споживати транзакція.
+ Код валюти на газ (Gas currency code): код валюти, який використовується для оплати газу.
+ Порядковий номер (Sequence number): це ціле число без знака, яке має дорівнювати порядковому номеру облікового запису відправника на момент виконання.
+ Час дії: мітка часу, після якої транзакція перестає бути дійсною (тобто закінчується).

## Стан книги (Ledger state)

Стан книги Aptos Blockchain (або глобальний стан) містить стан усіх облікових записів у блокчейні. Кожен вузол валідатора в блокчейні повинен знати глобальний стан останньої версії розподіленої бази даних блокчейну (версійної бази даних), щоб виконати будь-яку транзакцію.

## Версійна база даних

Усі дані в Aptos Blockchain зберігаються в одноверсійній розподіленій базі даних. Номер версії — це 64-розрядне ціле без знака, яке відповідає кількості транзакцій, виконаних системою.

Ця версійна база даних дозволяє вузлам валідатора:
+ Виконувати транзакцію щодо стану книги в останній версії.
+ Відповідати на запити клієнтів щодо історії книги як у поточній, так і в попередніх версіях.

## Зміна стану транзакцій

![](https://aptos.dev/assets/images/transactions-7d6b830b61b1b992811649a3e3ec85de.svg)

FIGURE 1.0 TRANSACTIONS CHANGE STATE

Figure 1.0 represents how executing transaction TN changes the state of the Aptos Blockchain from SN-1 to SN.

+ Accounts A and B - Представляють облікові записи Аліси та Боба в блокчейні Aptos
+ SN-1 - Представляє (N-1)-й стан блокчейну. У цьому стані на рахунку Аліси А є залишок 110 монет Aptos, а на рахунку Боба B — 52 монети Aptos.
+ TN - Це N-та транзакція, виконана в блокчейні. У цьому прикладі він представляє Алісу, яка надсилає Бобу 10 монет Aptos.
+ F - Це детермінована функція. F завжди повертає той самий кінцевий стан для певного початкового стану та конкретної транзакції. Якщо поточний стан блокчейну SN-1, а транзакція TN виконується в стані SN-1, новим станом блокчейну завжди є SN. Блокчейн Aptos використовує мову Move для реалізації детермінованої функції виконання F.
+ SN - Це N-ий стан блокчейну. Коли транзакція TN застосовується до блокчейну, вона генерує новий стан SN (результат застосування F до SN-1 і TN). Це призводить до зменшення балансу рахунку Аліси на 10–100 монет Aptos, а баланс облікового запису Боба – на 10–62 монети Aptos. Новий стан SN показує ці оновлені залишки.

