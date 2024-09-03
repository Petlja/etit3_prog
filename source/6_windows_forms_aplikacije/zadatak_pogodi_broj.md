# Задатак: Игра погађања замишљеног броја

На форму постави један оквир за текст, једно дугме и једну лабелу. Креирај
игру "ПОГОДИ БРОЈ" за погађање насумично генерисаног броја у интервалу од 1 до 100.

```{image} images/zadatak_pogodi_broj.png
:scale: 100
:align: center
```


## Могуће решење задатка

```cs
using System;
using System.Windows.Forms;

namespace PogodiZamisljenBroj
{
    public partial class Form1 : Form
    {
        private int zamisljeni;
        private Random random;
        public Form1()
        {
            InitializeComponent();
            button1.Text = "Погоди!";
            random = new Random();
            Resetuj();
        }

        private void Resetuj()
        {
            zamisljeni = random.Next(1, 101);
            label1.Text = "Погоди замишљени број између 1 и 100";
            textBox1.Clear();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            int uneti;
            if (int.TryParse(textBox1.Text, out uneti))
            {
                if (uneti < 1 || uneti > 100)
                {
                    label1.Text = "Унеси број између 1 и 100.";
                }
                else if (uneti < zamisljeni)
                {
                    label1.Text = "Погрешно, твој број је мањи од замишљеног.";
                }
                else if (uneti > zamisljeni)
                {
                    label1.Text = "Погрешно, твој број је већи од замишљеног.";
                }
                else
                {
                    label1.Text = "Честитам! Погодиo си број!";
                    MessageBox.Show("Честитам! Погодиo си број!");
                    Resetuj();
                }
            }
            else
            {
                label1.Text = "Унеси валидан број!";
            }
        }
    }
}
```

## Додатни задаци

1. Креирај систем за праћење броја покушаја погађања. Број покушаја треба да
буде приказан у новој лабели на форми.
2. Креирај систем за памћење најбољег резултата - колики је био најмањи број
покушаја када је корисник погодио замишљен број. Најбољи резултат треба да се
памти у бинарном фајлу `rezultat.dat` и приказује у новој лабели на форми са
текстом `Најбољи резултат: n покушаја!`, где `n` представља најбољи резултат.
3. Обради могуће изузетке, нарочито приликом рада са бинарним фајлом.
