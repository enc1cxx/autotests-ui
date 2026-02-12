# Проект по курсу Автоматизация тестирования UI с Python и Playwright. Базовый

## Основы:
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