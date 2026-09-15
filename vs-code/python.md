# VS Code для работы с Python

Эта заметка описывает базовую настройку Visual Studio Code для Python: отдельный профиль, расширение Python, создание виртуального окружения `.venv`, выбор интерпретатора, установка зависимостей, запуск и отладку программ и настройку Git.

## 1. Что должно быть установлено

Нужны три основных компонента:

1. **Visual Studio Code** — редактор.
2. **Python** — установленный в системе интерпретатор.
3. **Python extension** — расширение VS Code для работы с Python.

Важно различать их:

```text
VS Code
    ↓
Python extension
    ↓
Python interpreter
```

VS Code и расширение Python сами по себе Python не содержат. Интерпретатор устанавливается отдельно.

Проверить установленный Python можно во встроенном терминале:

```powershell
python --version
```

На Windows также полезна команда:

```powershell
py --version
```

---

## 2. Создание отдельного профиля Python

Для Python удобно создать отдельный профиль VS Code.

Открыть:

```text
File → Preferences → Profiles
```

и выбрать:

```text
New Profile
```

Назвать профиль:

```text
Python
```

Есть два разумных варианта.

### Вариант 1. Empty Profile

Создать:

```text
Python
→ Empty Profile
```

и затем самостоятельно установить нужные расширения.

Преимущество — полный контроль над тем, что находится в профиле.

### Вариант 2. Python Profile Template

VS Code также содержит готовый шаблон профиля:

```text
Python
```

Он устанавливает набор настроек и расширений для Python-разработки.

Для минимальной конфигурации удобнее начать с `Empty Profile` и добавить только необходимые расширения.

---

## 3. Установка расширения Python

Находясь в профиле `Python`, открыть Extensions:

```text
Ctrl+Shift+X
```

Найти:

```text
Python
```

Расширение:

```text
Python
Publisher: Microsoft
```

и установить его.

Современная Python-конфигурация VS Code также использует связанные компоненты, в частности:

```text
Pylance
Python Debugger
Python Environments
```

Они обеспечивают соответственно:

* анализ кода и автодополнение;
* отладку;
* управление интерпретаторами, виртуальными окружениями и пакетами.

После установки Python extension VS Code обычно устанавливает необходимые связанные расширения автоматически.

---

## 4. Проект следует открывать как папку

Для Python-проекта лучше создавать отдельную папку, например:

```text
my-project/
```

и открывать в VS Code именно её:

```text
File → Open Folder
```

а не отдельный `.py`-файл.

Так папка становится workspace проекта.

Например:

```text
my-project/
├── .venv/
├── main.py
└── .gitignore
```

В дальнейшем сюда могут добавиться:

```text
my-project/
├── .venv/
├── src/
├── tests/
├── pyproject.toml
├── README.md
└── .gitignore
```

---

## 5. Создание виртуального окружения

Для каждого самостоятельного Python-проекта лучше использовать собственное виртуальное окружение.

В Python sidebar найти:

```text
Environment Managers
```

и нажать:

```text
+
```

VS Code предложит два основных варианта:

```text
Quick Create
Custom Create
```

### Quick Create

Для обычного проекта выбрать:

```text
Quick Create
```

VS Code:

1. использует `venv` как стандартный environment manager;
2. выбирает последнюю доступную версию Python;
3. создаёт окружение:

```text
.venv/
```

в корне workspace;

4. выбирает это окружение для проекта;
5. устанавливает зависимости проекта, если найдены `requirements.txt` или `pyproject.toml`.

Получается:

```text
my-project/
├── .venv/
└── main.py
```

Это хороший вариант по умолчанию для небольшого самостоятельного проекта.

---

## 6. Когда использовать Custom Create

`Quick Create` использует последнюю подходящую установленную версию Python.

Если нужна конкретная версия Python, использовать:

```text
Python: Create Environment
```

через:

```text
Ctrl+Shift+P
```

или выбрать вариант:

```text
Custom Create
```

Затем можно явно указать:

```text
venv
```

и нужный интерпретатор, например:

```text
Python 3.13
Python 3.14
```

Это полезно, если проект должен работать с определённой версией Python.

Например:

```text
проект требует Python 3.13
              ↓
Custom Create
              ↓
Python 3.13
              ↓
.venv/
```

---

## 7. Зачем нужен `.venv`

Виртуальное окружение отделяет зависимости конкретного проекта от глобального Python.

Например:

```text
Project A
└── .venv
    ├── numpy 2.x
    └── scipy

Project B
└── .venv
    ├── numpy 1.x
    └── matplotlib
```

Пакеты одного проекта не вмешиваются в окружение другого.

Поэтому `.venv` относится к проекту логически, но само содержимое `.venv` в Git не сохраняется.

Окружение можно в любой момент пересоздать из описания зависимостей.

---

## 8. Выбор интерпретатора

Текущий Python-интерпретатор отображается в Status Bar VS Code.

Для его изменения можно нажать на указанный там Python или выполнить:

```text
Ctrl+Shift+P
```

и:

```text
Python: Select Interpreter
```

Для проекта с локальным окружением нужно выбрать интерпретатор из:

```text
.venv
```

VS Code обычно обнаруживает workspace-local окружения автоматически и отдаёт `.venv` более высокий приоритет, чем глобальному Python.

Выбранное окружение используется для:

* запуска программы;
* отладки;
* IntelliSense;
* анализа импортов;
* тестирования;
* работы с пакетами.

---

## 9. Терминал и автоматическая активация окружения

После выбора `.venv` открыть новый терминал:

```text
Terminal → New Terminal
```

или:

```text
Ctrl+Shift+`
```

VS Code автоматически активирует выбранное окружение.

В PowerShell приглашение обычно выглядит примерно так:

```powershell
(.venv) PS D:\Projects\my-project>
```

Проверить используемый Python:

```powershell
python --version
```

и его расположение:

```powershell
Get-Command python
```

Путь должен вести внутрь:

```text
my-project\.venv\
```

Для Windows интерпретатор находится примерно здесь:

```text
.venv\Scripts\python.exe
```

---

## 10. Установка пакетов

Пакеты необходимо устанавливать в `.venv`, а не в глобальный Python.

Один вариант — терминал:

```powershell
python -m pip install numpy
```

Например:

```powershell
python -m pip install numpy scipy matplotlib
```

Использование:

```powershell
python -m pip
```

предпочтительнее простого:

```powershell
pip
```

поскольку явно означает:

> запустить `pip`, принадлежащий текущему интерпретатору Python.

Проверить установленные пакеты:

```powershell
python -m pip list
```

---

## 11. Управление пакетами через VS Code

Пакеты можно устанавливать и без терминала.

Открыть:

```text
Python sidebar
→ Environment Managers
```

Найти:

```text
.venv
```

и выбрать:

```text
Manage Packages
```

После этого можно найти нужный пакет, например:

```text
numpy
```

и установить его через интерфейс VS Code.

Терминал и графический интерфейс работают с тем же выбранным окружением.

---

## 12. Первая программа

Создать:

```text
main.py
```

например:

```python
print("Hello, Python!")
```

Запустить можно кнопкой:

```text
Run Python File
```

в правом верхнем углу редактора.

Либо через терминал:

```powershell
python main.py
```

Оба варианта должны использовать выбранный интерпретатор `.venv`.

---

## 13. Отладка

Поставить breakpoint слева от нужной строки кода.

Например:

```python
x = 10
y = 20

result = x + y

print(result)
```

Поставить breakpoint на:

```python
result = x + y
```

и нажать:

```text
F5
```

или:

```text
Run and Debug
```

Для обычного Python-файла VS Code может запустить отладчик без предварительного создания сложной конфигурации.

По умолчанию Python Debugger использует тот же интерпретатор, который выбран для workspace.

Конфигурация:

```text
.vscode/launch.json
```

нужна только тогда, когда запуск требует специальных параметров, переменных среды, аргументов командной строки и т. п.

---

## 14. Зависимости проекта

Сам каталог:

```text
.venv/
```

не переносится между компьютерами.

Вместо этого сохраняется описание зависимостей.

Есть два распространённых подхода.

### requirements.txt

Простой вариант:

```text
requirements.txt
```

Например:

```text
numpy
scipy
matplotlib
```

Установка:

```powershell
python -m pip install -r requirements.txt
```

Можно получить список текущих установленных пакетов:

```powershell
python -m pip freeze > requirements.txt
```

Но `pip freeze` записывает все установленные пакеты окружения, включая косвенные зависимости.

---

## 15. pyproject.toml

Для новых полноценных Python-проектов всё чаще используется:

```text
pyproject.toml
```

Он может содержать:

* metadata проекта;
* минимальную версию Python;
* зависимости;
* настройки инструментов;
* параметры сборки Python package.

Например, концептуально:

```toml
[project]
name = "my-project"
version = "0.1.0"
requires-python = ">=3.13"

dependencies = [
    "numpy",
    "scipy",
]
```

Для небольшого одноразового скрипта `requirements.txt` может быть достаточно.

Для проекта, который развивается как полноценный Python package или приложение, `pyproject.toml` обычно удобнее.

---

## 16. Git

В Git следует сохранять исходный код и описание проекта:

```text
my-project/
├── src/
├── tests/
├── pyproject.toml
├── README.md
├── .gitignore
└── .vscode/
```

Но не само виртуальное окружение:

```text
.venv/
```

Минимальный `.gitignore`:

```gitignore
.venv/
__pycache__/
*.py[cod]
```

Обычно также исключаются:

```gitignore
.pytest_cache/
.mypy_cache/
.ruff_cache/
.coverage
htmlcov/
dist/
build/
*.egg-info/
```

---

## 17. Создание Git-репозитория

Если проект ещё не является Git-репозиторием:

```powershell
git init
```

Проверить:

```powershell
git status
```

Перед первым commit желательно убедиться, что `.venv` действительно игнорируется:

```powershell
git status
```

В списке untracked files не должно быть тысяч файлов из:

```text
.venv/
```

После этого:

```powershell
git add .
git commit -m "Initial project setup"
```

---

## 18. `.venv` не нужно переносить между компьютерами

При клонировании проекта на другой компьютер:

```powershell
git clone ...
cd my-project
```

каталога `.venv` там не будет.

Это нормально.

Нужно открыть проект в VS Code и снова выполнить:

```text
Environment Managers
→ +
→ Quick Create
```

Если в проекте имеется:

```text
requirements.txt
```

или:

```text
pyproject.toml
```

VS Code сможет использовать их при создании окружения.

Идея следующая:

```text
Git хранит:
    код
    конфигурацию
    описание зависимостей

Git не хранит:
    конкретное .venv
```

Каждый компьютер создаёт собственное локальное окружение.

---

## 19. Настройки профиля и настройки проекта

Как и с LaTeX, полезно разделять два уровня.

### Профиль Python

Профиль содержит общие инструменты:

```text
Python extension
Pylance
Python Debugger
Python Environments
```

а также общие пользовательские настройки.

Это конфигурация:

> как я вообще работаю с Python.

### `.vscode/settings.json`

Здесь можно хранить настройки конкретного проекта.

Это конфигурация:

> как VS Code должен работать именно с этим проектом.

Например, современный Python Environments может записывать в workspace настройки environment manager для конкретного Python-проекта без жёстко заданного абсолютного пути к интерпретатору.

Такой `.vscode/settings.json` можно хранить в Git, если его настройки действительно относятся к проекту и полезны на других компьютерах.

---

## 20. Форматирование кода

Форматирование Python в современных версиях VS Code выполняется отдельными formatter extensions.

Например, можно использовать:

```text
Black Formatter
```

или:

```text
autopep8
```

После установки formatter можно назначить его только для Python:

```json
"[python]": {
    "editor.defaultFormatter": "ms-python.black-formatter"
}
```

При желании можно автоматически форматировать файл при сохранении:

```json
"[python]": {
    "editor.defaultFormatter": "ms-python.black-formatter",
    "editor.formatOnSave": true
}
```

Это лучше хранить в профиле Python, если одинаковая политика форматирования используется во всех проектах.

Если конкретный проект требует собственного стиля, настройку лучше хранить на уровне проекта.

---

## 21. Linting

Formatter и linter выполняют разные задачи.

Formatter:

```text
Black
autopep8
```

изменяет оформление кода.

Linter анализирует код и сообщает о потенциальных проблемах.

Современный VS Code использует отдельные расширения для linting; старые настройки вида:

```text
python.linting.*
```

устарели.

Линтер обычно запускается автоматически при открытии или сохранении Python-файла и выводит найденные проблемы в:

```text
Problems
```

открываемый через:

```text
Ctrl+Shift+M
```

На начальном этапе linter и formatter можно вообще не настраивать: Python + Pylance уже дают рабочую среду для написания и выполнения программ.

---

## 22. Тесты

Python extension поддерживает:

```text
unittest
pytest
```

Настроить тестирование можно через:

```text
Python: Configure Tests
```

После этого тесты появляются в:

```text
Testing
```

и могут запускаться или отлаживаться непосредственно из VS Code.

Например:

```text
my-project/
├── src/
│   └── calculations.py
└── tests/
    └── test_calculations.py
```

Для небольших скриптов на начальном этапе отдельная настройка тестирования не обязательна.

---

## 23. Рекомендуемая минимальная структура

Для небольшого проекта:

```text
my-project/
├── .venv/
├── main.py
├── requirements.txt
├── .gitignore
└── README.md
```

Для более серьёзного проекта:

```text
my-project/
├── .venv/
├── src/
│   └── my_project/
│       ├── __init__.py
│       └── main.py
├── tests/
├── pyproject.toml
├── README.md
├── .gitignore
└── .vscode/
    └── settings.json
```

---

## 24. Что не стоит настраивать заранее

VS Code позволяет сразу добавить:

* formatter;
* linter;
* type checker;
* pytest;
* coverage;
* Jupyter;
* Ruff;
* Black;
* launch configurations;
* tasks;
* Dev Containers;
* Poetry;
* uv.

Но для обычного нового проекта всё это сразу не требуется.

Минимальная рабочая схема:

```text
VS Code profile Python
          ↓
Python extension
          ↓
Python Environments
          ↓
project/.venv
          ↓
Python
          ↓
packages
```

Для начала достаточно:

```text
отдельный Python profile
+
Python extension
+
workspace folder
+
.venv
+
Git
```

Остальные инструменты стоит добавлять тогда, когда возникает конкретная потребность.

---

## 25. Быстрая процедура создания нового проекта

Создать папку:

```text
my-project
```

Открыть её в VS Code:

```text
File → Open Folder
```

Убедиться, что выбран профиль:

```text
Python
```

Затем:

```text
Python sidebar
→ Environment Managers
→ +
→ Quick Create
```

Проверить появление:

```text
.venv/
```

Создать:

```text
main.py
```

Создать `.gitignore`:

```gitignore
.venv/
__pycache__/
*.py[cod]
```

Инициализировать Git:

```powershell
git init
```

Проверить:

```powershell
git status
```

После этого проект готов к работе.

---

## 26. Быстрая диагностика

Проверить глобальный Python:

```powershell
python --version
```

Проверить выбранное окружение в новом VS Code terminal:

```powershell
Get-Command python
```

Путь должен указывать на:

```text
.venv\Scripts\python.exe
```

Проверить pip:

```powershell
python -m pip --version
```

Проверить установленные пакеты:

```powershell
python -m pip list
```

Если `.venv` существует, но VS Code использует другой Python:

```text
Ctrl+Shift+P
→ Python: Select Interpreter
→ .venv
```

Если `.venv` не отображается в Environment Managers:

```text
Ctrl+Shift+P
→ Python Environments: Refresh All Environment Managers
```

Полезная модель для диагностики:

```text
Python source
     ↓
VS Code Python extension
     ↓
selected environment
     ↓
.venv
     ↓
Python interpreter
     ↓
installed packages
```
