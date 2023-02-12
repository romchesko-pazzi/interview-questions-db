# Interview Questions

В данном репозитории находится контент для приложения [Interview Questions](https://it-incubator.io/simulators/interview-questions/info).
Это дружелюбное приложение для обучения разработчиков и подготовки к собеседованию.

Вы можете внести свой вклад в развитие проекта: cтать автором вопроса или теста, исправить ошибки, отправить issue с описанием бага.

### Как внести свой вклад
Ниже приводится инструкция, рассчитанная на новичков в open-source. Ещё более подробную инструкцию можно прочитать [здесь](https://github.com/firstcontributions/first-contributions).

1. Форкни этот репозиторий (в твоём аккаунте появится копия этого репозитория)
2. Склонируй форкнутый репозитория из своего аккаунта к себе на компьютер
3. Создай ветку от ветки develop и внеси в неё необходимые изменения
4. Сделай коммит и запуш свою ветку на GitHub

```git push -u origin your-branch-name```

5. В твоём репозитории на GitHub появится кнопка `Compare & pull request`. С помощью неё отправь пулреквест в ветку develop этого репозитория. В скором времени твои изменения будут приняты!

Не забывай периодически подтягивать изменения из исходного репозитория `git pull upstream develop`

Если возникнут вопросы, можно писать в телеграм: @srStarkov

### Какие вопросы добавлять
Основная цель приложения - подготовка к собеседованию. Поэтому в приложение добавляются вопросы, которые могут прозвучать на собеседовании и проверить глубину знаний. У каждого теста есть уровень сложности - basic, middle, advanced - это ориентировочная оценка сложности входящих в тест вопросов. Условно, это вопросы, которые могут спросить на собеседовании у джуниора, мидла или сеньора.

Приветствуются интересные вопросы из вашей практики, вызывающие желание изучить тему. Будет здорово, если к вопросу будет прикреплено текстовое пояснение, ссылка на статью или видео, раскрывающие его глубину. 

Не следует добавлять элементарные/слишком поверхностные вопросы, которые точно не прозвучат на собеседовании. Например, вопрос "Какое ключевое слово создаёт константу в JavaScript" - плохой вопрос.

Не следует копировать вопросы из тестов со сторонних ресурсов! Обычно эти вопросы слишком элементарны и не подходят для целей Interview Questions.
Формулирование вопросов и ответов помогают упорядочить знания. Также будет здорово, если вопросы будут отражать ваши собственные открытия, которыми вы хотите поделиться :)

Перед добавлением вопроса, стоит ознакомиться с существующими вопросами в данном тесте, чтобы не повториться.

### Как добавить новый вопрос в существующий тест
В тестах может быть любое количество вопросов. Сервер выбирает 10 случайных вопросов для отправки. Можно добавлять вопросы в любой из существующих тестов.

Для каждого теста есть папка (находится в `src/data/tasks`), в которой лежат файлы вопросов в формате json. Создай новый json-файл и добавь туда вопрос в формате описанном ниже.

Пример вопроса без блока кода:
```json
{
  "questionText": "Какое значение не может принимать свойство `position`?",
  "type": "radio",
  "answers": [
    {
      "text": "`static`",
      "isCorrect": false
    },
    {
      "text": "`block`",
      "isCorrect": true
    },
    {
      "text": "`absolute`",
      "isCorrect": false
    },
    {
      "text": "`sticky`",
      "isCorrect": false
    }
  ]
}

```

Пример вопроса с блоком кода и примечанием:
```json
{
  "questionText": "Как можно сделать глубокую копию этого объекта?",
  "type": "checkbox",
  "code": {
    "lang": "js",
    "text": "const user = {\n  name: 'Sonya',\n  age: 28,\n  friends: ['Vasilisa', 'Kate', 'Brendan'],\n}\n\nlet userDeepCopy"
  },
  "answers": [
    {
      "text": "Вручную, используя spread-оператор следующим образом: `{...user, friends: [...user.friends]}`",
      "isCorrect": true
    },
    {
      "text": "Использовать метод Object.assign: `Object.assign(userDeepCopy, user)`",
      "isCorrect": false
    },
    {
      "text": "Использовать методы встроенного JSON-объекта: `JSON.parse(JSON.stringify(user))`",
      "isCorrect": true
    },
    {
      "text": "С помощью WebAPI-метода `structuredClone`",
      "isCorrect": true
    }
  ],
  "author": "YourGitHubName",
  "descriptionMarkup": "Следует помнить, что `Object.assign` и spread-оператор делают неглубокую копию (shallow copy).\n\nИспользовать JSON-методы следует с пониманием ограничений JSON-формата. Например, такая копия лишит объект всех методов (JSON не предусматривает функций).\n\n`structuredClone` - новое браузерное API для глубокого копирования. Почитать о нём можно на [MDN](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone)"
}
```

В созданном json-файле могут быть следующие ключи:
- `questionText` - текст вопроса в формате markdown-строки (подробнее о формате markdown написано ниже). Лучше ограничиться одним параграфом
- `type` - тип вопроса. В данный момент доступны два варианта: `radio` (только один правильный ответ) и `checkbox` (правильных ответов может быть больше одного)
- `code` (опционально) - в вопрос можно добавить блок кода. Значение этого свойства - объект с двумя ключами:
    - `text` - код в виде строки. Для переноса строк можно использовать символ переноса строки `\n`
    - `lang` - язык на котором написан код. Например, `css`, `js`, `jsx`, `html`
- `answers` - массив, содержащий варианты ответа в виде объектов. Каждый ответ содержит два поля:
    - `text` - текст ответа в формате markdown-строки. Не следует превышать 100 символов. Многострочные блоки кода в ответах не используются
    - `isCorrect` - булевое значение (является ли ответ правильным). В зависимости от типа вопроса правильных ответов может быть один или несколько.
- `author` - (опционально) твой ник на GitHub - будет отображаться в приложении вместе с вопросом.
- `descriptionMarkup` - (опционально) - примечание к вопросу в формате markdown-строки. Сюда можно добавить дополнительную информацию, ссылки на статьи или YouTube-видео, объясняющие вопрос или ответ.

Для предпросмотра можно воспользоваться [созданным для этого сервисом](https://interview-questions-preview.vercel.app/).

### Как добавить новый тест
Можно добавлять новые тесты по различным технологиям и на различные темы.
Для этого нужно:
1. Создать новую папку в папке `tasks` (в неё будут добавляться вопросы)
2. Добавить описание теста в массив `exams` (в файле: `src/exams.ts`) в виде объекта:
```ts
  {
    id: 'js-basic', // соответствует названию созданной папки, в которой хранятся вопросы
    title: 'JS Basic',
    category: 'JavaScript', // язык или технология
    level: 'basic', //  'basic' | 'middle' | 'advanced'
    labels: ['frontend', 'backend'] // будут использоваться как теги
  }
```
Новый тест будет добавлен в приложение, как только в нём будет хотя бы 5 вопросов.

### О формате markdown
В json-файлах, описывающих вопросы, используются строки markdown-текста. Markdown - простой язык текстовой разметки, который легко конвертируется в HTML. Ниже представлены примеры использования markdown:
- Ссылки
```markdown
Список [анимируемых CSS-свойств](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties) на MDN.
```
Результат: Список [анимируемых CSS-свойств](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties) на MDN.
- Строки кода
```markdown
Используй `Array.prototype.shift()`
```
Результат: Используй `Array.prototype.shift()`

- Для переноса текста на следующую строку можно использовать `\n\n`
```markdown
Первый параграф. \n\n Второй параграф.
```
Результат:

Первый параграф.

Второй параграф.

Больше примеров использования markdown можно найти [здесь](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet). Впрочем, для составления вопросов в Interview Questions, синтаксиса, продемонстрированного выше, вполне хватит.
