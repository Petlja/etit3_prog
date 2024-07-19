# Квиз: Низови

## Питање 1

```{mchoice}
:answer1: int niz = new int(30);
:answer2: double[ ] niz = new double[30];
:answer3: int[ ] niz = { 3, 4, 3, 2 };
:answer4: char[ ] niz = new char[ ];
:answer5: char[ ] niz = new char { 'a', 'b', 'c', 'd' };
:answer6: char[ ] niz = new char[ ] { 'a', 'b' };
:correct: 2,3,6

Штиклирај исправно написане наредбе за декларацију низа.
```

## Питање 2

Дат је следећи кôд програма који формира и штампа елементе низа `а`:

```cs
namespace TestPrimer
{
    class Program
    {
        static void Main(string[] args)
        {
            int[] a = new int[5];
            for (int i = 0; i < a.Length; i++) a[i] = i;
            Console.Write(a[i] + " ");
        }
    }
}
```

```{mchoice}
:answer1: Програм у конзоли исписује бројеве 0 1 2 3 4.
:answer2: Програм има грешку, јер ће у последњој наредби Console.Write методa Main покушати приступ непостојећем елементу а[5].
:answer3: Програм у конзоли исписује број 5.
:answer4: Програм има грешку, јер променљива i у последњој наредби Console.Write у методу Main неће имати дефинисану вредност.
:correct: 4

Анализирај дати кôд и процени шта ће се догодити након његовог извршавања.
Означи очекивани одговора.
```

## Питање 3

Дата је декларација променљиве и низа:

```cs
int k;
int[ ] brojevi = {5, 12, 37, 7, 27, 33, 36};
```

```cs
k = Array.BinarySearch(brojevi, 37);
```

```{mchoice}
:answer1: k=0, јер метод BinarySearch прво изврши сортирање низа у опадајућем редоследу, па онда тражи задату вредност.
:answer2: метод BinarySearch баца изузетак увек када је низ неуређен и програм "пуца".
:answer3: k=2, јер се тражени елемент налази на позицији 2.
:answer4: k добија неочекивану вредност, јер низ мора бити сортиран у растућем поретку пре позива методе BinarySearch.
:answer5: k=6, јер метод BinarySearch прво изврши сортирање низа у растућем редоследу, па онда тражи задату вредност.
:correct: 4

На основу дате декларације одреди шта је резултат позива. Означи очекивани
одговор.
```

## Питање 4

Дати су делови кода који треба да рачунају збир елемената матрице `a`,
декларисане на следећи начин: `int[,] a = new int[10, 10]`.

```cs
// Предлог 1:
int sum = 0;
for (int i = 0; i < a.Length; i++)
    for (int j = 0; j < a[i].Length; j++)
        sum += a[i][j];

// Предлог 2:
int sum = 0;
foreach (int x in a)
    sum += x;

// Предлог 3:
int sum = 0;
for (int i = 0; i < a.GetLength(0); i++)
    for (int j = 0; j < a.GetLength(1); j++)
        sum += a[i, j];

// Предлог 4:
int sum = 0;
foreach (int[] vrsta in a)
    foreach (int el in vrsta)
        sum += el;
```

```{mchoice}
:answer1: Предлог 1.
:answer2: Предлог 2.
:answer3: Предлог 3.
:answer4: Предлог 4.
:correct: 2,3

Анализирај и проценити који је од предлога тачан. Штиклирај очекиване
одговоре.
```

## Питање 5

Дата је рекурзивна метода за бинарно претраживање сортираног целобројног низа.

```cs
public static int TraziBroj(int[] niz, int broj)
{
    return TraziBroj(niz, broj, 0, niz.Length - 1);
}

public static int TraziBroj(int[] niz, int broj, int levi, int desni)
{
    if (levi > desni)
    {
        return -1; // broj nije nadjen u nizu
    }
    int sredina = (levi + desni) / 2;
    if (broj < niz[sredina])
    {
        return TraziBroj(niz, broj, levi, sredina - 1);
    }
    else if (broj > niz[sredina])
    {
        return ______________________________;
    }
    else
    {
        return sredina;
    }
}
```

```{mchoice}
:answer1: TraziBroj(niz, broj, sredina + 1, levi)
:answer2: TraziBroj(niz, broj, sredina - 1, levi)
:answer3: TraziBroj(niz, broj, desni, sredina + 1)
:answer4: TraziBroj(niz, broj, sredina + 1, desni)
:correct: 4

Да би кôд био комплетиран потребно је допунити деветнаести ред. Означи
очекивани одговор.
```
