## Как работает

Изначально всё резюме пишется в README.md чтобы быть доступным для чтения в github.
Затем используется [pandoc](https://pandoc.org/) чтобы конвертировать резюме в другие форматы.

### Конвертация в HTML
Для конвертации в HTML pandoc использует template.html,
где заранее размечено всё
и есть место для вставки сконвертированного body, помечено $body$

используется команда <code>pandoc --template=template.html README.md index.html</code>


### Конвертация в PDF

Для конвертации в pdf необходим движок
* для Windows подходит xelatex, его можно поставить, установив [MikTex](https://miktex.org/download), подробнее [здесь](https://stackoverflow.com/a/60687165)
* для linux опишу позже.

С markdown при конвертации в pdf какие-то проблемы у pandoc, поэтому сначала конвертируем в html, а его уже в pdf. Также важно указать шрифт, который существует в системе, так как в противном случае русский алфавит может пропасть и не отображаться.  

используются команды  
<code>
pandoc -o temp.html README.md  
&&  
pandoc temp.html --output=output/cv.pdf --pdf-engine=xelatex --listings --css=css/bootstrap.min.css -V geometry:"left=1.5cm,right=1.5cm,top=2cm,bottom=2cm" -V colorlinks=trgue -V linkcolor=blue -V urlcolor=blue -V toccolor=gray -V mainfont="DejaVuSans"
</code>

### Зачем докерфайл?

Ну, я сбилдил свой образ над pandoc/latex:latest (возможно, это была версия 2.9) и залил его на докер хаб, чтобы использовать кириллицу в github actions...