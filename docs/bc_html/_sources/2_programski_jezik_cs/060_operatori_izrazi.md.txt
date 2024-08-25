# Оператори и изрази

Најједноставнији C# изрази су литерали (нпр. цео или реалан број) и имена
променљивих. Њих можеш комбиновати у сложене изразе користећи операторе.
Приоритет и асоцијативност оператора одређују редослед којим се извршавају
операције у изразу. Тај редослед, наметнут приоритетом оператора и
асоцијативношћу, можеш да промениш заградама.

Операторе можеш да примењујеш над подацима различитих уграђених типова.
Слично као у програмском језику C, оператори у програмском језику C# могу се
поделити у групе:

* аритметички оператори,
* оператори једнакости и поређења,
* логички оператори и
* битски оператори.

Ови оператори се могу преоптеретити ако се примењују над кориснички-дефинисаним
типовима података.

## Аритметички оператори

Као и у програмском језику C, аритметички оператори у програмском језику C#
могу бити:

* унарни: инкремент `++`, декремент `--`, плус `+` и минус `-` и
* бинарни: множење `*`, дељење `/`, остатак `%`, сабирање `+` и одузимање `-`.

Њих можеш да користиш над операндима целобројних типова или типова са покретном
тачком. У случају целобројних типова, бинарни оператори и унарни плус и минус
дефинисани су за типове `int`, `uint`, `long` и `ulong`. Ако су операнди типа
`sbyte`, `byte`, `short`, `ushort` или `char`, њихове вредности се прво
конвертују у `int` па се онда извршава операција која даје резултат типа `int`.

У следећим примерима демонстрирана је примена постфиксних и префиксних
оператора инкрементирања и декрементирања...

```cs
int a = 1;
double b = 1.5;

// Postfiksni inkrement operatori
Console.WriteLine(a++);    // 1
Console.WriteLine(b++);    // 1.5
Console.WriteLine(a);      // 2
Console.WriteLine(b);      // 2.5

// Prefiksni inkrement operatori
Console.WriteLine(++a);    // 3
Console.WriteLine(++b);    // 3.5
Console.WriteLine(a);      // 3
Console.WriteLine(b);      // 3.5

// Postfiksni dekrement operatori
Console.WriteLine(a--);    // 3
Console.WriteLine(b--);    // 3.5
Console.WriteLine(a);      // 2
Console.WriteLine(b);      // 2.5

// Prefiksni dekrement operatori
Console.WriteLine(--a);    // 1
Console.WriteLine(--b);    // 1.5
Console.WriteLine(a);      // 1
Console.WriteLine(b);      // 1.5
```

...примена унарних плус и минус оператора...

```cs
int a = 1;
Console.WriteLine(+a);     // 1
Console.WriteLine(a);      // 1
Console.WriteLine(-a);     // -1
Console.WriteLine(a);      // 1
```

...и примена оператора множења, дељења, остатка, сабирања и одузимања:

```cs
int a = 5, b = 2;
double c = 5.5, d = 2.2;
Console.WriteLine(a * b);     // 10
Console.WriteLine(c * d);     // 12.1
Console.WriteLine(a / b);     // 2
Console.WriteLine(c / d);     // 2.5
Console.WriteLine(a % b);     // 1
Console.WriteLine(c % d);     // 1.1
Console.WriteLine(a + b);     // 7
Console.WriteLine(c + d);     // 7.7
Console.WriteLine(a - b);     // 3
Console.WriteLine(c - d);     // 3.3
```

Обрати пажњу да је у програмском језику C# могуће рачунати остатак приликом
дељења и када су операнди реалног типа!

### Сложена додела

Слично као у програмском језику C, аритметички оператори у комбинацији са
оператором доделе чине операторе сложене доделе (енгл. *Compound Assignment*).
То значи да је израз `x op= y` еквивалентан изразу `x = x op y`. У следећем
примеру демонстрирана је примена аритметичких оператора у операторима сложене
доделе:

```cs
int a = 5;
Console.WriteLine(a += 4);    // 9   (5 + 4 = 9)
Console.WriteLine(a -= 4);    // 5   (9 - 4 = 5)
Console.WriteLine(a *= 4);    // 20  (5 * 4 = 20)
Console.WriteLine(a /= 4);    // 5   (20 / 4 = 5)
Console.WriteLine(a %= 4);    // 1   (5 % 4 = 1)
```

## Оператори једнакости и поређења

Оператори једнакости `==` једнако и `!=` неједнако проверавају да ли су њихови
операнди једнаки или не. Овим операторима може да се проверава једнакост
операнада вредносних типова, операнада референтних типова, слогова, стрингова и
делегата. У овој лекцији бавићеш се само једнакошћу операнада вредносних
типова.

Операнди уграђених вредносних типова су једнаки ако су њихове вредности
једнаке, па је резултат операције једнакости `true`. Операнди уграђених
вредносних типова нису једнаки ако су њихове вредности различите, па је
резултат операције једнакости `false`. Важи и обрнуто. Операнди уграђених
вредносних типова су неједнаки ако су њихове вредности различите, па је
резултат операције неједнакости `true`. Операнди уграђених вредносних типова
нису неједнаки ако су њихове вредности једнаке, па је резултат операције
неједнакости `false`. На пример:

```cs
int a = 1, b = 1, c = 2;
Console.WriteLine(a == b);    // True
Console.WriteLine(a == c);    // False
Console.WriteLine(a != b);    // False
Console.WriteLine(a != c);    // True
```

Оператори поређења мање `<`, веће `>`, мање или једнако `<=` и веће или једнако
`>=`, познати и као релациони оператори, пореде вредности операнада целобројног
типа или типа са покретном тачком. У случају операнада знаковног типа пореде се
кодови карактера. На пример:

```cs
int a = 1, b = 2;
Console.WriteLine(a < b);     // True (1 < 2)
Console.WriteLine(a <= b);    // True (1 <= 2)
Console.WriteLine(a > b);     // False (1 > 2)
Console.WriteLine(a >= b);    // False (1 >= 2)
char c = 'a', d = 'A';
Console.WriteLine(c < d);     // False (U+0061 < U+0041)
Console.WriteLine(c <= d);    // False (U+0061 <= U+0041)
Console.WriteLine(c > d);     // True (U+0061 > U+0041)
Console.WriteLine(c >= d);    // True (U+0061 >= U+0041)
```

## Логички оператори

Логички оператори примењују се на логичким операндима. Они могу бити унарни или
бинарни.

Унарни оператор **логичке негације** `!` резултује вредношћу `true` када његов
операнд има вредност `false`, односно вредношћу `false` када његов операнд има
вредност `true`. На пример:

```cs
bool a = true, b = false;
Console.WriteLine(!a);    // False
Console.WriteLine(!b);    // True
```

У случају бинарних оператора **логичке конјукције** (*AND*) `&`,
**логичке дисјункције** (*OR*) `|` и логичке **ексклузивне дисјункције**
(*XOR*) `^`, увек се процењују оба операнда према већ познатим таблицама
истинитости.

| `a`     | `b`     | `a & b` | `a \| b` | `a ^ b`  |
|---------|---------|---------|----------|----------|
| `true`  | `true`  | `true`  | `true`   | `false`  |
| `true`  | `false` | `false` | `true`   | `true`   |
| `false` | `true`  | `false` | `true`   | `true`   |
| `false` | `false` | `false` | `false`  | `false`  |

На пример:

```cs
bool a = true, b = false;
// Konjukcija
Console.WriteLine(a & a);     // True
Console.WriteLine(a & b);     // False
Console.WriteLine(b & a);     // False
Console.WriteLine(b & b);     // False
// Disjunkcija
Console.WriteLine(a | a);     // True
Console.WriteLine(a | b);     // True
Console.WriteLine(b | a);     // True
Console.WriteLine(b | b);     // False
// Ekskluzivna disjunkcija
Console.WriteLine(a ^ a);     // False
Console.WriteLine(a ^ b);     // True
Console.WriteLine(b ^ a);     // True
Console.WriteLine(b ^ b);     // False
```

У случају бинарних оператора **условне логичке конјукције** (*AND*) `&&` и
**условне логичке дисјункције** (*OR*) `||`, десни оператор се процењује само
када је то неопходно.

У случају условне логичке конјукције, десни оператор се не процењује када је
леви оператор `false`. У случају условне логичке дисјункције, десни оператор се
не процењује када је леви оператор `true`. На пример:

```cs
bool DesniTrue()
{
    Console.Write("Procenjuje se. ");
    return true;
}

bool DesniFalse()
{
    Console.Write("Procenjuje se. ");
    return false;
}

bool r1 = true && DesniTrue();
Console.WriteLine(r1);                // Procenjuje se. True
bool r2 = true && DesniFalse();
Console.WriteLine(r2);                // Procenjuje se. False
bool r3 = false && DesniTrue();
Console.WriteLine(r3);                // False
bool r4 = false && DesniFalse();
Console.WriteLine(r4);                // False
bool r5 = true || DesniTrue();
Console.WriteLine(r5);                // True
bool r6 = true || DesniFalse();
Console.WriteLine(r6);                // True
bool r7 = false || DesniTrue();
Console.WriteLine(r7);                // Procenjuje se. True
bool r8 = false || DesniFalse();
Console.WriteLine(r8);                // Procenjuje se. False
```

### Оператори сложене логичке доделе

Бинарни логички оператори `&`, `|` и `^` у комбинацији са оператором доделе
чине операторе сложене доделе - израз `x op= y` еквивалентан је изразу
`x = x op y`. На пример:

```cs
bool a = true;
a &= true;
Console.WriteLine(a);    // True
a |= false;
Console.WriteLine(a);    // True
a ^= true;
Console.WriteLine(a);    // False
```

Бинарни условни логички оператори не подржавају сложену доделу.
