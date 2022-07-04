# V9 Передача данных

Убедитесь, что исследуемое приложение соответствует следующим концептуальным требованиям:

* Требует TLS или шифрования, независимо от конфиденциальности обрабатываемой информации.
* Следует последним рекомендациям в части:
  * безопасных конфигураций;
  * предпочтительных алгоритмов и шифров.
* Избегает нестойких или устаревающих алгоритмов и шифров, за исключением крайних случаев.
* Отключает небезопасные алгоритмы и шифры.

В рамках этих требований:

* Будьте в курсе рекомендаций по безопасной конфигурации TLS, поскольку они часто меняется («часто» из-за катастрофических проблем, обнаруживаемых в существующих алгоритмах и шифрах).
* Используйте самые последние версии инструментов анализа конфигурации TLS, чтобы настроить предпочтительный порядок и выбор алгоритмов.
* Периодически проверяйте конфигурацию, чтобы убедиться, что данные передаются надежно и безопасно.

## V9.1 Безопасность подключений со стороны клиента

Убедитесь, что сообщения клиента передаются по зашифрованным каналам с использованием TLS 1.2 или более поздней версии.
Используйте современные инструменты для регулярной проверки конфигурации клиента.

| № | Описание | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **9.1.1** | Убедитесь, что для клиентских подключений используется протокол TLS, и при этом он не оставляет соединения без защиты (незашифрованными или неаутентифицированными). ([C8](https://owasp.org/www-project-proactive-controls/#div-numbering)) | ✓ | ✓ | ✓ | 319 |
| **9.1.2** | С помощью современных инструментов тестирования TLS убедитесь, что включены только стойкие шифронаборы, при этом наиболее стойкие из них выбраны как предпочтительные. | ✓ | ✓ | ✓ | 326 |
| **9.1.3** | Убедитесь, что включены только актуальные и рекомендуемые версии протокола TLS, такие как TLS 1.2 и TLS 1.3. Наиболее свежая версия TLS должна быть выбрана как предпочтительная. | ✓ | ✓ | ✓ | 326 |

## V9.2 Безопасность подключений со стороны сервера

Связь с сервером — это не только HTTP. Также необходимо обеспечить безопасные соединения с другими системами, такими как системы мониторинга, инструменты управления, удаленный доступ и ssh, промежуточное ПО, базы данных, серверы, партнерские или внешние API. Все эти соединения должны быть зашифрованы, чтобы не допустить перехвата информации по принципу «трудно снаружи, но легко внутри».

| № | Описание | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **9.2.1** | Убедитесь, что для подключения к и от сервера используются доверенные сертификаты TLS. Если используются сгенерированные собственным УЦ или самоподписанные сертификаты, то сервер должен быть настроен так, чтобы доверять только утвержденным внутренним центрам сертификации и только указанным самоподписанным сертификатам. Все остальные должны отвергаться. | | ✓ | ✓ | 295 |
| **9.2.2** | Убедитесь, что для всех входящих и исходящих подключений используются зашифрованные соединения, такие как TLS, в том числе для портов управления, мониторинга, аутентификации, вызовов API или web-сервисов, подключений к базам данных, облачным сервисам, бессерверным функциям, серверам, внешних и партнерских подключений. Сервер не должен возвращаться к небезопасным или незашифрованным протоколам. | | ✓ | ✓ | 319 |
| **9.2.3** | Убедитесь, что все зашифрованные соединения с внешними системами, передающие конфиденциальную информацию или функции, аутентифицированы. | | ✓ | ✓ | 287 |
| **9.2.4** | Убедитесь, что включена и настроена процедура отзыва сертификатов, например, Online Certificate Status Protocol (OCSP) Stapling. | | ✓ | ✓ | 299 |
| **9.2.5** | Убедитесь, что сбои TLS-соединений со стороны сервера  регистрируются в журнале. | | | ✓ | 544 |

## Ссылки

Для дополнительной информации см. также:

* [OWASP – TLS Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html)
* [OWASP - Pinning Guide](https://owasp.org/www-community/controls/Certificate_and_Public_Key_Pinning)
* Примечания по рекомендованным режимам TLS:
  * В прошлом ASVS ссылался на стандарт США FIPS 140-2, но рекомендация о применении стандартов США в качестве международных может оказаться трудной в реализации, противоречивой и нелогичной.
  * Лучшим способом достижения соответствия разделу 9.1 будет рассмотрение таких руководств, как [Mozilla's Server Side TLS](https://wiki.mozilla.org/Security/Server_Side_TLS) или [generate known good configurations](https://mozilla.github.io/server-side-tls/ssl-config-generator/), и использование известных и современных инструменты анализа TLS для достижения желаемого уровня безопасности.