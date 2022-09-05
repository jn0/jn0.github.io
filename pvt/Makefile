PANDOC := pandoc
PDFVIEW := evince
RM := rm -f
SED := sed

none := 
space := $(none) $(none)

MARKDOWN_TYPE := markdown_github
# MARKDOWN_TYPE += hard_line_breaks
PANDOC_OPTIONS := --from $(subst $(space),+,$(strip $(MARKDOWN_TYPE)))+smart
PANDOC_OPTIONS += --standalone			# to build "solid" PDFs
PANDOC_OPTIONS += --wrap=none
PANDOC_OPTIONS += --variable=mainfont=Georgia	# this is to support UTF-8
PANDOC_OPTIONS += --pdf-engine=xelatex	# this is for the same

OS_TYPE := $(shell	if test -r /etc/os-release; \
			then grep '^ID=' /etc/os-release | cut -d= -f2-; \
			else echo unknown; fi)
OS_NAME := $(shell	if test -r /etc/os-release; \
			then grep '^NAME=' /etc/os-release | cut -d= -f2-; \
			else echo unknown; fi)
OS_VERSION := $(shell	if test -r /etc/os-release; \
			then grep '^VERSION=' /etc/os-release | cut -d= -f2-; \
			else echo unknown; fi)

$(info Running in $(OS_NAME), version $(OS_VERSION) (like "$(OS_TYPE)"))

UBUNTU_PACKAGES := pandoc evince		# pandoc + evince
UBUNTU_PACKAGES += texlive-xetex		# xelatex
UBUNTU_PACKAGES += ttf-mscorefonts-installer	# Georgia TTF

%.pdf:	%.md
	$(SED) -e 's/.md)/.pdf)/g' < $< | $(PANDOC) $(PANDOC_OPTIONS) --output=$@

.PHONY:	clean all view install

MARKDOWNS := $(wildcard */*.md)
PDFS := $(MARKDOWNS:.md=.pdf)

README.md:	$(MARKDOWNS)
	echo "# Private Topics on $$(date '+%Y-%m-%d')" > "$@"; \
	for md in $^;	\
	do	t=$$(grep -m1 '^#\s\+' $$md | cut -c3-); \
		echo "- [$$t]($$md)"; \
	done >> "$@"; \
	echo "# EOF #" >> "$@"

README.pdf:	README.md $(PDFS)
all:	README.pdf

view:	$(PDFS)
	$(PDFVIEW) $^ &

clean:
	$(RM) *.pdf */*.pdf

install:
ifeq ($(OS_TYPE),ubuntu)
	$(info Installing for "$(OS_TYPE)"...)
	sudo apt install $(UBUNTU_PACKAGES)
else
	$(error Cannot install on "$(OS_TYPE)"!)
endif
