# Домашнее задание к занятию «Система сборки Maven»

## Цели задания

1. Научиться создавать maven-проекты.
2. Научиться писать юнит-тесты с помощью JUnit 5.
3. Научиться использовать maven-плагины.

------

## Инструкция к заданию

1. Скачайте и установите профессиональный редактор кода [Intellij Idea Community Version](https://www.jetbrains.com/idea/download/).
1. :new: Откройте IDEA, [создайте и настройте новый maven-проект](QA_Maven_Idea_Create.md). Под каждую задачу следует создавать отдельный проект, если обратное не сказано в условии.
2. Создайте пустой репозиторий на GitHub и свяжите его с папкой вашего проекта (не с какой-либо другой папкой).
3. :new: Правильно настройте репозиторий в плане `.gitignore`. Проигнорируйте папки `.idea` и `target` (раньше была `out`) и `.iml`-файл — их в репозитории быть не должно.
4. Выполните в IDEA задачу согласно условию.
5. Проверьте соблюдение [правил форматирования кода](QA_Java_Idea_Format.md).
6. :new: Убедитесь, что при запуске `mvn clean test` все тесты запускаются, проходят, а сборка завершается успешно.
7. Закоммитьте и отправьте в репозиторий содержимое папки проекта.

------

## Материалы, которые пригодятся для выполнения задания

1. :new: [Как создать maven-проект в IDEA.](QA_Maven_Idea_Create.md)
1. [Как отформатировать код в Java.](QA_Java_Idea_Format.md)

------

## Задание 1 (обязательное)

Нашей целью будет переделать проект с приложением про бонус с покупки на Maven и его протестировать.

**Шаг 1.** Создайте проект на базе Maven.

**Шаг 2.** Добавьте в проект JUnit Jupiter & Surefire Plugin.

**Шаг 3.** Создайте сервисный класс со следующим исходным кодом:
```java
public class BonusService {
  public long calculate(long amount, boolean registered) {
    int percent = registered ? 3 : 1;
    long bonus = amount * percent / 100;
    long limit = 500;
    if (bonus > limit) {
      bonus = limit;
    }
    return bonus;
  }
}
```

**Шаг 4.** Создайте тестовый класс со следующим исходным кодом:
```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.Assertions;

public class BonusServiceTest {

  @Test
  void shouldCalculateForRegisteredAndUnderLimit() {
    BonusService service = new BonusService();

    // подготавливаем данные:
    long amount = 1000;
    boolean registered = true;
    long expected = 30;

    // вызываем целевой метод:
    long actual = service.calculate(amount, registered);

    // производим проверку (сравниваем ожидаемый и фактический):
    Assertions.assertEquals(expected, actual);
  }

  @Test
  void shouldCalculateForRegisteredAndOverLimit() {
    BonusService service = new BonusService();

    // подготавливаем данные:
    long amount = 1_000_000;
    boolean registered = true;
    long expected = 500;

    // вызываем целевой метод:
    long actual = service.calculate(amount, registered);

    // производим проверку (сравниваем ожидаемый и фактический):
    Assertions.assertEquals(expected, actual);
  }
}
```

**Шаг 5.** Запустите тесты через `mvn clean test`, убедитесь, что они запускаются и проходят.

**Шаг 6.** Проведите поверхностный тест-дизайн сервисного класса, допишите как минимум два недостающих и прямо напрашивающихся теста.

**Шаг 7.** Убедитесь, что тесты запускаются и проходят.

Итого: отправьте на проверку ссылку на репозиторий GitHub с вашим проектом.

------
