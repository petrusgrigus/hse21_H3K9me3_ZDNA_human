# hse21_H3K9me3_ZDNA_human

## Анализ пиков гистоновой метки

### Скачиваем данные экспериментов
Скачиваем данные, оставляем первые 5 столбцов

`zcat ENCFF921OTR.bed.gz | cut -f1-5 > H3K9me9_SJSA1.ENCFF921OTR.hg38.bed`

`zcat ENCFF157SWY.bed.gz | cut -f1-5 > H3K9me9_SJSA1.ENCFF157SWY.hg38.bed`

**Гистограммы длин:**

<p float="left">
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/c97f17ea87ad33de5c881e289d12c310bf5b8c9b/img/len_hist.H3K9me9_SJSA1.ENCFF157SWY.hg38.png" width="450" />
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/c97f17ea87ad33de5c881e289d12c310bf5b8c9b/img/len_hist.H3K9me9_SJSA1.ENCFF921OTR.hg38.png" width="450" /> 
</p>

**Переводим координаты из hg38 в hg19**
Скачиваем необходимые данные о переводе, запускаем liftOver

`wget https://hgdownload.cse.ucsc.edu/goldenpath/hg38/liftOver/hg38ToHg19.over.chain.gz`

`liftOver H3K9me9_SJSA1.ENCFF921OTR.hg38.bed hg38ToHg19.over.chain.gz H3K9me9_SJSA1.ENCFF921OTR.hg19.bed H3K9me9_SJSA1.ENCFF921OTR.unmapped.bed`

`liftOver H3K9me9_SJSA1.ENCFF157SWY.hg38.bed hg38ToHg19.over.chain.gz H3K9me9_SJSA1.ENCFF157SWY.hg19.bed H3K9me9_SJSA1.ENCFF157SWY.unmapped.bed`

**Гистограммы длин:** 

<p float="left">
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/c97f17ea87ad33de5c881e289d12c310bf5b8c9b/img/len_hist.H3K9me9_SJSA1.ENCFF157SWY.hg19.png" width="450" />
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/c97f17ea87ad33de5c881e289d12c310bf5b8c9b/img/len_hist.H3K9me9_SJSA1.ENCFF921OTR.hg19.png" width="450" /> 
</p>

### Отбросим outliers

Я выбрал отбросить пики длиннее, чем 700, так график получается достаточно равномерным

<p float="left">
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/99281436d8fa3e48e44cbd55c696595d085808b3/img/filter_peaks.H3K9me9_SJSA1.ENCFF157SWY.hg19.filtered.hist.png" width="450" />
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/99281436d8fa3e48e44cbd55c696595d085808b3/img/filter_peaks.H3K9me9_SJSA1.ENCFF921OTR.hg19.filtered.hist.png" width="450" /> 
</p>

### Анализ расположения меток
Смотрим, где располагаются пики гистоновой метки относительно аннотированных генов

<p float="left">
  <figure>
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/b0b45867b24ed6b1ebe890b82b261c7f85d12ddb/img/chip_seeker.H3K9me9_SJSA1.ENCFF157SWY.hg19.filtered.plotAnnoPie.png" width="450" /> <figcaption>ENCFF157SWY</figcaption>
    </figure>
   <figure>
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/b0b45867b24ed6b1ebe890b82b261c7f85d12ddb/img/chip_seeker.H3K9me9_SJSA1.ENCFF921OTR.hg19.filtered.plotAnnoPie.png" width="450" />  <figcaption>ENCFF921OTR</figcaption>
     </figure>
</p>
