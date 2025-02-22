---
title: CSS счётчики
slug: Web/CSS/CSS_counter_styles/Using_CSS_counters
tags:
  - CSS
  - CSS счётчики
  - вложенные счётчики
translation_of: Web/CSS/CSS_Lists_and_Counters/Using_CSS_counters
original_slug: Web/CSS/CSS_Lists_and_Counters/Using_CSS_counters
---

{{CSSRef}}

CSS счётчики, в своей сущности, переменные CSS, значения которых могут быть инкрементированы при помощи CSS для отслеживания количества их использования. Они позволяют регулировать внешний вид контента, основываясь на его местоположении в документе. CSS счётчики реализованы в CSS 2.1 ([ссылка на спецификацию](https://www.w3.org/TR/CSS21/generate.html#counters)).

Значение счётчика сбрасывается (инициализируется) при помощи {{cssxref("counter-reset")}}.

{{cssxref("counter-increment")}} может быть отображён на странице, используя функцию `counter()` или counters() в свойстве {{cssxref("content")}}.

## Использование счётчиков

Для того, чтобы использовать CSS счётчики, сначала необходимо сбросить их значение (0 по умолчанию). Для того, чтобы отобразить значение счётчика - используйте функцию `counter()`. Следующий пример прибавляет в начале каждого h3 элемента "Section <_значение счётчика_>:".

```css
body {
  counter-reset: section;                     /* Устанавливает значение
                                                 счётчика, равным 0 */
}

h3::before {
  counter-increment: section;                 /* Инкрементирует счётчик*/
  content: "Секция " counter(section) ": ";   /* Отображает текущее
                                                 значение счётчика */
}
```

Пример:

```html
<h3>Вступление</h3>
<h3>Основная часть</h3>
<h3>Заключение</h3>
```

{{EmbedLiveSample("Использование_счётчиков", 200, 150)}}

## Вложенные счётчики

CSS счётчики могут быть очень полезны для создания нумерованных списков, потому что новая сущность CSS счётчика автоматически создаётся в дочерних элементах. Используя функцию `counters(), можно вставить строку между разными уровнями вложенных счётчиков. Пример:`

```css
ol {
  counter-reset: section;           /*Создаёт новый счётчик для каждого
                                      тега <ol>*/
  list-style-type: none;
}

li::before {
  counter-increment: section;      /*Инкрементируется только счётчик
                                     текущего уровня вложенности*/
  content: counters(section,".") " ";/*Добавляем значения всех уровней
                                    вложенности, используя разделитель '.'*/
                                   /*Если необходима поддержка < IE8,
                                      необходимо убедиться, что после
                                      разделителя ('.') не стоит пробел*/
}
```

Объединим с данным HTML:

```html
<ol>
  <li>item</li>          <!-- 1     -->
  <li>item               <!-- 2     -->
    <ol>
      <li>item</li>      <!-- 2.1   -->
      <li>item</li>      <!-- 2.2   -->
      <li>item           <!-- 2.3   -->
        <ol>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
        </ol>
        <ol>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
          <li>item</li>  <!-- 2.3.3 -->
        </ol>
      </li>
      <li>item</li>      <!-- 2.4   -->
    </ol>
  </li>
  <li>item</li>          <!-- 3     -->
  <li>item</li>          <!-- 4     -->
</ol>
<ol>
  <li>item</li>          <!-- 1     -->
  <li>item</li>          <!-- 2     -->
</ol>
```

Результат:

{{EmbedLiveSample("Вложенные_счётчики", 250, 350)}}

## Спецификации

| Specification                                                                        | Status                           | Comment            |
| ------------------------------------------------------------------------------------ | -------------------------------- | ------------------ |
| {{SpecName("CSS3 Lists", "#auto-numbering", "CSS Counters")}}     | {{Spec2("CSS3 Lists")}} | No change          |
| {{SpecName("CSS2.1", "generate.html#counters", "CSS Counters")}} | {{Spec2("CSS2.1")}}         | Initial definition |

## Смотрите также

- {{cssxref("counter-reset")}}
- {{cssxref("counter-increment")}}
