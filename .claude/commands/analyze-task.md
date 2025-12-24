{
  "command": {
    "name": "analyze-task",
    "description": "Анализ задачи: поиск неясностей, составление плана реализации",
    "version": "1.0.0"
  },
  "inputs": {
    "taskId": {
      "type": "string",
      "description": "ID задачи (имя файла без .md в tasks/todo/)",
      "source": "$ARGUMENTS"
    }
  },
  "paths": {
    "todo": "tasks/todo/",
    "in_progress": "tasks/in-progress/",
    "done": "tasks/done/",
    "docs": "docs/"
  },
  "steps": [
    {
      "step": 1,
      "name": "validate_task",
      "action": "Проверь что файл tasks/todo/$ARGUMENTS.md существует",
      "on_failure": "Сообщи что задача не найдена и останови выполнение"
    },
    {
      "step": 2,
      "name": "read_task",
      "action": "Прочитай файл задачи tasks/todo/$ARGUMENTS.md",
      "analyze": [
        "Описание задачи",
        "Требования",
        "Ограничения",
        "Критерии приёмки"
      ]
    },
    {
      "step": 3,
      "name": "study_context",
      "action": "Изучи контекст проекта",
      "search": [
        "Найди связанный код в проекте",
        "Посмотри похожие реализации",
        "Проверь документацию в docs/"
      ]
    },
    {
      "step": 4,
      "name": "find_questions",
      "action": "Составь список вопросов и неясностей",
      "check": [
        "Что не определено в ТЗ?",
        "Какие edge cases не описаны?",
        "Есть ли конфликты с существующим кодом?",
        "Какие зависимости нужны?"
      ]
    },
    {
      "step": 5,
      "name": "create_plan",
      "action": "Составь план реализации",
      "include": [
        "Какие файлы создать/изменить",
        "В каком порядке делать изменения",
        "Какие тесты написать"
      ]
    },
    {
      "step": 6,
      "name": "save_analysis",
      "action": "Сохрани анализ в файл",
      "output_file": "tasks/todo/$ARGUMENTS-analysis.md",
      "format": {
        "sections": [
          "## Понимание задачи",
          "## Вопросы к уточнению",
          "## Затрагиваемые файлы",
          "## План реализации",
          "## Риски и edge cases",
          "## Оценка сложности"
        ]
      }
    },
    {
      "step": 7,
      "name": "output_summary",
      "action": "Выведи результат",
      "show": [
        "Краткое саммари задачи",
        "Список вопросов (если есть)",
        "Готовность к реализации (да/нет)"
      ]
    }
  ]
}
