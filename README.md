# Проект по курсу Автоматизация тестирования UI с Python и Playwright. Базовый

## Основы:

1. Основа теста
```
from playwright.sync_api import sync_playwright, expect  # Импорт Playwright для синхронного режима и проверки

# Запуск Playwright в синхронном режиме
# Открываем браузер с использованием Playwright
with sync_playwright() as playwright:
    # Запускаем Chromium браузер в обычном режиме (не headless)
    browser = playwright.chromium.launch(headless=False)
    # Создаем новый контекст браузера (новая сессия, которая изолирована от других)
    context = browser.new_context()
    # Открываем новую страницу в рамках контекста
    page = context.new_page()
```

2. Синтаксис ожиданий
```
expect(no_results_description).to_be_visible()
expect(no_results_description).to_have_text('Results from the load test pipeline will be displayed here')
```

3. Запуск из Pytest
```
python -m pytest -k "example"
```
                  
Запустит все тесты, в имени которых есть слово example (например, в файле example_login.py или функции test_example_case).

```
python -m pytest -k "login and not logout"
```
                  
Запустит все тесты, где в имени встречается login, но не logout.

Таким образом, -k используется для выборочного запуска тестов через командную строку, а параметр python_files — для настройки глобальных правил поиска тестовых файлов в pytest.ini.


4. Настройка pytest.ini

```
[pytest]
python_files = *_tests.py test_*.py   # Устанавливает правила для тестовых файлов
python_classes = Test*               # Устанавливает правила для имен классов
python_functions = test_*            # Устанавливает правила для имен функций

```

5. Маркировка тестов
```
import pytest

@pytest.mark.smoke
def test_smoke_case():
    assert 1 + 1 == 2

@pytest.mark.regression
def test_regression_case():
    assert 2 * 2 == 4
```
Здесь smoke и regression — это пользовательские маркировки, с помощью которых можно удобно фильтровать тесты при запуске
Запуск тестов с маркировками smoke и regression:
```
python -m pytest -m "smoke and regression"
```
Запуск тестов с любой из этих маркировок:
```
python -m pytest -m "smoke or regression"
```

Маркировки особенно полезны, если вам нужно управлять большими наборами тестов. Например, можно разделить быстрые и медленные тесты:
```
@pytest.mark.fast
def test_fast():
    pass

@pytest.mark.slow
def test_slow():
    pass
```

Маркировку можно применить к классу:
```
@pytest.mark.smoke
class TestSuite:
    def test_case1(self):
        ...

    def test_case2(self):
        ...
```