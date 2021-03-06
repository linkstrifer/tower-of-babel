У ES6 додано спосіб `for of` ітерації по масиву. Подивімося приклад:

```javascript
var res = [];
// Наступний рядок містить for-of синтаксис.
for (let element of [1, 2, 3]) {
  res.push(element * element);
}
console.log(res); // [1, 4, 9]
```

Отже, яка відмінність від класичного `for` синтаксису? На відміну від `for`, синтаксис `for of` не обмежується масивами. Поки щось можна повторити, поки це "щось" є "ітерабельним", його можна використовувати з `for of`.

Щоб зробити дещо ітерабельним, потрібно використовувати `Symbol.Iterator`. Ось приклад використання `Symbol.Iterator`:

```javascript
// обчислення послідовності Фібоначчі до 1000-го кроку
var fibonacci = {
  // Створіть метод, який має функцію Symbol.iterator.
  [Symbol.iterator]() {
    let pre = 0, cur = 1;
    // Ітерований об'єкт, що обчислює результат, повинен мати метод next:
    return {
      next() {
        // Метод next має повертати об'єкт з властивістю `done`, що вказує, чи виконується ітератор.
        [pre, cur] = [cur, pre + cur];
        if (pre < 1000)  return { done: false, value: pre };
        return { done: true };
      }
    }
  }
}

// Значення значення результату стане `n`.
for (var n of fibonacci) {
  console.log(n);
}
```

# Вправа

Створіть ітерабельний об'єкт, який виконує розрахунок FizzBuzz для заданої кількості чисел.

# Поради

## Задача FizzBuzz

Перерахуйте числа від 1 до максимуму (отриманого за допомогою `process.argv`). Однак для кожного числа, що кратне 3, ви пишете «Fizz», а для кожного числа, кратного 5, ви пишете «Buzz», якщо число, кратне і 3 і 5, ви пишете «FizzBuzz».
Ось приклад.

```javascript
const max = process.argv[2];
let FizzBuzz = {
  [Symbol.iterator]() {
    // Тут знаходиться логіка FizzBuzz
    // Підказка: 
    // Нарпикінці, вам доведеться повернути об'єкт
    // з властивістю `done: true`, але сперршу 
    // вами треба встановити `done: false`
  }
}

for (var n of FizzBuzz) {
  console.log(n);
// 1
// 2
// Fizz
// 4
// Buzz
// Fizz
// 7
// 8
// Fizz
// Buzz
// 11
// Fizz
// 13
// 14
// FizzBuzz
// 16
// 17
// Fizz
// 19
// Buzz
// Fizz
// 22
// 23
// Fizz
// Buzz
// 26
// Fizz
// 28
// 29
// FizzBuzz
// ...
}

```
