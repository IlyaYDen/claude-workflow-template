{
  "command": {
    "name": "init-project",
    "description": "Первичный анализ проекта и настройка рабочего окружения",
    "version": "1.0.0"
  },
  "paths": {
    "docs": "docs/",
    "tasks": "tasks/",
    "claude_md": "CLAUDE.md"
  },
  "steps": [
    {
      "step": 1,
      "name": "scan_structure",
      "action": "Изучи структуру проекта",
      "commands": [
        "find . -type f -name '*.js' -o -name '*.ts' -o -name '*.py' -o -name '*.go' -o -name '*.kt' -o -name '*.swift' | head -50",
        "ls -la package.json requirements.txt go.mod build.gradle Cargo.toml 2>/dev/null"
      ]
    },
    {
      "step": 2,
      "name": "detect_stack",
      "action": "Определи стек технологий",
      "detect": [
        "Язык программирования",
        "Фреймворки",
        "База данных",
        "Инструменты сборки"
      ]
    },
    {
      "step": 3,
      "name": "analyze_code",
      "action": "Изучи существующий код",
      "analyze": [
        "Архитектура (MVC, Clean Architecture, etc.)",
        "Паттерны используемые в проекте",
        "Стиль именования",
        "Структура папок"
      ]
    },
    {
      "step": 4,
      "name": "find_docs",
      "action": "Найди документацию",
      "search": [
        "README.md",
        "docs/",
        "Wiki",
        "Комментарии в коде",
        "Swagger/OpenAPI спецификации"
      ]
    },
    {
      "step": 5,
      "name": "find_commands",
      "action": "Найди команды разработки",
      "check": [
        "package.json scripts",
        "Makefile",
        "README.md инструкции"
      ]
    },
    {
      "step": 6,
      "name": "update_claude_md",
      "action": "Обнови файл CLAUDE.md",
      "fill_sections": [
        "Описание проекта",
        "Стек технологий",
        "Структура проекта",
        "Команды разработки",
        "Стиль кода"
      ]
    },
    {
      "step": 7,
      "name": "output_report",
      "action": "Выведи отчёт об анализе",
      "format": {
        "sections": [
          "### Технологии (язык, фреймворк, БД)",
          "### Структура (архитектура)",
          "### Ключевые файлы",
          "### Команды (запуск, тесты, сборка)",
          "### Документация (что есть, чего не хватает)",
          "### Рекомендации"
        ]
      }
    },
    {
      "step": 8,
      "name": "confirm_ready",
      "action": "Подтверди готовность",
      "checks": [
        "CLAUDE.md обновлён",
        "Папки tasks/ существуют",
        "Готов к работе с задачами"
      ]
    }
  ]
}
