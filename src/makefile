GCC          = g++ 
CLANG        = clang++
CC           = $(GCC)
CFLAGS       = -c -Wall -std=c++11 -ggdb1 -lpthread
LDFLAGS      = 

LATEX        = /usr/texbin/pdflatex
LATEXFLAGS   = -output-directory=$(DOCDIR)

HTLATEX      = /usr/texbin/htlatex
HTLATEXFLAGS = "" "" -d


#htlatex ../docs/func-idioms-c++.tex  "" "" -d/tmp/

OBJDIR       = ../obj
EXEDIR       = ../bin
DOCDIR       = ../docs
HTMLDIR      = ../html

EXE          = main

SOURCES      = $(wildcard *.cpp)
INCLUDES     = $(wildcard *.hpp)
DOCS         = $(wildcard $(DOCDIR)/*.tex)


PDF          = $(DOCS:.tex=.pdf)
DVI	     = $(DOCS:.tex=.dvi)
AUX	     = $(DOCS:.tex=.aux)
LOG          = $(DOCS:.tex=.log)

BASEDOC      = $(DOCDIR)/func-idioms-c++.tex


OBJECTS      = $(addprefix $(OBJDIR)/, $(SOURCES:.cpp=.o))
EXECUTABLE   = $(addprefix $(EXEDIR)/, $(EXE))
MKTARGETDIR  = @mkdir -p $(@D)

#$(info $(PDF))
#$(info $(OBJECTS))
#$(info $(INCLUDES))

all : $(SOURCES) $(EXECUTABLE) $(INCLUDES)

$(EXECUTABLE): $(OBJECTS) $(INCLUDES) 
		$(MKTARGETDIR)
		$(CC)  $(OBJECTS) -o $@ $(LDFLAGS)

$(OBJDIR)/%.o: %.cpp $(INCLUDES) 
		$(MKTARGETDIR)
		$(CC) $(CFLAGS) $< -o $@


docs 	: $(PDF)

$(PDF) : $(DOCS)
	$(foreach var, $(DOCS), $(LATEX) $(LATEXFLAGS) $(var);)
	$(foreach var, $(DOCS), $(LATEX) $(LATEXFLAGS) $(var);)

html  :
	cd $(HTMLDIR); \
	$(HTLATEX) $(BASEDOC) 

clean:
	rm -f $(OBJECTS) $(EXEDIR)/core $(EXECUTABLE)

docsclean: 
	rm -f $(PDF) $(AUX) $(DVI) $(LOG)

realclean:
	-rm -f $(OBJECTS) $(EXEDIR)/core $(EXECUTABLE)
	-rm -f *~
	-rm -f $(PDF) $(AUX) $(DVI) $(LOG)
	-rm $(DOCDIR)/*~  $(DOCDIR)/*log 
	-rmdir $(OBJDIR)
	-rmdir $(EXEDIR)

