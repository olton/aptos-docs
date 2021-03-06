# Повні вузли (FullNodes)

Вузол Aptos — це об’єкт екосистеми Aptos, який відстежує стан блокчейна Aptos. Клієнти взаємодіють з блокчейном через вузли Aptos. Існує два типи вузлів:

+ [Вузли-валідатори (Validator nodes)](basics-validator-nodes.md)
+ Повні вузли (Full nodes)

Кожен вузол Aptos складається з кількох логічних компонентів:

+ [REST service]()
+ [Mempool]()
+ [Consensus (disabled in FullNodes)]()
+ [Execution]()
+ [Virtual Machine]()
+ [Storage]()
+ [State synchronizer]()

Програмне забезпечення [Aptos-core]() можна налаштувати на роботу як вузол-валідатор або як повний вузол.

## Огляд

FullNodes може запускати будь-хто. FullNodes повторно виконує всі транзакції в історії блокчейна Aptos. Повні вузли реплікують весь стан блокчейну шляхом синхронізації з учасниками вище по потоку, наприклад, іншими повними вузлами або вузлами перевірки. Щоб перевірити стан блокчейна, FullNodes отримують набір транзакцій і хеш-корінь накопичувача книги, підписаний валідаторами. Крім того, FullNodes приймають транзакції, надіслані клієнтами Aptos, і пересилають їх безпосередньо (або опосередковано) на вузли перевірки. Хоча FullNodes і валідатори використовують один і той же код, FullNodes не беруть участі в консенсусі.

Сторонні блокчейн-дослідники, гаманці, біржі та DApps можуть запускати локальний FullNode для:

+ Використовувати інтерфейс REST для взаємодії з блокчейном.
+ Отримання послідовного представлення Aptos Ledger.
+ Уникання обмежень швидкості читання.
+ Запуску спеціальної аналітикі на основі історичних даних.
+ Отримання сповіщення про певні події в мережі.

