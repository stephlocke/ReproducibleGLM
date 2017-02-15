MODELNAME := $(shell sed -n "s/Package: *\([^ ]*\)/\1/p" DESCRIPTION)
MODELVERS := $(shell sed -n "s/Version: *\([^ ]*\)/\1/p" DESCRIPTION)
MODELSRC  := $(shell basename `pwd`)

all: check clean

build:
	cd ..;\
	R CMD build  --no-manual $(MODELSRC)

install: build
	cd ..;\
	R CMD INSTALL $(MODELNAME)_$(MODELVERS).tar.gz

check: build
	cd ..;\
	R CMD check $(MODELNAME)_$(MODELVERS).tar.gz

clean:
	cd ..;\
	$(RM) -r $(MODELNAME).Rcheck/

analysis:
	cd ..;\
	Rscript -e 'rmarkdown::render("README.Rmd", output_format = "rmarkdown::github_document", out)'
