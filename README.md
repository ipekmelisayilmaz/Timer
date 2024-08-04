# WindowsFormsApp12
# Windows Forms Timer Örneği

Bu, bir zamanlayıcı kullanımı gösteren basit bir C# Windows Forms uygulamasıdır. Uygulama 60 saniyeden geri sayar ve kalan süreyi bir ilerleme çubuğu ve etiket ile günceller. Ayrıca, bir düğmenin arka plan rengi, mevcut saniyenin tek mi yoksa çift mi olduğuna bağlı olarak değişir.

## Özellikler

- 60 saniyelik geri sayım zamanlayıcısı
- Kalan süreyi yansıtan ilerleme çubuğu
- Kalan süreyi gösteren etiket
- Her saniyede rengi değişen düğme (tek saniyeler için kırmızı, çift saniyeler için beyaz)

## Başlangıç

### Gereksinimler

- Visual Studio 2019 veya daha yenisi
- .NET Framework 4.7.2 veya daha yenisi

### Kurulum

1. Depoyu klonlayın:
    ```bash
    git clone https://github.com/kullaniciadi/projeadi.git
    ```
2. Çözüm dosyasını (.sln) Visual Studio'da açın.
3. Projeyi oluşturun ve çalıştırın.

## Kullanım

- Geri sayımı başlatmak için "Başlat" düğmesine tıklayın.
- Geri sayımı durdurmak için "Durdur" düğmesine tıklayın.
- İlerleme çubuğunun ve etiketin her saniyede güncellendiğini gözlemleyin.
- Düğmenin renginin her saniyede değiştiğini (tek saniyeler için kırmızı, çift saniyeler için beyaz) izleyin.

## Kod

Bu projede kullanılan ana kod aşağıda verilmiştir:

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsApp12
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        
        int counter = 60;
        
        private void btnStart_Click(object sender, EventArgs e)
        {
            counter = 60; // Zamanlayıcıyı başlattığınızda sayacı 60'a sıfırlayın
            progressBar1.Value = counter; // İlerleme çubuğunun değerini sıfırlayın
            timer1.Start();
        }

        private void btnStop_Click(object sender, EventArgs e)
        {
            timer1.Stop();
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            if (counter == 0)
            {
                timer1.Stop();
                MessageBox.Show("Zamanlayıcı durduruldu");
            }
            else
            {
                counter--;
                progressBar1.Value = counter;
                label1.Text = counter.ToString();
                if (counter % 2 == 1)
                    button4.BackColor = Color.Red;
                else
                    button4.BackColor = Color.White;
            }
        }

        private void progressBar1_Click(object sender, EventArgs e)
        {
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            label1.Text = counter.ToString();
            progressBar1.Maximum = 60; // İlerleme çubuğunun maksimum değerini ayarlayın
            progressBar1.Value = counter; // İlerleme çubuğunun başlangıç değerini ayarlayın
            timer1.Stop(); // Form yüklendiğinde zamanlayıcının durdurulduğundan emin olun
        }
    }
}
