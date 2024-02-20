# FastQC Kullanım Kılavuzu

FastQC, yüksek kaliteli RNA-seq veya DNA-seq verilerinin kalitesini değerlendirmek için kullanılan bir araçtır. Bu kılavuzda, FastQC'nin kurulumu ve temel kullanımı adımlarını bulacaksınız.

## Kurulum
Bu komut, Conda paket yöneticisi aracılığıyla "bioconda" kanalından "fastqc" paketini kurar. İşlevi şunlardır:

1. **Paket Yöneticisi Aracılığıyla Kurulum**: Conda, Python ve diğer diller için bir paket yöneticisi ve ortam yöneticisidir.
 `conda install` komutu, belirli bir paketin Conda depolarından (standart veya özel) yüklenmesini sağlar. Bu durumda, `fastqc` paketi, bioinformatic alanında kullanılan bir araç olan FastQC'nin Conda ortamına kurulmasını sağlar.

2. **bioconda Kanalı**: "bioconda" kanalı, biyoinformatik araçlarının (örneğin, genetik veri analizi araçları gibi) yayınlandığı bir Conda kanalıdır. Bu kanal, biyoinformatik topluluğu için popüler ve yaygın olarak kullanılan araçların kolayca erişilebilir olmasını sağlar. FastQC gibi biyoinformatik araçlarını kurmak için genellikle "bioconda" kanalı kullanılır.

3. **FastQC Paketi**: FastQC, yüksek hacimli genetik verilerin kalite kontrolü için kullanılan popüler bir araçtır. Genellikle, bir dizi veri setinin (örneğin, FASTQ dosyalarının) kalite değerlendirmesi yapmak için kullanılır. Bu nedenle, 
```
conda install -c bioconda fastqc

```
 komutu, FastQC aracının Conda ortamına kurulumunu gerçekleştirir ve kullanıcının bu aracı hızlı bir şekilde yüklemesini sağlar.

 ###
 fastqc komutları için:

 ```
 fasqtc -h
 ```

- **SYNOPSIS** (Özet):
    - `fastqc seqdosya1 seqdosya2 .. seqdosyaN`
    - `fastqc [-o çıktı dizini] [--(no)extract] [-f fastq|bam|sam] [-c kontaminant dosyası] seqdosya1 .. seqdosyaN`

- **DESCRIPTION** (Açıklama):
    - FastQC, bir dizi dizgi dosyasını okur ve her birinden veri setinizdeki farklı olası problemleri belirlemeye yardımcı olacak bir dizi farklı modülden oluşan bir kalite kontrol raporu üretir.
    - Komut satırında işlenecek dosyalar belirtilmezse, program etkileşimli bir grafik uygulaması olarak başlar. Dosyalar komut satırında belirtilirse, kullanıcı etkileşimi gerektirmeyen bir şekilde çalışır. Bu mod, standartlaştırılmış bir analiz iş akışına dahil edilmek için uygundur.
    - Programın seçenekleri aşağıdaki gibidir:
        - `-h --help`: Bu yardım dosyasını yazdırır ve çıkar.
        - `-v --version`: Programın sürümünü yazdırır ve çıkar.
        - `-o --outdir`: Tüm çıktı dosyalarını belirtilen çıktı dizininde oluşturun. Lütfen bu dizinin var olması gerektiğini unutmayın, çünkü program bunu oluşturmaz. Bu seçenek belirlenmediyse, her dizgi dosyası için çıktı dosyası, işlenen dizgi dosyasının bulunduğu dizinde oluşturulur.
        - `--casava`: Dosyalar ham casava çıktısından gelir. Aynı örnek grubundaki dosyalar (yalnızca grup numarasıyla farklılık gösterenler) bir set olarak değil, bireysel olarak analiz edilir. Başlıkta filtre bayrağı ayarlı olan dizgiler analizden hariç tutulur. Dosyaların casava tarafından verilen isimlere (`.gz` ile sıkıştırılmış ve biten dosya adları dahil) sahip olması gerekir, aksi takdirde doğru şekilde gruplandırılmazlar.
        - `--nano`: Dosyalar nanopore dizilerinden gelir ve fast5 formatındadır. Bu modda, işlemek için dizinler geçirebilirsiniz ve program, bu dizinlerde bulunan tüm fast5 dosyalarını alacak ve bu dosyalardaki dizgilerden tek bir çıktı dosyası üretecektir.
        - `--nofilter`: --casava ile çalışırken, QC analizi yapılırken casava tarafından kalitesiz olarak işaretlenen dizgileri kaldırmayın.
        - `--extract`: Ayarlandığında, zipli çıktı dosyası oluşturulduktan sonra aynı dizinde sıkıştırılır. Varsayılan olarak, bu seçenek, fastqc etkileşimsiz modda çalıştırıldığında ayarlanır.
        - `-j --java`: Fastqc'yi başlatmak için kullanmak istediğiniz java ikilisinin tam yolunu sağlar. Sağlanmadıysa, java'nın yolunuzda olduğu varsayılır.
        - `--noextract`: Çıktı dosyasını oluşturduktan sonra dosyayı sıkıştırma. Eğer etkileşimsiz modda çalıştırıyorsanız, bu seçeneği ayarlamazsanız.
        - `--nogroup`: Okunabilirler >50bp için bazların gruplandırılmasını devre dışı bırakır. Tüm raporlar okunabilirdeki her baz için veri gösterecek. UYARI: Bu seçeneği kullanırsanız fastqc çılgınca düşecek ve yanacak ve gerçekten uzun okumalarda kullanırsanız çizimleriniz saçma bir boyutta olabilir. Sizi uyardım!
        - `--min_length`: Raporlanacak dizginin uzunluğuna yapay bir alt sınır belirler. Bu değeri en uzun dizgi uzunluğunuzdan büyük veya eşit olacak şekilde ayarladığınız sürece, bu, dizgi gruplarınızı oluşturmak için kullanılacak dizi uzunluğu olacaktır. Bunlar, biraz değişken dizgi uzunluklarına sahip veri setlerinden doğrudan karşılaştırılabilir istatistikler oluşturmak için kullanışlı olabilir.
        - `-f --format`: Normal dizi dosyası biçimi algılama atlanır ve programın belirtilen biçimi kullanması sağlanır. Geçerli biçimler `bam`, `sam`, `bam_mapped`, `sam_mapped` ve `fastq`'dur.
        - `-t --threads`: Eşzamanlı olarak işlenebilecek dosya sayısını belirtir. Her iplik için 250MB bellek tahsis edilecektir, bu nedenle kullanılabilir belleğinizin daha fazla iplik çalıştırmamanızı ve 32 bit bir makinede 6 iplikten fazla çalıştırmamanızı sağlamalısınız.
        - `-c --contaminants`: Aşırı temsil edilen dizgileri taramak için varsayılan olmayan bir dosyayı belirtir. Dosya, adlı kirleticilerin gruplarını içermelidir. Kirleticiler, biçim adı[tab]dizgi şeklinde belirtilmelidir. Satırlar bir kare ile başlarsa yoksayılacaktır.
        - `-a --adapters`: Kütüphane tarafından açıkça aranacak adaptör dizilerini belirten varsayılan olmayan bir dosyayı belirtir. Dosya, ad[tab]dizgi biçiminde adlandırı

##
Elinizdeki bir veya birden fazla dosyanın kalite kontrolü için:

```
fastqc fasqc-(ortam)/(inceleyeceğiniz dosyanın ismi)
```

Elde edilen sonuçları incelemek için:
```
explorer.ex .
```
bu kod ile dosya konumuna girip elde edilem html. dosyasını açarak sonuçlara ulaşabilirsiniz.