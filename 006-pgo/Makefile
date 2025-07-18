.DELETE_ON_ERROR:
.PHONY: all preview testsimul clean test testdb
.DEFAULT_GOAL:=all

PAPERBACK:=pgo-pb
OUT:=out
TEXCC:=lualatex
TEXOPTS:=-shell-escape -halt-on-error
TEX:=$(addsuffix .tex, pgo foreward objectives trainer friends types attacks \
											 species pokémon battle unbounded bounded tactics \
											 simul spawn example about ooo optimal notice)
CIRCO:=$(addprefix circo/, $(addsuffix .dot, dragon nature phases rational steel))
DOT:=$(addprefix dot/, $(addsuffix .dot, death jumble))
PDFVIEW:=okular
PDF:=$(addsuffix .pdf, $(PAPERBACK))
MAKEFILE:=Makefile

UPSTREAM:=$(addsuffix .csv, moves)
TESTDB:=$(OUT)/testdb
BREAKPOINTS:=$(OUT)/breakpoints
SIMUL:=$(OUT)/s/simul
FATTACKS:=$(OUT)/fastattacks
CARDEXAMPLE:=$(OUT)/cardexample
CATTACKS:=$(OUT)/chargedattacks
DUALTYPES:=$(OUT)/dualtypes
SPECIES:=$(OUT)/species
FORMS:=$(OUT)/forms
HETERO:=$(OUT)/hetero
TRELS:=$(OUT)/typerels
TIMETOFIRST:=$(OUT)/timetofirst
DUALCHARGED:=$(OUT)/dualcharged
USERS:=$(OUT)/users
REGIONS:=$(OUT)/regions
WEATHER:=$(OUT)/weather
POPS:=$(OUT)/populations
DPEVSE:=$(OUT)/dpevse
PPTVST:=$(OUT)/pptvst
PAIRS:=$(OUT)/pairs
EPTVST:=$(OUT)/eptvst
ATKTYPES:=$(OUT)/attacktypes
SINDEX:=$(OUT)/sindex
FATTACKTEX:=$(OUT)/fastattacks.tex
CATTACKTEX:=$(OUT)/chargedattacks.tex
CARDEXAMPLETEX:=$(CARDEXAMPLE).tex
DUALTYPESTEX:=$(OUT)/dualtypes.tex
DPEVSEDAT:=$(DPEVSE).dat
PPTVSTDAT:=$(PPTVST).dat
EPTVSTDAT:=$(EPTVST).dat
DUALSUMSTEX:=$(OUT)/dualsummaries.tex
FUSERSTEX:=$(OUT)/fastusers.tex
CUSERSTEX:=$(OUT)/chargedusers.tex
ATKTYPESTEX:=$(OUT)/attacktypes.tex
SPECIESTEX:=$(OUT)/species.tex
FPAIRSTEX:=$(OUT)/fpairs.tex
CPAIRSTEX:=$(OUT)/cpairs.tex
MEGATEX:=$(OUT)/mega.tex
#DYNATEX:=$(OUT)/dynas.tex
SINDEXTEX:=$(SINDEX).tex
GIGANTATEX:=$(OUT)/gigantas.tex
WEATHERTEX:=$(WEATHER).tex
POPSTEX:=$(POPS).tex
REGIONSTEX:=$(REGIONS).tex
CP1500A:=$(OUT)/cp1500a.tex
CP2500A:=$(OUT)/cp2500a.tex
CP1500G:=$(OUT)/cp1500g.tex
CP2500G:=$(OUT)/cp2500g.tex
HETEROTEX:=$(OUT)/hetero.tex
TRELSTEX:=$(OUT)/typerels.tex
DUALCHARGEDTEX:=$(DUALCHARGED).tex
TIMETOFIRSTTEX:=$(TIMETOFIRST).tex
BREAKPOINTSDAT:=$(BREAKPOINTS).tex
GENTEX:=$(DUALTYPESTEX) $(SPECIESTEX) $(MEGATEX) $(CP1500A) $(CP2500A) \
	$(FATTACKTEX) $(CATTACKTEX) $(HETEROTEX) $(TRELSTEX) \
	$(GIGANTATEX) $(ATKTYPESTEX) $(WEATHERTEX) $(REGIONSTEX) \
	$(CUSERSTEX) $(FUSERSTEX) $(DUALSUMSTEX) $(POPSTEX) $(CPAIRSTEX) \
	$(SINDEXTEX) $(DPEVSEDAT) $(PPTVSTDAT) $(EPTVSTDAT) \
	$(BREAKPOINTSDAT) $(FPAIRSTEX) $(CARDEXAMPLETEX) $(CP1500G) $(CP2500G) \
	$(TIMETOFIRSTTEX) $(DUALCHARGEDTEX)
GRAPHS:=$(addprefix $(OUT)/, $(addsuffix .png, $(CIRCO) $(DOT))) \
	octave/greninja.png
SIMULSRC:=$(addprefix s/, simul.cpp bottom.h charged.h ko.h moves.h sift.h simul.h top.h)

preview: all
	$(PDFVIEW) $(PAPERBACK).pdf

all: $(PDF) $(SIMUL)

$(PAPERBACK).pdf: $(TEX) $(MAKEFILE) $(GRAPHS) $(GENTEX) $(SIMULSRC) $(PAPERBACK).toc testdb
	$(TEXCC) --shell-escape -jobname=$(basename $(@F)) '\def\paperback{yes}\input{$(<F)}' $(TEXOPTS)

$(PAPERBACK).toc: $(TEX) $(MAKEFILE) $(GRAPHS) $(GENTEX) $(SIMULSRC) testdb
	$(TEXCC) --shell-escape -jobname=$(basename $(@F)) '\def\paperback{yes}\input{$(<F)}' $(TEXOPTS)

$(OUT)/dot/%.png: dot/%
	@mkdir -p $(@D)
	dot -Tpng $< > $@

$(OUT)/circo/%.png: circo/%
	@mkdir -p $(@D)
	circo -Tpng $< > $@

$(OUT)/dualtypes.tex: $(OUT)/dualtypes
	@mkdir -p $(@D)
	$(<) > $@

$(OUT)/dualsummaries.tex: $(OUT)/dualtypes
	@mkdir -p $(@D)
	$(<) summary > $@

$(OUT)/cp1500a.tex: $(OUT)/bounded $(MAKEFILE)
	@mkdir -p $(@D)
	$(<) a 1500 128.75 > $@

$(OUT)/cp1500g.tex: $(OUT)/bounded $(MAKEFILE)
	@mkdir -p $(@D)
	$(<) g 1500 124.66 > $@

$(OUT)/cp2500a.tex: $(OUT)/bounded $(MAKEFILE)
	@mkdir -p $(@D)
	$(<) a 2500 161.85 > $@

$(OUT)/cp2500g.tex: $(OUT)/bounded $(MAKEFILE)
	@mkdir -p $(@D)
	$(<) g 2500 156.80 > $@

$(CUSERSTEX): $(OUT)/users
	@mkdir -p $(@D)
	$(<) charged > $@

$(FUSERSTEX): $(OUT)/users
	@mkdir -p $(@D)
	$(<) fast > $@

$(OUT)/mega.tex: $(OUT)/forms
	@mkdir -p $(@D)
	$(<) mega > $@

#$(OUT)/dynas.tex: $(OUT)/forms
#	@mkdir -p $(@D)
#	$(<) dynamax > $@

$(OUT)/gigantas.tex: $(OUT)/forms
	@mkdir -p $(@D)
	$(<) gigantamax > $@

$(FPAIRSTEX): $(PAIRS)
	@mkdir -p $(@D)
	$(<) fast > $@

$(CPAIRSTEX): $(PAIRS)
	@mkdir -p $(@D)
	$(<) charged > $@

$(OUT)/graphs/%.png: $(OUT)/graphs/%.plg
	@mkdir -p $(@D)
	gnuplot $(<) > $@

$(OUT)/%.tex: $(OUT)/%
	@mkdir -p $(@D)
	$(<) > $@

$(DUALCHARGEDTEX): $(DUALCHARGED)
	@mkdir -p $(@D)
	$(<) d > $@

$(BREAKPOINTSDAT): $(basename $(BREAKPOINTS))
	@mkdir -p $(@D)
	$(<) clodsire 15-15-15@99 "poison sting" "megahorn/earthquake" sawk 15-14-14@99 "low kick" "focus blast/low sweep" > $@

$(OUT)/%.dat: $(OUT)/%
	@mkdir -p $(@D)
	$(<) > $@

$(SIMUL): $(SIMULSRC) pgotypes.cpp
	@mkdir -p $(@D)
	g++ -std=c++23 -march=native -mtune=native -o $@ -Wall -W -O3 $(<) -lm

$(OUT)/%: %.cpp pgotypes.cpp
	@mkdir -p $(@D)
	g++ -std=c++23 -g -o $@ -Wall -W -O2 $(<F) -lm

test: testsimul testdb

testdb: $(TESTDB)
	$(<)

testsimul: $(SIMUL)
	time $(<) clodsire 15-15-15@70 "poison sting" "megahorn" sawk 15-14-14@50 "low kick" "focus blast"
	time $(<) clodsire 15-15-15@70 "poison sting" "earthquake" sawk 15-14-14@50 "low kick" "low sweep"
	time $(<) clodsire 15-15-15@50 "poison sting" "megahorn/earthquake" sawk 15-14-14@50 "low kick" "focus blast/low sweep"
	time $(<) clodsire 15-15-15@99 "poison sting" "megahorn/earthquake" sawk 15-14-14@99 "low kick" "focus blast/low sweep"

clean:
	@rm -vrf $(PAPERBACK).toc $(PAPERBACK).log $(PAPERBACK).aux $(PAPERBACK).lof $(PAPERBACK).listing
	@rm -vrf pdfa.xmpi
	@rm -vrf $(OUT)
	@rm -vrf svg-inkscape
	@rm -vrf _minted
	@rm -vf tags
