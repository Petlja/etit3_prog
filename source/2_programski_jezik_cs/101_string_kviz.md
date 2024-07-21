# Квиз: Стрингови

## Питање 1

Дата је декларација једне стринг и једне целобројне променљиве, као и део кода:

```cs
string str = "Rec";
int num = 12;
Console.Write(str + num + 12 + " ");
Console.WriteLine(num + 12 + str);
```

```{mchoice}
:answer1: Rec1212 24Rec
:answer2: Rec1212 1212Rec
:answer3: Rec24 24Rec
:answer4: Rec24 1212Rec
:correct: 1

Анализирај дати кôд и процени шта ће се исписати у конзоли након његовог
извршења. Означи очекивани одговор.
```

## Питање 2

```{mchoice}
:answer1: String.Equals()
:answer2: String.Distinguish()
:answer3: String.Compare()
:answer4: String.CompareTo()
:answer5: String.Differentiate()
:correct: "1,3,4"

Које се од наведених метода НЕ користе за поређење вредности типа `String`?
Штиклирај тачне одговоре.
```

## Питање 3

Дат је следећи део кода:

```cs
int a = 2, b = 1, c = 0;
string str = $"{a}{b}{c}";
Console.WriteLine(str);
```

```{mchoice}
:answer1: abc
:answer2: 012
:answer3: 210
:answer4: 3
:correct: 3

Анализирај дати кôд и процени шта ће се исписати у конзоли након његовог
извршења. Означи очекивани одговор.
```

## Питање 4

Дата је декларација једне стринг и једне целобројне променљиве, као и део кода:

```cs
string str = "2E-2";
double num = str.Length;
Console.WriteLine(num);
```

```{mchoice}
:answer1: 0.02
:answer2: 4
:answer3: 4.000000
:answer4: 8
:correct: 2

Анализирај дати кôд и процени шта ће се исписати у конзоли након његовог
извршења. Означи очекивани одговор.
```

## Питање 5

```{mchoice}
:answer1: Методу `String.Merge()`.
:answer2: Методу `String.Concat()`.
:answer3: Методу `String.Strcat()`.
:answer4: Оператор `+`.
:correct: 2,4

Шта од понуђеног можеш користити за спајање два стринга? Штиклирај тачне
одговоре.
```
