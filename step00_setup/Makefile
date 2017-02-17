MODELNAME = $(shell sed -n "s/Package: *\([^ ]*\)/\1/p" DESCRIPTION)
MODELVERS = $(shell sed -n "s/Version: *\([^ ]*\)/\1/p" DESCRIPTION)
MODELSRC  = $(shell basename `pwd`)
AUTHORNAME = "Steph"
AUTHOREMAIL = "Steph@itsalocke.com"
RENDERDIR = "../new_version"
GITURL = "https://${GITHUB_PAT}@github.com/${TRAVIS_REPO_SLUG}.git"

getrepo:
  git clone $(GITURL) $(RENDERDIR)
  git config --global user.name $(AUTHORNAME)
  git config --global user.email $(AUTHOREMAIL)

analysis:
  cd $(RENDERDIR);\
  Rscript -e 'rmarkdown::render("README.Rmd", output_format = rmarkdown::github_document(), output_dir="docs")'

commit:
  git commit -am "Documents produced in clean environment via Travis ${TRAVIS_BUILD_NUMBER}"

push:
  git push --quiet origin master

build: getrepo analysis commit push
