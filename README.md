# hse21_H3K9me3_ZDNA_human

## Анализ пиков гистоновой метки

### Скачиваем данные экспериментов**
Скачиваем данные, оставляем первые 5 столбцов

`zcat ENCFF921OTR.bed.gz | cut -f1-5 > H3K9me9_SJSA1.ENCFF921OTR.hg38.bed`

`zcat ENCFF157SWY.bed.gz | cut -f1-5 > H3K9me9_SJSA1.ENCFF157SWY.hg38.bed`

Гистограммы экпериментов: 

<object data="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/main/img/len_hist.H3K9me9_SJSA1.ENCFF921OTR.hg38.pdf" type="application/pdf" width="700px" height="700px">
    <embed src="http://yoursite.com/the.pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="http://yoursite.com/the.pdf">Download PDF</a>.</p>
    </embed>
</object>

**Переводим координаты из hg38 в hg19**, скачиваем необходимые данные о переводе для liftOver

`wget https://hgdownload.cse.ucsc.edu/goldenpath/hg38/liftOver/hg38ToHg19.over.chain.gz`

`liftOver H3K9me9_SJSA1.ENCFF921OTR.hg38.bed hg38ToHg19.over.chain.gz H3K9me9_SJSA1.ENCFF921OTR.hg19.bed H3K9me9_SJSA1.ENCFF921OTR.unmapped.bed`

`liftOver H3K9me9_SJSA1.ENCFF157SWY.hg38.bed hg38ToHg19.over.chain.gz H3K9me9_SJSA1.ENCFF157SWY.hg19.bed H3K9me9_SJSA1.ENCFF157SWY.unmapped.bed`

**Строим гистогограммы длин участков**
