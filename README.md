# hse21_H3K9me3_ZDNA_human

## Анализ пиков гистоновой метки

1) Оставляем первые 5 столбцов:

`zcat ENCFF921OTR.bed.gz | cut -f1-5 > H3K9me9_SJSA1.ENCFF921OTR.hg38.bed`

`zcat ENCFF157SWY.bed.gz | cut -f1-5 > H3K9me9_SJSA1.ENCFF157SWY.hg38.bed`

2) Переводим координаты из hg38 в hg19, скачиваем данные о переводе для liftOver

`wget https://hgdownload.cse.ucsc.edu/goldenpath/hg38/liftOver/hg38ToHg19.over.chain.gz`

`liftOver H3K9me9_SJSA1.ENCFF921OTR.hg38.bed hg38ToHg19.over.chain.gz H3K9me9_SJSA1.ENCFF921OTR.hg19.bed H3K9me9_SJSA1.ENCFF921OTR.unmapped.bed`

`liftOver H3K9me9_SJSA1.ENCFF157SWY.hg38.bed hg38ToHg19.over.chain.gz H3K9me9_SJSA1.ENCFF157SWY.hg19.bed H3K9me9_SJSA1.ENCFF157SWY.unmapped.bed`
