# hse21_H3K9me3_ZDNA_human

## Анализ пиков гистоновой метки

### Скачиваем данные экспериментов
Скачиваем данные, оставляем первые 5 столбцов

`zcat ENCFF921OTR.bed.gz | cut -f1-5 > H3K9me9_SJSA1.ENCFF921OTR.hg38.bed`

`zcat ENCFF157SWY.bed.gz | cut -f1-5 > H3K9me9_SJSA1.ENCFF157SWY.hg38.bed`

Гистограммы экпериментов: 



<p float="left">
  <img src="/https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/c97f17ea87ad33de5c881e289d12c310bf5b8c9b/img/len_hist.H3K9me9_SJSA1.ENCFF157SWY.hg38.png" width="100" />
  <img src="/https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/c97f17ea87ad33de5c881e289d12c310bf5b8c9b/img/len_hist.H3K9me9_SJSA1.ENCFF157SWY.hg38.png" width="100" /> 
</p>

**Переводим координаты из hg38 в hg19**, скачиваем необходимые данные о переводе для liftOver

`wget https://hgdownload.cse.ucsc.edu/goldenpath/hg38/liftOver/hg38ToHg19.over.chain.gz`

`liftOver H3K9me9_SJSA1.ENCFF921OTR.hg38.bed hg38ToHg19.over.chain.gz H3K9me9_SJSA1.ENCFF921OTR.hg19.bed H3K9me9_SJSA1.ENCFF921OTR.unmapped.bed`

`liftOver H3K9me9_SJSA1.ENCFF157SWY.hg38.bed hg38ToHg19.over.chain.gz H3K9me9_SJSA1.ENCFF157SWY.hg19.bed H3K9me9_SJSA1.ENCFF157SWY.unmapped.bed`

**Строим гистогограммы длин участков**
