# hse21_H2AFZ_ZDNA_human

### Cтудент - Мансуров Марат
| Организм      | Структура ДНК | Гистоновая метка | Тип клеток| .bed файл 1| .bed файл 2  |
| ------------- |:-------------:|:----------------:|:---------:|:----------:|:------------:|
| human(hg38)   | ZDNA          | H2AFZ           | A549      | ENCFF107KLN| ENCFF615OJI |

## Анализ пиков гистоновой метки

С помощью команды wget были получены файлы с пиками ENCFF107KLN и ENCFF615OJI :

`wget https://www.encodeproject.org/files/ENCFF107KLN/@@download/ENCFF107KLN.bed.gz` 

`wget https://www.encodeproject.org/files/ENCFF615OJI/@@download/ENCFF615OJI.bed.gz`

Были оставлены только первые пять столбцов:

`zcat ENCFF107KLN.bed.gz | cut -f1-5 > H2AFZ_A549.ENCFF107KLN.hg38.bed` 

`zcat ENCFF615OJI.bed.gz | cut -f1-5 > H2AFZ_A549.ENCFF615OJI.hg38.bed`

## Гистограммы длин участков пиков гистоновой метки

<p float="left">
  <img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/len_hist.H2AFZ_A549.ENCFF107KLN.hg38.png" />
  <img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/len_hist.H2AFZ_A549.ENCFF107KLN.hg19.png" />
</p>

<p float="left">
  <img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/len_hist.H2AFZ_A549.ENCFF615OJI.hg38.png" />
  <img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/len_hist.H2AFZ_A549.ENCFF615OJI.hg19.png" />
</p>

## Распредление длин пиков после фильтраци ( < 5000)

<p float="left">
  <img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/len_hist.H2AFZ_A549.ENCFF107KLN.hg19.png" />
  <img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/filter_peaks.H2AFZ_A549.ENCFF107KLN.hg19.filtered.hist.png" />
</p>

<p float="left">
  <img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/len_hist.H2AFZ_A549.ENCFF615OJI.hg19.png" />
  <img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/filter_peaks.H2AFZ_A549.ENCFF615OJI.hg19.filtered.hist.png" />
</p>

## Расположение пиков гистоновой метки H2AFZ относительно аннотироанных генов

<p float="left">
  <img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/chip_seeker.H2AFZ_A549.ENCFF107KLN.hg19.filtered.plotAnnoPie.png" />
  <img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/chip_seeker.H2AFZ_A549.ENCFF615OJI.hg19.filtered.plotAnnoPie.png" />
</p>

Объединяем файлы с пиками с помощью bedtools

`cat  *.filtered.bed  |   sort -k1,1 -k2,2n   |   bedtools merge   >  H2AFZ_A549.merge.hg19.bed`

Визуализируем в геномном браузере файлы с пиками и файл с объединенными пиками: 

`track visibility=dense name="ENCFF107KLN" description="H2AFZ_A549.ENCFF107KLN.hg19.filtered.bed"
https://raw.githubusercontent.com/Mrrrat/hse21_H2AFZ_ZDNA_human/main/data/H2AFZ_A549.ENCFF107KLN.hg19.filtered.bed`

`track visibility=dense name="ENCFF615OJI" description="H2AFZ_A549.ENCFF615OJI.hg19.filtered.bed"
https://raw.githubusercontent.com/Mrrrat/hse21_H2AFZ_ZDNA_human/main/data/H2AFZ_A549.ENCFF615OJI.hg19.filtered.bed`

`track visibility=dense name="ChIP_merge" color=50,50,200 description="H2AFZ_A549.merge.hg19.bed"
https://raw.githubusercontent.com/Mrrrat/hse21_H2AFZ_ZDNA_human/main/data/H2AFZ_A549.merge.hg19.bed`


Убеждаемся в корректности работы bedtools:

<img alt="ex0" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/intersection.png">



## Анализ участков вторичной структуры ДНК
### Распределение длин участков вторичной структуры ДНК 

<img width="60%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/len_hist.DeepZ.png" />

### Расположение участков вторичной структуры относительно аннотированных генов

<img width="60%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/chip_seeker.DeepZ.plotAnnoPie.png" />

## Анализ пересечений гистоновой метки и структуры ДНК

Находим пересечения между гистоновой меткой и ZDNA

`bedtools intersect -a DeepZ.bed -b H2AFZ_A549.merge.hg19.bed > H2AFZ_A549.intersect_with_DeepZ.hg19.bed`

### Визуализация в геномном браузере исходных участков структуры ДНК, а также их пересечения с гистоновой меткой

`track visibility=dense name="DeepZ" color=0,200,0 description="DeepZ"
https://raw.githubusercontent.com/Mrrrat/hse21_H2AFZ_ZDNA_human/main/data/DeepZ.bed`

`track visibility=dense name="intersect_with_DeepZ" color=200,0,0 description="H2AFZ_A549.intersect_with_DeepZ.bed"
https://raw.githubusercontent.com/Mrrrat/hse21_H2AFZ_ZDNA_human/main/data/H2AFZ_A549.intersect_with_DeepZ.bed`

Координаты: chr1:17,231,470-17,231,761 

<img alt="ex1" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/intersection.png">

[Ссылка](http://genome.ucsc.edu/s/Mansurov%20Marat/hse21_H2AFZ_ZDNA_human) на сохраненную сессию

### Ассоциируем полученные пересечения с ближайшими генами

<img width="45%" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/chip_seeker.H2AFZ_A549.intersect_with_DeepZ.plotAnnoPie.png" />


## GO-анализ

Был проведен GO-анализ для уникальных генов с использованием сайта http://pantherdb.org/ 

Общая информация 

<img width="948" alt="е" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/pantherdb1.png">

Наиболее значимые категории

<img width="946" alt="go_analysis" src="https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/images/pantherdb2.png">

Полный список категорий приведен [здесь](https://github.com/Mrrrat/hse21_H2AFZ_ZDNA_human/blob/main/data/pantherdb_GO_analysis.txt)
