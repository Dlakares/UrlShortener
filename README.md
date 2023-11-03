# Url shortener service
Весь функционал реализован только мной.
Сокращатель ссылок - это API позволяющий отправить длинную ссылку и получить короткую, переход по которой в свою очередь перейти по длинной ссылке.

Данная реализация основна на алгоритме BASE62. Внутри используется асинхронизм для оптимизации работы при высоких нагрузках.

# Cache
[Кэш](https://github.com/Dlakares/UrlShortener/blob/medusa/rustam-BC-6350-url-shortener/src/main/java/faang/school/urlshortenerservice/cache/HashCache.java) используется для хранения заранее сгенерированных хэшей для ссылок. Есть коофицент заполнения по истечению которого начинает генерацию хэшей в отдельном потоке

[Контроллер](https://github.com/Dlakares/UrlShortener/blob/medusa/rustam-BC-6350-url-shortener/src/main/java/faang/school/urlshortenerservice/controller/UrlController.java) как точка входа в приложение. Используется для выдачи ссылок и редиректа по основной ссылке

[Base62Encoder](https://github.com/Dlakares/UrlShortener/blob/medusa/rustam-BC-6350-url-shortener/src/main/java/faang/school/urlshortenerservice/service/Base62Encoder.java) принимает на вход коллекцию чисел и возвращает коллекцию сгенерированных хэшей

[Клинер](https://github.com/Dlakares/UrlShortener/blob/medusa/rustam-BC-6350-url-shortener/src/main/java/faang/school/urlshortenerservice/service/CleanerScheduler.java) очищает устаревшие хэши и возвращает их в базу. Используется конфигурирование параметров

[Генератор хэшей](https://github.com/Dlakares/UrlShortener/blob/medusa/rustam-BC-6350-url-shortener/src/main/java/faang/school/urlshortenerservice/service/HashGenerator.java) получает из бд уникальную последовательность, из которой создаёт хэши и сохраняет в другой таблице.

[Сервис](https://github.com/Dlakares/UrlShortener/blob/medusa/rustam-BC-6350-url-shortener/src/main/java/faang/school/urlshortenerservice/service/UrlService.java) соединяет всю вышеописаную логику вместе.
