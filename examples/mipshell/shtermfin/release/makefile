CC=g++
ARC=-mfpmath=sse -msse2
CFLAGS=-c -std=c++17 -fno-rtti -O3 $(ARC) -I$(HDR_MIPSHELL) -I$(HDR_MIPCL)
LDFLAGS=-shared-libgcc
RM=rm -f
INS=install
INSDIR=../bin
MIP_DIR=$(MIPCLDIR)
CFLAGS+=-DMIPSHELL_API="" -DMIP_API=""
LDFLAGS+= -L$(MIP_DIR)/lib -lmipcl -lmipshell
TARGET=shtermfin
#
HDR_MIPCL=$(MIP_DIR)/mipcl/headers
HDR_MIPSHELL=$(MIP_DIR)/mipshell/headers
#
VPATH=../sources
CFLAGS+=-I$(VPATH)
MOD= $(shell echo $(VPATH)/*.mod)
AUX=$(MOD:.mod=.aux)
SRC=$(notdir $(shell echo $(VPATH)/*.cpp))
OBJS=$(SRC:.cpp=.o)
#
.cpp.o:
	$(CC) $(CFLAGS) $< -o $@
%.aux : %.mod ;	$(MIP_DIR)/bin/mod2cpp $< $(<D)/$@
#
build: $(OBJS) 
	$(CC) $(LDFLAGS) $(OBJS) -o $(TARGET)
#dependencies
shtermfin.cpp: shtermfin.mod 
shtermfin.o: shtermfin.cpp shtermfin.aux shtermfin.h
main.o: main.cpp shtermfin.h
#
.PHONY: clean
clean:
	$(RM) $(OBJS) $(AUX)
install: $(TARGET)
	$(INS) $(TARGET) $(INSDIR)
	$(RM) $(TARGET)
all: build install

