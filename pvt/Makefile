%.pdf:	%.md
	pandoc	-f markdown_github+hard_line_breaks \
		-N -S -s \
		--normalize --wrap=none \
		--variable=mainfont=Georgia \
		--latex-engine=xelatex \
		-o $@ $<

.PHONY:	clean all

MARKDOWNS := $(wildcard *.md)

all:	$(MARKDOWNS:.md=.pdf)

view:	$(MARKDOWNS:.md=.pdf)
	evince $^ &

clean:
	rm -f *.pdf
