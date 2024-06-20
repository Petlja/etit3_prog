# Позивање конструктора базне класе

Конструктор изведене класе позива конструктор своје базне класе помоћу кључне
речи `new`. На пример, ако је дефинисана базна класа `BaznaKlasa` овако...

```cs
class BaznaKlasa
{
    public BaznaKlasa(string ime)
    {
        //
    }
}
```

...онда у изведеној класи `IzvedenaKlasa`, конструктор базне класе треба да
дефинишеш овако:

```cs
class IzvedenaKlasa : BaznaKlasa
{
    public IzvedenaKlasa(string ime) : base (ime)
    {
        //
    }
}
```

Ако то не урадиш доћи ће до грешке:

```text
CS7036: There is no argument given that corresponds to the required parameter 'ime' of 'BaznaKlasa.BaznaKlasa(string)'
```

С друге стране, ако базна класа има дефинисан јавни подразумевани конструктор,
на пример овако...

```cs
class BaznaKlasa
{
    public BaznaKlasa() { }
}
```

...а ти у изведеној класи дефинишеш јавни подразумевани конструктор овако...

```cs
class IzvedenaKlasa : BaznaKlasa
{
    public IzvedenaKlasa() { }
}
```

...компајлер ће сам "кришом" допунити твој кôд у изведеној класи овако...

```cs
class IzvedenaKlasa : BaznaKlasa
{
    public IzvedenaKlasa() : base() { }
}
```

...и неће доћи до грешке.

Класа `System.Object` има јавни подразумевани конструктор, па нема потребе да
га позиваш помоћу `: base()` нити да размишљаш о томе - компајлер ће то увек
урадити сам за тебе.

Кључну реч `base` можеш користити и приликом позивања метода или приступа
својствима и индексерима базне класе. О овоме ћеш учити касније.
