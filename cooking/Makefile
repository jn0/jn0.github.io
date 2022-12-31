PANDOC := pandoc
PDFVIEW := evince
RM := rm -f
SED := sed

%.pdf:	%.md
	$(PANDOC) -d md2pdf.yaml --to=pdf -V title="$$(grep -m1 '^# ' $^|sed -e 's/^# //')" --output=$@ $^

%.html:	%.md
	$(PANDOC) -d md2pdf.yaml --to=html5 -V title="$$(grep -m1 '^# ' $<|sed -e 's/^# //')" --output=$@ $<
	$(SED)	-e 's#<title></title>#<title>'"$$(grep -m1 '^# ' $^|sed -e 's/^# //')"'</title>#' \
		-e 's,<h1 id="--">,<h1 id="--" style="display:none">,' \
		-e '1,$$s,href="\([^"]\+\)\.md",href="\1.html",g' \
		-i $@

.PHONY:	clean all view README.md

MARKDOWNS := $(wildcard *.md)

README.md:	$(MARKDOWNS:README.md=)
	@echo '# Рецепты' > $@
	grep -m1 '^# ' $^ | sed -e 's/^\(.*\):# \(.*\)$$/- [\2](\1)/' >> $@

all:	README.md $(MARKDOWNS:.md=.pdf) $(MARKDOWNS:.md=.html)

view:	$(MARKDOWNS:.md=.pdf)
	$(PDFVIEW) $^ &

clean:
	$(RM) *.pdf *.html
