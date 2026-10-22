# Репорт по работе с CI/CD

### Ссылки на один красный и один исправленный зелёный запуск, коммиты этих запусков.

Вид | Коммит | Запуск
--- | --- | ---
Красный запуск после `break stylesheet link` | коммит: [`f69a9e4`](https://github.com/psengx/cicd-first-run/commit/f69a9e40b2e29b882c056b047fc580605b307371) | [ссылка на запуск](https://github.com/psengx/cicd-first-run/actions/runs/39796899532)
Исправленный зелёный запуск после `restore stylesheet link` | коммит: [`46f384`](https://github.com/psengx/cicd-first-run/commit/846f384462e776cc2e9fb166c27b87c2712dea20) | [ссылка на запуск](https://github.com/psengx/cicd-first-run/actions/runs/39798214959)

### Прогноз до поломки и фактический результат

Прогноз: `test_stylesheet_exists (test_site.SiteTests.test_stylesheet_exists)` - будет НЕ ok

Факт: `test_stylesheet_exists (test_site.SiteTests.test_stylesheet_exists) (href='missing.css') ... FAIL`

### Название упавшего теста и строку причины из журнала

```
FAIL: test_stylesheet_exists (test_site.SiteTests.test_stylesheet_exists) (href='missing.css')
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/home/runner/work/cicd-first-run/cicd-first-run/tests/test_site.py", line 54, in test_stylesheet_exists
    self.assertTrue(bool(href) and (SITE / href).is_file(),
AssertionError: False is not true : Missing stylesheet: missing.css
```
### Что произошло с шагами сборки и сохранения артефакта после ошибки:

На выполнении Run tests процесс отвалился, дальнейшие Build Site, Save site artifact и Post Prepare Python не выполнились. 

### Где выполнялись тесты и почему результат сохранён на GitHub, а не только у вас на компьютере

Тесты выполнялись на удалённых серверах GitHub, которые называются *раннерами*. Результат тестов сохранён на GitHub, потому что GitHub Actions — это независимая облачная система автоматизации (CI/CD)

### Почему зелёный результат после смены аудитории не доказывает отсутствие ошибки:

Результат зелёный, так как тесты пройдены. Тесты пройдены, так как теста, связанного с проверкой аудитории не было. Соответственно некорректность аудитории не является как таковой ошибкой в программе.
