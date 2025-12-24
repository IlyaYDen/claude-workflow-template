{
  "command": {
    "name": "implement",
    "description": "Реализация задачи согласно подготовленному плану",
    "version": "1.0.0"
  },
  "inputs": {
    "taskId": {
      "type": "string",
      "description": "ID задачи для реализации",
      "source": "$ARGUMENTS"
    }
  },
  "paths": {
    "todo": "tasks/todo/",
    "in_progress": "tasks/in-progress/",
    "done": "tasks/done/"
  },
  "steps": [
    {
      "step": 1,
      "name": "check_files",
      "action": "Проверь наличие файлов задачи",
      "check": [
        "tasks/in-progress/$ARGUMENTS.md",
        "tasks/in-progress/$ARGUMENTS-analysis.md"
      ],
      "if_not_found": {
        "action": "Перемести из todo в in-progress",
        "commands": [
          "mv tasks/todo/$ARGUMENTS.md tasks/in-progress/",
          "mv tasks/todo/$ARGUMENTS-analysis.md tasks/in-progress/"
        ]
      }
    },
    {
      "step": 2,
      "name": "read_plan",
      "action": "Прочитай план реализации из $ARGUMENTS-analysis.md",
      "validate": "Проверь что нет открытых вопросов",
      "on_open_questions": "Сообщи о вопросах и останови выполнение"
    },
    {
      "step": 3,
      "name": "create_branch",
      "action": "Создай git ветку",
      "command": "git checkout -b feature/$ARGUMENTS",
      "optional": true
    },
    {
      "step": 4,
      "name": "implement",
      "action": "Реализуй задачу по плану",
      "rules": [
        "Следуй шагам из analysis.md",
        "Соблюдай code style проекта (см. CLAUDE.md)",
        "Добавляй комментарии только где необходимо"
      ]
    },
    {
      "step": 5,
      "name": "verify",
      "action": "Проверь работоспособность",
      "checks": [
        "Код компилируется/запускается",
        "Существующие тесты проходят",
        "Ничего не сломалось"
      ]
    },
    {
      "step": 6,
      "name": "write_tests",
      "action": "Напиши тесты на новую функциональность",
      "include": [
        "Unit-тесты на новые функции",
        "Integration-тесты если нужно"
      ]
    },
    {
      "step": 7,
      "name": "final_check",
      "action": "Финальная проверка",
      "commands": [
        "npm test (или pytest, ./gradlew test)",
        "npm run lint (или flake8, ktlint)"
      ]
    },
    {
      "step": 8,
      "name": "move_to_done",
      "action": "Перемести задачу в done",
      "commands": [
        "mv tasks/in-progress/$ARGUMENTS.md tasks/done/",
        "mv tasks/in-progress/$ARGUMENTS-analysis.md tasks/done/"
      ]
    },
    {
      "step": 9,
      "name": "output_report",
      "action": "Выведи отчёт о реализации",
      "format": {
        "sections": [
          "### Изменённые файлы",
          "### Новые файлы",
          "### Добавленные тесты",
          "### Как протестировать вручную",
          "### Готово к code review (ветка: feature/$ARGUMENTS)"
        ]
      }
    }
  ]
}
