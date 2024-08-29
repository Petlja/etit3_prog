# Задатак: Будилник

На форму постави једну лабелу, два оквира за текст и једно дугме. У лабели увек
треба да се приказује тренутно време. У оквире за текст корисник треба да унесе
сате и минуте када жели да се пробуди.

```{image} images/zadatak_budilnik1.png
:scale: 100
:align: center
```


Кликом на дугме, ако је исправно унето време буђења, активира се аларм.

```{image} images/zadatak_budilnik2.png
:scale: 100
:align: center
```
У наведено време, аларм се активира приказивањем поруке.

```{image} images/zadatak_budilnik3.png
:scale: 100
:align: center
```

## Могуће решење задатка

```cs
using System;
using System.Windows.Forms;

namespace ZadatakBudilnik
{
    public partial class Form1 : Form
    {
        private bool ukljucen = false;
        private int sati;
        private int minuti;

        public Form1()
        {
            InitializeComponent();
            timer1.Interval = 1000;
            timer1.Start();
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            DateTime sada = DateTime.Now;
            label1.Text = sada.ToString("HH:mm:ss");

            if (ukljucen && sada.Hour == sati && sada.Minute == minuti)
            {
                ukljucen = false;
                button1.Text = "Укључи аларм!";
                MessageBox.Show("Пробуди се!");
            }
        }

        private void button1_Click(object sender, EventArgs e)
        {
            if (ukljucen)
            {
                ukljucen = false;
                button1.Text = "Укључи аларм!";
            }
            else
            {
                if (int.TryParse(textBox1.Text, out sati) && int.TryParse(textBox2.Text, out minuti))
                {
                    ukljucen = true;
                    button1.Text = "Искључи аларм";
                }
                else
                {
                    MessageBox.Show("Унеси исправно број сати и минута!");
                }
            }
        }
    }
}
```

## Додатни задатак

1. Омогући да се на форми, поред времена, приказује и данашњи датум.
2. Омогући да се аларм покреће одређеног датума у одређено време.
3. Омогући да уместо приказивања поруке, аларм покреће одређену апликацију на
рачунару.
