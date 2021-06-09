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
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/b0b45867b24ed6b1ebe890b82b261c7f85d12ddb/img/chip_seeker.H3K9me9_SJSA1.ENCFF157SWY.hg19.filtered.plotAnnoPie.png" width="450" /> 
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/b0b45867b24ed6b1ebe890b82b261c7f85d12ddb/img/chip_seeker.H3K9me9_SJSA1.ENCFF921OTR.hg19.filtered.plotAnnoPie.png" width="450" />  

</p>

### Объединение наборов
Объединяем два набора отфильтрованных ChIP-seq пиков с помощью утилиты bedtools merge
`cat  *.filtered.bed  |   sort -k1,1 -k2,2n   |   bedtools merge   >  H3K9me9_SJSA1.merge.hg19.bed`

![](https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/fad64b947423bc562e60689da522b157aedbbde7/img/merge.PNG)

### Вторичная структура DeepZ
Скачиваем файл со вторичной стр-рой ДНК, строим распределение длин участков вторичной стр-ры ДНК, смотрим, где располагаются участки стр-ры ДНК относительно аннотированных генов
`wget https://raw.githubusercontent.com/vanya-antonov/hse21_H3K4me3_ZDNA_human/main/data/DeepZ.bed`

<p float="left">
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/4b530216b8a1aa135b33e67c036721938bd12f10/img/len_hist.DeepZ.png" width="450" />
  <img src="https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/4b530216b8a1aa135b33e67c036721938bd12f10/img/chip_seeker.DeepZ.plotAnnoPie.png" width="450" /> 
</p>

## Анализ пересечений гистоновой метки и стр-ры ДНК

## Пересечения гистоновой меткой и стр-рами ДНК
Находим пересечения, строим гистограмму
`bedtools intersect -a DeepZ.bed -b H3K9me9_SJSA1.merge.hg19.bed > H3K9me9_SJSA1.intersect_with_DeepZ.bed`
![](https://github.com/petrusgrigus/hse21_H3K9me3_ZDNA_human/blob/0af1b11c009fce04ac75dc00b78c1101b88395e0/img/len_hist.H3K9me9_SJSA1.intersect_with_DeepZ.png)
