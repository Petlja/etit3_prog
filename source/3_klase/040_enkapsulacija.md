# Енкапсулација података

О енкапсулацији података, једном од основних принципа објектно-оријентисаног
програмирања, учио си у лекцији
[Енкапсулација](../1_osnovni_koncepti_oop/04_enkapsulacija.md)
у уводном поглављу. У овој лекцији научићеш како да енкапсулацију конкретно
примениш у програмском језику C#.

У програмском језику C# енкапсулација се реализује коришћењем
**модификатора приступа** (енгл. *Access Modifiers*). Модификаторима приступа
можеш да контролишеш када се члан класе може користити и то:

* у оквиру фајла,
* у оквиру класе,
* у изведеној класи у истом склопу,
* у не-изведеној класи у истом склопу,
* у изведеној класи у другом склопу и
* у не-изведеној класи у другом склопу.

**Склоп** (енгл. *Assembly*) може бити извршни *.exe* фајл или библиотека
динамичких веза тј. *.dll* фајл, настао једним компајлирањем једног или више
изворних C# фајлова, тј. *.cs* фајлова. Постоје следећи модификатори приступа:

* `public`: чланови класе су доступни из било ког дела програма,
* `protected internal`: чланови класе су доступни унутар саме класе, унутар
истог склопа и унутар изведених класа,
* `protected`: чланови класе су доступни унутар саме класе и унутар изведених
класа,
* `internal`: чланови класе су доступни унутар саме класе и унутар истог
склопа,
* `private protected`: чланови класе су доступни унутар саме класе и унутар
изведених класа у истом склопу,
* `private`: чланови класе су доступни унутар саме класе и
* `file`: чланови класе су доступни унутар истог фајла.

Ниво приступачности члановима класа најлакше можеш запамтити путем следеће
табеле:

| Локација                       | `public` | `protected internal` | `protected` | `internal` | `private protected` | `private` | `file` |
|--------------------------------|--------|--------------------|-----------|----------|-------------------|---------|------|
| У фајлу                        | ✔️        | ✔️                    | ✔️           | ✔️          | ✔️                   | ✔️         | ✔️      |
| У класи                        | ✔️        | ✔️                    | ✔️           | ✔️          | ✔️                   | ✔️         | ❌      |
| Изведена класа, исти склоп     | ✔️        | ✔️                    | ✔️           | ✔️          | ✔️                   | ❌         | ❌      |
| Не-изведена класа, исти склоп  | ✔️        | ✔️                    | ❌           | ✔️          | ❌                   | ❌         | ❌      |
| Изведена класа, други склоп    | ✔️        | ✔️                    | ✔️           | ❌          | ❌                   | ❌         | ❌      |
| Не-изведена класа, други склоп | ✔️        | ❌                    | ❌           | ❌          | ❌                   | ❌         | ❌      |

У лекцији [Енкапсулација](../1_osnovni_koncepti_oop/04_enkapsulacija.md) у
уводном поглављу разматран је пример банковног рачуна особе, конкретно, зашто
поље `balans` треба да буде приватно, а методе `priliv_sredstava()`,
`odliv_sredstava()` и `prikazi_balans()` јавне.

```cs
class BankovniRacun
{
    private double balans;

    public void priliv_sredstava(double iznos)
    {
            balans += iznos;
    }

    public bool odliv_sredstava(double iznos)
    {
        if (iznos <= balans)
        {
            balans -= iznos;
            return true;
        }
        return false;
    }

    public double prikazi_balans()
    {
        return balans;
    }
}
```

У класи `Program` дати су једноставни примери коришћења класе `BankovniRacun`:

```cs
class Program
{
    static void Main()
    {
        BankovniRacun PetarPetrovic = new BankovniRacun();

        // Uplata 120.000,00 dinara na račun i prikaz balansa nakon uplate:
        PetarPetrovic.priliv_sredstava(120000.0);
        Console.WriteLine("Uspesna uplata. Trenutno stanje: " + PetarPetrovic.prikazi_balans());
        Console.WriteLine();

        // Neuspeli pokušaj podizanja 150.000,00 dinara sa računa
        bool isplata1 = PetarPetrovic.odliv_sredstava(150000.0);
        if (isplata1)
        {
            Console.WriteLine("Uspesna ispata. Trenutno stanje: " + PetarPetrovic.prikazi_balans());
            Console.WriteLine();
        }
        else
        {
            Console.WriteLine("Neuspesna ispata. Trenutno stanje: " + PetarPetrovic.prikazi_balans());
            Console.WriteLine();
        }

        // Podizanje 100.000,00 dinara sa računa
        bool isplata2 = PetarPetrovic.odliv_sredstava(100000.0);
        if (isplata2)
        {
            Console.WriteLine("Uspesna ispata. Trenutno stanje: " + PetarPetrovic.prikazi_balans());
            Console.WriteLine();
        }
        else
        {
            Console.WriteLine("Neuspesna ispata. Trenutno stanje: " + PetarPetrovic.prikazi_balans());
            Console.WriteLine();
        }
    }
}
```

Прво је креиран нови рачун за корисника Петар Петровић. Потом је извршена
уплата од $120.000,00$ динара на рачун и исписано тренутно стање на рачуну:

```text
Uspesna uplata. Trenutno stanje: 120000
```

Уплата је извршена позивањем јавне методе `priliv_sredstava()` са параметром
`120000,0`. Пошто се метода `priliv_sredstava()` налази у истој класи као и
приватно поље `balans`, метода је приступила и ажурирала вредност поља додајући
вредност `120000`.

Потом се десио неуспели покушај исплате већег износа од износа на рачуну...

```text
Neuspesna ispata. Trenutno stanje: 120000
```

...и успешна исплата $100.000,00$ динара са рачуна.

Да се у класи `Program` десио покушај директнe измене вредности поља `balans`,
на пример...

```cs
PetarPetrovic.balans = 1000000.0;
```

...компајлер би јавио следећу грешку:

```text
Error CS0122 'BankovniRacun.balans' is inaccessible due to its protection level
```

Значи, коришћењем модификатора приступа `private` у класи `BankovniRacun`
забрањен је директан приступ пољу `balans`. Вредност поља `balans` може се
мењати или прочитати само путем дефинисаних метода са модификатором приступа
`public`, онако како је то планирао творац класе `BankovniRacun`.

Користи употребе принципа енкапсулације су прилично јасне:

* **Сигурност података**: Енкапсулација омогућава заштиту осетљивих података од
неовлашћеног приступа и модификације.
* **Контрола над подацима**: Класа може дефинисати правила за приступ и измену
података, чиме се осигурава њихова валидност.
* **Смањивање зависности**: Енкапсулацијом се може смањити зависност између
различитих делова кода, чинећи систем лакшим за одржавање и промене.
* **Апстракција**: Енкапсулација помаже у скривању сложености импленетације од
корисника, пружајући му једноставан интерфејс за интеракцију са класом.
