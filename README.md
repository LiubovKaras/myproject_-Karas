# NATASHA мы ничего не уронили
## 
*Как работает библиотека Natasha и как она пригодится культурологам*

**Проект выполнили: Мария Константинова, Татьяна Шишкина, Любовь Карась**
![картинка](https://www.meme-arsenal.com/memes/1e9fba4eb538ab18e0e17cdf346eac91.jpg)

Библиотека Natasha решает базовые задачи обработки  русского языка:
сегментация на токены и предложения;
морфологический и синтаксический анализ;
лемматизация;
извлечение;
нормализация именованных сущностей.

То есть вы можете мзвлечь из текста определенные слова, даты, адреса, суммы денег.На вход программному модулю дается текст, а на выходе получаются структурированные объекты. Например, вы выделяете в романе сущности (места, героев, военные звания, даты и так далее). Natasha решает задачу лемматизации, использует Pymorphy2 и результаты морфологического разбора. 

**Пример использования**
```{python}
from natasha import NamesExtractor
from natasha.markup import show_markup, show_json

extractor = NamesExtractor()

text = '''
Благодарственное письмо   Хочу поблагодарить учителей моего, теперь уже бывшего, одиннадцатиклассника:  Бушуева Вячеслава Владимировича и Бушуеву Веру Константиновну. Они вовлекали сына в интересные внеурочные занятия, связанные с театром и походами.

Благодарю прекрасного учителя 1"А" класса - Волкову Наталью Николаевну, нашего наставника, тьютора - Ларису Ивановну, за огромнейший труд, чуткое отношение к детям, взаимопонимание! Огромное спасибо!
'''
matches = extractor(text)
spans = [_.span for _ in matches]
facts = [_.fact.as_json for _ in matches]
show_markup(text, spans)
show_json(facts)

>>> Благодарственное письмо   Хочу поблагодарить учителей моего, теперь уже бывшего, одиннадцатиклассника:  [[Бушуева Вячеслава Владимировича]] и [[Бушуеву Веру Константиновну]]. Они вовлекали сына в интересные внеурочные занятия, связанные с театром и походами.

Благодарю прекрасного учителя 1"А" класса - [[Волкову Наталью Николаевну]], нашего наставника, тьютора - [[Ларису Ивановну]], за огромнейший труд, чуткое отношение к детям, взаимопонимание! Огромное спасибо!

[
  {
    "first": "вячеслав",
    "middle": "владимирович",
    "last": "бушуев"
  },
  {
    "first": "вера",
    "middle": "константиновна",
    "last": "бушуева"
  },
  {
    "first": "наталья",
    "middle": "николаевна",
    "last": "волкова"
  },
  {
    "first": "лариса",
    "middle": "ивановна"
  }
]
```

*Краткая инструкция по использованию библиотеки*:

1. Призвать Наташу: from Natasha import NamesExtractor / Address xtractor / Dates xtractor / MoneyExtractor (на выбор)

2. Ввести текст text = '''уронили'''

3. matches = extractor(text)

**Наши коды**
1. Ссылка [тут](https://colab.research.google.com/drive/1Va82LNm7SlZOfLztYafGbbLY1J0C6c0Z)

Что здесь сделано: 
посчитано количество токенов;
посчитано количество предложений;
проведен грамматический анализ (посчитано, сколько существительных, глаголов, прилагательных),
определены наиболее повторяющиеся даты и посчитано их количество. 

2. И еще один пример [тут](https://colab.research.google.com/drive/16WeE0Nl_elYoCLtb9zWeEtRmddIumRA-?usp=sharing)



Что здесь сделано: 

текст разделен на токены и предложения;
каждый токен лемматизирован;
извлечены сущности (выделены локации, персоны).

Natasha объединяет под одним интерфейсом другие библиотеки проекта. Для решения практических задач стоит использовать их напрямую:

[Razdel](https://github.com/natasha/razdel)— сегментация текста на предложения и токены;

[Navec](https://github.com/natasha/navec) — качественный компактные эмбеддинги;

[Slovnet](https://github.com/natasha/slovnet) — современные компактные модели для морфологии, синтаксиса, NER;

[Yargy](https://github.com/natasha/yargy) — правила и словари для извлечения структурированной информации;

[Ipymarkup](https://github.com/natasha/ipymarkup) — визуализация NER и синтаксической разметки.

## 
Выводы
Благодаря библиотеке Natasha мы можем обработать большой массив текста, а именно: провести грамматический анализ, вычленять даты, имена, локации, суммы денег. 


