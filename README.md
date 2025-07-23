# cpp-optional

# Optional<T> — Реализация обёртки для значения

##  Описание

Этот проект реализует шаблонный класс `Optional<T>`, который может либо хранить значение типа `T`, либо быть пустым. Он аналогичен `std::optional` из C++17, но написан с нуля.

##  Содержимое

* `optional.h` — реализация `Optional<T>`.
* `main.cpp` — набор тестов, проверяющих корректность реализации.

## � Компиляция и запуск

```bash
g++ -std=c++20 -Wall -Wextra -pedantic main.cpp -o optional_test
./optional_test
```

Если программа завершилась успешно — значит, все тесты пройдены.

##  Пример использования

```cpp
Optional<std::string> name;
name = "Alice";
if (name.HasValue()) {
    std::cout << name.Value();
}
```

```cpp
std::string user = GetName().Value();
```

##  Особенности реализации

* Собственная безбезопасная реализация хранения с выравниванием (`alignas(T) unsigned char data[sizeof(T)]`)
* Поддержка:

  * Конструкторов копирования и перемещения
  * Операторов присваивания
  * `Emplace`, `Reset`, `HasValue`, `Value`, `*`, `->`
  * Rvalue-qualified доступ (`T&& Value() &&`)
* `BadOptionalAccess` для обработки ошибочного вызова `.Value()`
* Точное учёт конструкций/деструкций в `main.cpp`

##  Тесты

Файл `main.cpp` проверяет:

* Инициализацию, `HasValue`, `Reset`
* Копирование и перемещение
* `Emplace`, `Value`, `*`, `->`
* Сигналы про состояние и количество объектов
* Поведение с rvalue/лефт-ссылками


