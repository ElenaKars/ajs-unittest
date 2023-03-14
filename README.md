# Домашнее задание к лекции «Unit-тестирование»

### **Важные моменты** 

1. Каждая задача выполняется в виде отдельного проекта с собственным GitHub-репозиторием.
2. ESLint не должен выдавать ошибок.
3. Jest должен обеспечивать 100-процентное покрытие по строкам для тестируемых функций.
4. Ко всем задачам должен быть подключён AppVeyor и выставлен бейджик статуса.
5. Используйте `import`/`export`, а не `require`.

В качестве шаблона можете использовать [готовый проект](/ci-template).

В личном кабинете на сайте [netology.ru](http://netology.ru/) в поле комментария к домашней работе добавьте ссылки на ваши GitHub-проекты.

## Описание установки

```shell
npm init
# При инициалиализации в качестве тестовой команды указать:
# test command: jest --coverage
npm install --save-dev jest babel-jest @babel/core @babel/cli @babel/preset-env
npm install core-js@3
```

Не забудьте про `.babelrc` и `.browserslistrc`.

В `.babelrc`:
```json
{
  "presets": [["@babel/preset-env", {
    "useBuiltIns": "usage",
    "corejs": 3
  }]]
}
```

Запуск тестов:
```shell
npm test
```

---

## Чистые функции

### Легенда

Во время игры вам нужно будет отображать полоску жизни над игровым персонажем. Для сигнализации пользователю вы решили добавить цветовую индикацию:
- здоровье более 50 — зелёный;
- здоровье от 50 и до 15 — жёлтый;
- здоровье менее 15 — красный.

### Описание

Реализуйте функцию, которая принимает на вход объект в виде:
```javascript
{name: 'Маг', health: 90}
```
И возвращает ответ в виде одной из строк: `healthy`, `wounded`, `critical`.

Сгенерируйте проект на базе `npm`. Подключите туда `jest` и напишите автотесты, которые обеспечивают 100-процентное покрытие вашей функции по строкам.

Убедитесь, что вы обеспечили 100-процентное покрытие тестами.

---

## Matchers

### Легенда

Так как в игре вы можете управлять несколькими героями, то во время битвы нужно, чтобы отображался уровень жизни каждого героя в отсортированном порядке: наверху — самые здоровые. Необходимо сделать это и написать соответствующие автотесты.

### Описание

Дан массив с информацией о героях, например:
```javascript
[
  {name: 'мечник', health: 10},
  {name: 'маг', health: 100},
  {name: 'лучник', health: 80},
]
```
В отсортированном порядке должно выглядеть так:
```javascript
[
  {name: 'маг', health: 100},
  {name: 'лучник', health: 80},
  {name: 'мечник', health: 10},
]
```

Убедитесь, что `toBe` работать не будет, но будет работать `toEqual`. Изучите документацию на [`toBe`]() и [`toEqual`]() и выясните в чём разница (а так же термин Deep Equality). Убедитесь, что вы обеспечили 100 % покрытие тестами по строкам.

Можете дополнительно изучить список доступных Matchers для организации сравнения. Этот список есть на странице [Документация по expect](https://jestjs.io/docs/ru/expect).

---

## Mocking * (задача со звёздочкой)

**Важно: это необязательная задача.**

### Легенда

Вы написали функцию, которая взаимодействует с функцией `fetchData`. Она достаточно тяжёлая, т. к. взаимодействует с удалённым веб-сервером. Вы хотите протестировать свою функцию, в том числе как она обрабатывает ошибки. Чтобы «отвязаться» от этой тяжёлой зависимости, решили использовать механизм mocking.

### Описание

```javascript
// Демо-реализация функции fetchData (модуль http):
export default function fetchData(url) {
  throw new Error('Mock this!');
}
```

```javascript
// Ваша функция:
import fetchData from './http';

export function getLevel(userId) {
  const response = fetchData(`https://server/user/${userId}`);
  
  // TODO: логика обработки
  if (response.status === 'ok') {
     return `Ваш текущий уровень: ${response.level}`; 
  }
  
  return `Информация об уровне временно недоступна`;
}
```

Сделайте моки для функции `fetchData` и напишите тесты так, чтобы обеспечить 100-процентное покрытие тестами функции `getLevel` по строкам.

**Обратите внимание**: вам нужно писать тесты для функции `getLevel`.