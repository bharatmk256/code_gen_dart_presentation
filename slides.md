---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: "text-center"
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
---

# Let your machine write code

Using code generation techniques to generate code and get error free code

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

# What is Code generation?

All you do is write repetitive code pattern once and create generator, which generates files with code based on the pattern your defined.

- What are the available solutions 🤔
- Using plugins 💭
- Defining annotations and generating code 👨‍💻

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---


# Kiwi

- Kiwi is an dependency injection tool (service locator)
- It can be used with code generation or without code generation

```dart {all|5|6|9-12|13|all}
abstract class Injector {
  static late KiwiContainer container;

  static void setup() {
    container = KiwiContainer();
    _$Injector()._configure();
  }

  void _configure() {
    _configureMemeFactories();
  }

  @Register.factory(MemeRepo)
  void _configureMemeFactories();
}

```

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

# Kiwi

- Output

```dart
// GENERATED CODE - DO NOT MODIFY BY HAND

part of 'injector.dart';

// **************************************************************************
// KiwiInjectorGenerator
// **************************************************************************

class _$Injector extends Injector {
  @override
  void _configureMemeFactories() {
    final KiwiContainer container = KiwiContainer();
    container
      ..registerFactory((c) => MemeRepo())
  }
}

```

- Using it


```dart
await Injector.resolve<MemeRepo>().getMeme();
```

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

# Freezed

- Freezed generates data class
- Data calss that we get from kotlin

```dart {all|1|3-7|9|all}
@freezed
class Person with _$Person {
  const factory Person({
    required String firstName,
    required String lastName,
    required final int age,
  }) = _Person;

  factory Person.fromJson(Map<String, Object?> json) => _$PersonFromJson(json);
}
```

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

# Freezed

- firstName and lastName are now mutable. As such, we can write:
- age is still immutable, because we explicitly marked the property as final.

```dart
void main() {
  Person person = Person(firstName: 'John', lastName: 'Smith', age: 42);

  person.firstName = 'Mona';
  person.lastName = 'Lisa';

  print(person.copyWith(firstName: 'Dash')); // Person(firstName: Dash, lastName: 'Smith', age: 42)
}
```
<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

# Freezed

- Deep copy

```dart
@freezed
class Company with _$Company {
  factory Company({String? name, required Director director}) = _Company;
}
@freezed
class Director with _$Director {
  factory Director({String? name, Assistant? assistant}) = _Director;
}
@freezed
class Assistant with _$Assistant {
  factory Assistant({String? name, int? age}) = _Assistant;
}
```

```dart
Company company;
Company newCompany = company.copyWith(
  director: company.director.copyWith(
    assistant: company.director.assistant.copyWith(
      name: 'John Smith',
    ),
  ),
);
```

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

# Freezed

```dart
Company company;
Company newCompany = company.copyWith.director.assistant(name: 'John Smith');
```

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>
---

# Json serializable

- Json to Dart

```dart
import 'package:json_annotation/json_annotation.dart';

part 'example.g.dart';

@JsonSerializable()
class Person {
  final String firstName, lastName;
  final DateTime? dateOfBirth;

  Person({
      required this.firstName,
      required this.lastName,
      this.dateOfBirth,
    });

  factory Person.fromJson(Map<String, dynamic> json) => _$PersonFromJson(json);
  Map<String, dynamic> toJson() => _$PersonToJson(this);
}
```

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---


# All the other packages

- There are many other packages are available
  - Mobx (for state management)
  - Injectable (for dependency injection)
  - Retrofit (for https request)
  - Spider (for assets)
  - Hive generator (for daratabse)


<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>
---

<div>
  <h1>Thank You!</h1>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/bharatmk256" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<style>
  div{
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
