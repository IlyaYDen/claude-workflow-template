{
  "command": {
    "name": "review",
    "description": "Code review изменений в текущей ветке",
    "version": "1.0.0"
  },
  "steps": [
    {
      "step": 1,
      "name": "get_changes",
      "action": "Получи список изменённых файлов",
      "command": "git diff main...HEAD --name-only"
    },
    {
      "step": 2,
      "name": "view_diff",
      "action": "Посмотри diff изменений",
      "command": "git diff main...HEAD"
    },
    {
      "step": 3,
      "name": "analyze_correctness",
      "action": "Проверь корректность кода",
      "checklist": [
        "Логика работает правильно",
        "Нет очевидных багов",
        "Edge cases обработаны",
        "Нет race conditions (для async кода)"
      ]
    },
    {
      "step": 4,
      "name": "analyze_security",
      "action": "Проверь безопасность",
      "checklist": [
        "Нет SQL/XSS/Command injection",
        "Секреты не захардкожены",
        "Входные данные валидируются",
        "Права доступа проверяются"
      ]
    },
    {
      "step": 5,
      "name": "analyze_quality",
      "action": "Проверь качество кода",
      "checklist": [
        "Понятные имена переменных и функций",
        "Нет дублирования кода",
        "Функции не слишком длинные (< 50 строк)",
        "Соблюдается code style проекта"
      ]
    },
    {
      "step": 6,
      "name": "analyze_performance",
      "action": "Проверь производительность",
      "checklist": [
        "Нет N+1 запросов",
        "Нет утечек памяти",
        "Большие операции не блокируют UI/main thread"
      ]
    },
    {
      "step": 7,
      "name": "analyze_tests",
      "action": "Проверь тесты",
      "checklist": [
        "Новый код покрыт тестами",
        "Тесты проходят",
        "Тесты проверяют edge cases"
      ]
    },
    {
      "step": 8,
      "name": "output_report",
      "action": "Сформируй отчёт",
      "format": {
        "sections": [
          "### Общая оценка (Approved / Needs Changes / Rejected)",
          "### Критические замечания (требуют исправления)",
          "### Рекомендации (желательно исправить)",
          "### Положительные моменты",
          "### Вопросы по коду"
        ]
      }
    },
    {
      "step": 9,
      "name": "next_steps",
      "action": "Предложи следующие шаги",
      "if_issues": "Перечисли что и как исправить",
      "if_approved": "Подтверди готовность к мержу"
    }
  ]
}
