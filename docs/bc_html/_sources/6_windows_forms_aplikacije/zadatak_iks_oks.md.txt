# Задатак: Икс-Окс

На форму динамички постави девет дугмади у матрицу 3×3. Креирај игру Икс-Окс,
тако што ће се у насловној линији форми исписивати који је играч на потезу.
Ако је на потезу играч Х, кликом на неко дугме, текст дугмета мења се у Х и
обрнутно, ако не на потезу играч Y, кликом на неко дугме, текст дугмета мења се
у Y.

![Икс-Окс](./images/iksoks1.png)

Победник (играч који је поставио три своја симбола у ред, колону или дијагоналу
матрице) исписује се у насловној линије форме...

![Икс-Окс](./images/iksoks2.png)

...односно, ако нико није победио, у насловној линије форме исписује се
Нерешено:

![Икс-Окс](./images/iksoks3.png)

## Могуће решење задатка

```cs
using System;
using System.Windows.Forms;

namespace ZadatakIksOks
{
    public partial class Form1 : Form
    {
        private const int dimenzija = 3;
        private Button[,] dugmad;
        private bool igracX;

        public Form1()
        {
            InitializeComponent();
            PocniIgru();
        }

        private void PocniIgru()
        {
            dugmad = new Button[dimenzija, dimenzija];
            igracX = true;
            this.Text = "Игра играч X";
            for (int i = 0; i < dimenzija; i++)
            {
                for (int j = 0; j < dimenzija; j++)
                {
                    dugmad[i, j] = new Button
                    {
                        Width = 100,
                        Height = 100,
                        Location = new System.Drawing.Point(i * 100, j * 100)
                    };
                    dugmad[i, j].Click += new EventHandler(dugmeClick);
                    this.Controls.Add(dugmad[i, j]);
                }
            }
        }

        private void dugmeClick(object sender, EventArgs e)
        {
            Button dugme = sender as Button;
            if (dugme.Text != "")
                return;
            if (igracX)
            {
                dugme.Text = "X";
                this.Text = "Игра играч O";
            }
            else
            {
                dugme.Text = "O";
                this.Text = "Игра играч X";
            }
            igracX = !igracX;
            Proveri();
        }

        private void Proveri()
        {
            for (int i = 0; i < dimenzija; i++)
            {
                if (dugmad[i, 0].Text != "" && dugmad[i, 0].Text == dugmad[i, 1].Text && dugmad[i, 1].Text == dugmad[i, 2].Text)
                {
                    Proglasi(dugmad[i, 0].Text);
                    return;
                }
            }
            for (int j = 0; j < dimenzija; j++)
            {
                if (dugmad[0, j].Text != "" && dugmad[0, j].Text == dugmad[1, j].Text && dugmad[1, j].Text == dugmad[2, j].Text)
                {
                    Proglasi(dugmad[0, j].Text);
                    return;
                }
            }
            if (dugmad[0, 0].Text != "" && dugmad[0, 0].Text == dugmad[1, 1].Text && dugmad[1, 1].Text == dugmad[2, 2].Text)
            {
                Proglasi(dugmad[0, 0].Text);
                return;
            }
            if (dugmad[0, 2].Text != "" && dugmad[0, 2].Text == dugmad[1, 1].Text && dugmad[1, 1].Text == dugmad[2, 0].Text)
            {
                Proglasi(dugmad[0, 2].Text);
                return;
            }
            bool nereseno = true;
            foreach (Button dugme in dugmad)
            {
                if (dugme.Text == "")
                {
                    nereseno = false;
                    break;
                }
            }
            if (nereseno)
            {
                this.Text = "Нерешено!";
            }
        }

        private void Proglasi(string pobednik)
        {
            this.Text = $"Победио је играч {pobednik}";
            foreach (Button dugme in dugmad)
            {
                dugme.Enabled = false;
            }
        }
    }
}
```

## Додатни задатак

1. Осмисли и имплементирај систем за иницијално и поновно покретање игре.
2. У ресурсима учитај слике `X.png` и `O.png` па поправи графички дизајн игре,
тако да се уместо текста, на дугмадима приказују адекватне слике.
3. Покушај да осмислиш и имплементираш алгоритам за исту игру, где корисник
игра против рачунара.
