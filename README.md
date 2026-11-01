# Тестирование интернет-магазина

[![hexlet-check](https://github.com/yourapology/qa-engineer-js-from-scratch-project-84/actions/workflows/hexlet-check.yml/badge.svg)](https://github.com/yourapology/qa-engineer-js-from-scratch-project-84/actions)

Протестируйте интернет-магазин, и найдите все ошибки

Учебный проект Хекслета: https://ru.hexlet.io/programs/qa-engineer-js-from-scratch
Как это должно работать: https://products-store-ru.hexlet.app

## О проекте

Ручное тестирование учебного интернет-магазина [Hexlet Store](https://products-store.hexlet.app/): каталог и пагинация, карточка и страница товара, поиск, фильтры (категория, бренд, наличие), корзина, оформление заказа, переключение языка (русский / английский). Отдельно проверены нефункциональные требования: работа без перезагрузки страницы, ошибки в консоли и ответы 4xx/5xx, скорость загрузки (3G, Lighthouse), нагрузка на 500 пользователей, HTTPS и XSS, адаптивная вёрстка 375–1920 px и поворот экрана.

**Окружение:** Windows 11 26H2 (сборка 26300.9711), Google Chrome 155.0.8059.80, Firefox 159.0.

## Что тестировалось
Учебный интернет-магазин Hexlet Store: каталог и пагинация, карточка и страница товара, поиск, фильтры (категория, бренд, наличие), корзина, оформление заказа, переключение языка (русский / английский). Отдельно проверены нефункциональные требования: работа без перезагрузки страницы, ошибки в консоли и ответы 4xx/5xx, скорость загрузки (3G, Lighthouse), нагрузка на 500 пользователей (Apache JMeter), HTTPS и XSS, адаптивная вёрстка 375–1920 px и поворот экрана.

### Версии

| Прогон | Версия сайта | Тест-кейсы | Отчёт | Баг-репорты |
|---|---|---|---|---|
| Основной прогон | [<Первая версия>](https://products-store.hexlet.app/) | `test-cases.yaml` | `testing-report.yml` | `bug-reports.yml` |
| Регресс | [<Вторая версия>](https://products-store-v2.hexlet.app/) | `regress-report.yml` | 

### Итоги

| Прогон | Кейсов прогнано | Pass | Fail | Дефектов заведено |
|---|---|---|---|---|
| Основной прогон | 122  | 93 | 29 | 27 |
| Регресс | <…> | <…> | <…> | <…> |

## Стек

- Chrome DevTools и Firefox DevTools — консоль, сеть, эмуляция 3G, Device Toolbar
- Lighthouse 12.8.2 — оценка производительности
- Apache JMeter 5.6.3 (Java) — нагрузочное тестирование
- YAML — требования, тест-кейсы, отчёты и баг-репорты

## Установка

Клонировать репозиторий:

```bash
git clone https://github.com/yourapology/qa-engineer-js-from-scratch-project-84.git
cd qa-engineer-js-from-scratch-project-84
```

Для просмотра тест-кейсов, отчётов и баг-репортов ничего устанавливать не нужно: это YAML-файлы, они открываются в любом редакторе или прямо на GitHub.

Для ручных проверок нужны браузеры:
- Google Chrome 155.0.8059.80 (Lighthouse встроен в DevTools)
- Firefox 159.0

Для повторного запуска нагрузочного теста:
- Java 17 или новее
- [Apache JMeter 5.6.3](https://jmeter.apache.org/download_jmeter.cgi): скачать zip-архив и распаковать рядом с папкой репозитория

Для повторного запуска нагрузочного теста нужны Java и [Apache JMeter 5.6.3](https://jmeter.apache.org/download_jmeter.cgi).

## Использование

### Файлы в репозитории

| Файл / папка | Что внутри |
|---|---|
| `requirements.yml` | требования: функциональные, нефункциональные, неявные (66 шт.) |
| `test-cases.yaml`, `regress-report.yml` | тест-кейсы основного прогона и регресса |
| `testing-report.yml`, `regress-report.yml` | статусы кейсов (pass / fail) по каждому прогону |
| `bug-reports.yml`, `regress-report.yml` | баг-репорты по каждому прогону |
| `load-test.jmx` | план нагрузочного теста для JMeter |
| `Screenshot/` | скриншоты ошибок, на них ссылаются баг-репорты |
| `logs/` | логи нагрузочного теста на 500 пользователей |

### Как читать результаты

1. Требования — `requirements.yml`.
2. Тест-кейсы — `test-cases.yaml` (основной прогон) и `regress-report.yml` (регресс). У каждого кейса в поле `requirement` указано требование из `requirements.yml`.
3. Статусы — `testing-report.yml` и `regress-report.yml`. Названия кейсов в отчётах совпадают с названиями в файлах тест-кейсов.
4. Дефекты — `bug-reports.yml` и `regress-report.yml`. В каждом баг-репорте есть ссылка на скриншот из папки `Screenshot/`.

### Нагрузочный тест

Запуск из корня репозитория (папка `apache-jmeter-5.6.3` необходимо добавить), 500 пользователей, разгон 2 мин, удержание 10 мин:

```bash
java -jar ..\apache-jmeter-5.6.3\bin\ApacheJMeter.jar -n -t load-test.jmx -Jthreads=500 -Jrampup=120 -Jduration=720 -Jsummariser.interval=30 -l logs\results-500-users.jtl -j logs\jmeter-500-users.log -e -o logs\report-500-users
```

Результат: 163 933 запроса, 0% ошибок, 95-й перцентиль — 23 мс. Требование выполнено. HTML-отчёт открывается из `logs/report-500-users/index.html`.

---

<details>
<summary>Автоматические тесты Хекслета</summary>

Тесты запускаются на каждый коммит. За запуск отвечает файл `.github/workflows/hexlet-check.yml` — не удаляйте и не переименовывайте ни его, ни репозиторий.

</details>

## О Хекслете

[Хекслет](https://ru.hexlet.io/) — школа программирования: авторские программы обучения с практикой, поддержкой наставников и реальными проектами, которые остаются в резюме. Этот репозиторий — один из таких проектов.
