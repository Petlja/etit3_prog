# Квиз: Стрингови

## Питање 4

Дата је декларација једне стринг и једне целобројне променљиве, као и део кода:

```cs
string str = "Primer";
int broj = 66;
Console.WriteLine(str + broj + 65);
Console.WriteLine(broj + 65 + str);
```

```{mchoice}
:answer1: Primer6665 131Primer
:answer2: Primer6665 6665Primer
:answer3: Primer131 131Primer
:answer4: PrimerBA BAPrimer
:correct: 1

Анализирај дати кôд и процени шта ће се приказати на екрану након његовог извршења. Заокружити број испред очекиваног одговора.
```

## Питање 7

Дат је рекурзивни метод који проверава да ли је неки стринг палиндром.

```cs
public static bool palindrom(String s)
{
    if (s.Length <= 1)
    {
        return true; // bazni slučaј
    }
    else
    {
        if (___________________)
        {
            return false;
        }
        else
        {
            return palindrom(s.Substring(1, s.Length - 2));
        }
    }
}
```

```{mchoice}
:answer1: s[0] != s[s.Length - 1]
:answer2: s[0] != s[s.Length]
:answer3: s[1] != s[s.Length - 1]
:answer4: s[1] != s[s.Length]
:correct: 1

Да би кôд био комплетиран потребно је допунити девети ред условом `if` наредбе. Заокружи број испред очекиваног одговора.
```

## Питање 8

Дат је рекурзивни метод који проверава да ли је неки стринг палиндром.

```cs
public static bool Palindrom(String s)
{
    return Palindrom(s, 0, s.Length - 1);
}

public static bool Palindrom(String s, int levi, int desni)
{
    if (desni <= levi)
    {
        return true; // bazni slucaj
    }
    else
    {
        if (s[levi] != s[desni])
        {
            return false;
        }
        else
        {
            return ___________________;
        }
    }
}
```

```{mchoice}
:answer1: Palindrom(s)
:answer2: Palindrom(s, levi, desni)
:answer3: Palindrom(s, levi + 1, desni - 1)
:answer4: Palindrom(s, levi + 1, desni)
:answer5: Palindrom(s, levi, desni - 1)
:correct: 3

Да би кôд био комплетиран потребно је допунити двадесети ред. Заокружи број испред очекиваног одговора.
```
