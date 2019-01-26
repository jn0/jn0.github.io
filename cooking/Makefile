PANDOC := pandoc
PDFVIEW := evince
RM := rm -f
SED := sed

none := 
space := $(none) $(none)

MARKDOWN_TYPE := markdown_github
MARKDOWN_TYPE += hard_line_breaks
PANDOC_OPTIONS := --from $(subst $(space),+,$(strip $(MARKDOWN_TYPE)))
PANDOC_OPTIONS += --standalone			# to build "solid" PDFs
PANDOC_OPTIONS += --smart
PANDOC_OPTIONS += --normalize
PANDOC_OPTIONS += --wrap=none
PANDOC_OPTIONS += --variable=mainfont=Georgia	# this is to support UTF-8
PANDOC_OPTIONS += --variable=papersize=A4
PANDOC_OPTIONS += --variable=fontsize=12pt
PANDOC_OPTIONS += --variable=margin-left=25mm
PANDOC_OPTIONS += --variable=margin-right=3ex
PANDOC_OPTIONS += --variable=margin-top=3ex
PANDOC_OPTIONS += --variable=margin-bottom=3ex
PANDOC_OPTIONS += --variable=links-as-notes=yes
PANDOC_OPTIONS += --latex-engine=xelatex	# this is for the same

%.pdf:	%.md
	$(PANDOC) $(PANDOC_OPTIONS) -V title="$$(grep -m1 '^# ' $^|sed -e 's/^# //')" --output=$@ $^

%.html:	%.md
	$(PANDOC) $(PANDOC_OPTIONS) --to=html5 -V title="$$(grep -m1 '^# ' $<|sed -e 's/^# //')" --output=$@ $<
	$(SED)	-e 's#<title></title>#<title>'"$$(grep -m1 '^# ' $^|sed -e 's/^# //')"'</title>#' \
		-e 's,<h1 id="--">,<h1 id="--" style="display:none">,' \
		-e '1,$$s,href="\([^"]\+\)\.md",href="\1.html",g' \
		-i $@

.PHONY:	clean all view README.md

MARKDOWNS := $(wildcard *.md)

README.md:	$(MARKDOWNS)
	@echo '# Рецепты' > $@
	grep -m1 '^# ' $^ | sed -e 's/^\(.*\):# \(.*\)$$/- [\2](\1)/' >> $@

all:	README.md $(MARKDOWNS:.md=.pdf) $(MARKDOWNS:.md=.html)

view:	$(MARKDOWNS:.md=.pdf)
	$(PDFVIEW) $^ &

clean:
	$(RM) *.pdf *.html
