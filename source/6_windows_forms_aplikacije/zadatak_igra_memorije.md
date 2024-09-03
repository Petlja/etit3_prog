# Задатак: Игра меморије - упари слике

На форму постави једну тајмер контролу и динамички постави 20 дугмади у матрици
димензија 4×5. На дугмадима насумично постави 10 парова емоџија или симбола, на
пример из фонта `Segoe UI Symbol`. Задатак корисника је кликће на парове
дугмади...

```{image} images/emoji1.png
:scale: 100
:align: center
```

...све док не упари свих 10 парова емоџија, тј. симбола:

```{image} images/emoji2.png
:scale: 100
:align: center
```

## Могуће решење задатка

```cs
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Windows.Forms;

namespace ZadatakIgraMemorije
{
    public partial class Form1 : Form
    {
        private Random random = new Random();
        private const int red = 5;
        private const int kol = 4;
        private Button[,] dugmad = new Button[red, kol];
        private List<string> simboli;
        private Button prviKlik = null;
        private Button drugiKlik = null;

        public Form1()
        {
            InitializeComponent();
            PocniIgru();
        }

        private void PocniIgru()
        {
            simboli = new List<string>
            {
                "🙂", "🙂", "🙃", "🙃", "🤡", "🤡", "👻", "👻", "👽", "👽",
                "🐧", "🐧", "🐢", "🐢", "🐵", "🐵", "💋", "💋", "❤", "❤"
            };
            int n = simboli.Count;
            while (n > 1)
            {
                n--;
                int k = random.Next(n + 1);
                string x = simboli[k];
                simboli[k] = simboli[n];
                simboli[n] = x;
            }
            for (int i = 0; i < red; i++)
            {
                for (int j = 0; j < kol; j++)
                {
                    dugmad[i, j] = new Button();
                    dugmad[i, j].Font = new Font("Segoe UI Symbol", 40);
                    dugmad[i, j].Size = new Size(75, 75);
                    dugmad[i, j].Location = new Point(80 * j, 80 * i);
                    dugmad[i, j].Click += Button_Click;
                    dugmad[i, j].Tag = simboli[i * kol + j];
                    dugmad[i, j].Text = "";
                    this.Controls.Add(dugmad[i, j]);
                }
            }
        }

        private void Button_Click(object sender, EventArgs e)
        {
            Button kliknuto = sender as Button;
            if (kliknuto == null || kliknuto.Text != "")
            {
                return;
            }
            if (prviKlik == null)
            {
                prviKlik = kliknuto;
                prviKlik.Text = prviKlik.Tag.ToString();
                return;
            }
            drugiKlik = kliknuto;
            drugiKlik.Text = drugiKlik.Tag.ToString();
            if (prviKlik.Tag.ToString() == drugiKlik.Tag.ToString())
            {
                prviKlik = null;
                drugiKlik = null;
            }
            else
            {
                timer1.Interval = 500;
                timer1.Start();
            }
            Pobednik();
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            timer1.Stop();
            prviKlik.Text = "";
            drugiKlik.Text = "";
            prviKlik = null;
            drugiKlik = null;
        }

        private void Pobednik()
        {
            foreach (Button dugme in dugmad)
            {
                if (dugme.Text == "")
                {
                    return;
                }
            }
            MessageBox.Show("Завршио си игру!", "Честитам!");
        }
    }
}
```

## Додатни задатак

1. Осмисли и имплементирај систем за иницијално и поновно покретање игре.
2. Поправи графички дизајн игре, тако да се уместо емоџија, на дугмадима
приказују адекватне слике учитане у ресурс фајлу.
3. Креирај систем за мерење времена игре и омогући чување и приказ најбољег
резултата.
