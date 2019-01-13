PANDOC := pandoc
PDFVIEW := evince
RM := rm -f

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
PANDOC_OPTIONS += --latex-engine=xelatex	# this is for the same

%.pdf:	%.md
	$(PANDOC) $(PANDOC_OPTIONS) --output=$@ $<

.PHONY:	clean all view

MARKDOWNS := $(wildcard *.md)

all:	$(MARKDOWNS:.md=.pdf)

view:	$(MARKDOWNS:.md=.pdf)
	$(PDFVIEW) $^ &

clean:
	$(RM) *.pdf
