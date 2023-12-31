#################################################################
# Makefile for HP aCC c++ programs SAR tools			#
# should work with other compilers as well			#
# "make [all]"		all exe's				#
# "make prog.o"		compile only prog.o			#
# "make prog"		compile only prog			#
# "make clean"		remove junk caused by makes		#
# "make cleaner"	remove all caused by makes 		#
# "make uninstall"	remove all caused by makes (incl. inst)	#
# "make install"	installs executables in INSTALL_DIR 	#
#                       (or if it's me, in CB_INSTALL	        #
#                       also installs gmt scripts.		#
#                       					#
#%// Bert Kampes 27-Dec-2000					#
### RCS								#
# $Header: /users/kampes/DEVELOP/DORIS/SARtools/RCS/Makefile,   #
# v 3.8 2004/08/06 15:41:24 kampes Exp $			#
#%// TUDelft     16-Apr-2009					#
#################################################################

### The shell we're using ###
SHELL	=	/bin/sh

### Installdirdef should exist!
INSTALL_DIR =	/usr/local/bin
#INSTALL_DIR =	/home/dlevelt/src/Doris_s1_git/bin

### GCC compiler
CC 	=	g++
CFLAGS  =       -O3 -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE  -D_LARGEFILE64_SOURCE #-m32 to force 32bit on 64bit platform

### Intel compiler
#CC	=	icpc
#CFLAGS	=	-Wp64 # -fast -O3 -parallel -auto-ilp32 -pc32

##################################################################
### THERE SHOULD BE NOTHING YOU WANT TO CHANGE BELOW THIS LINE ###
##################################################################
### Only for me, this will be ignored...
CB_INSTALL = 	../../executables/64bit

### The programs we want
PROGS	=	wrap \
		bkconvert \
		cpxmult \
		cpxdiv  \
		cpxconj \
		flapjack \
		cpxfiddle \
		floatmult \
		floatmask \
		readrasterheader \
		rasterheader \
		dateconv

# usedin install:
SCRIPTS =	
#SCRIPTS =	cpx2ps \
#		philamh2ps

### Compilation
default:	all
all:		$(PROGS) dummy

# dummy, since else makefile want to recompile the last util.
dummy:

# the utilities.
bkconvert:	bkconvert.o
		$(CC) $(CFLAGS) $@.o -o $@
wrap:		wrap.o
		$(CC) $(CFLAGS) $@.o -o $@
cpxmult:	cpxmult.o
		$(CC) $(CFLAGS) $@.o -o $@
cpxdiv: 	cpxdiv.o 
		$(CC) $(CFLAGS) $@.o -o $@
cpxconj:	cpxconj.o
		$(CC) $(CFLAGS) $@.o -o $@
cpxfiddle:	cpxfiddle.o
		$(CC) $(CFLAGS) $@.o -o $@
flapjack:	flapjack.o
		$(CC) $(CFLAGS) $@.o -o $@
floatmask:	floatmask.o
		$(CC) $(CFLAGS) $@.o -o $@
floatmult:	floatmult.o
		$(CC) $(CFLAGS) $@.o -o $@
readrasterheader:	readrasterheader.o
		$(CC) $(CFLAGS) $@.o -o $@
rasterheader:	rasterheader.o
		$(CC) $(CFLAGS) $@.o -o $@
dateconv:	dateconv.o
		$(CC) $(CFLAGS) $@.o -o $@


### Install in CB_INSTALL by linking/copying executables ###
install:	$(PROGS)
		dir=$(CB_INSTALL); \
        	if test -d $$dir; then \
		  $(MAKE) cbinstall; else $(MAKE) definstall; fi;

# or use ln instead of cp
#		  ln -sf `pwd`/$$p $(CB_INSTALL)/$$p; \

### Use symbolic links at our system, copy to /usr/local/bin on other.
definstall:	$(PROGS)
		dir=$(INSTALL_DIR); \
        	if test ! -d $$dir; then \
		  echo "Sorry, dir $(INSTALL_DIR) does not exist, exiting..."; exit; fi; \
		echo Installing in directory: $$dir; \
		list='$(PROGS) $(SCRIPTS)'; for p in $$list; do \
		  echo "Installing (copy): $$p"; \
		  cp -f $$p $(INSTALL_DIR)/$$p; \
		done
		$(MAKE) cleaner

### Use symbolic links at our system, copy to /usr/local/bin on other.
cbinstall:
		dir=$(CB_INSTALL); \
        	if test ! -d $$dir; then \
		  echo "Sorry, dir $(CB_INSTALL) does not exist, exiting..."; exit; fi; \
		echo Installing in directory: $$dir; \
		list='$(PROGS) $(SCRIPTS)'; for p in $$list; do \
		  echo "Installing (copy): $$p"; \
		  cp -f $$p $(CB_INSTALL)/$$p; \
		done
		$(MAKE) cleaner

lninstall:
		dir=$(CB_INSTALL); \
        	if test ! -d $$dir; then \
		  echo "Sorry, you are not me, exiting..."; exit; fi; \
		echo Installing in directory: $$dir; \
		list='$(PROGS) $(SCRIPTS)'; for p in $$list; do \
		  echo "Installing (link): $$p"; \
		  cp -f `pwd`/$$p $(CB_INSTALL)/$$p; \
		done
		  #ln -sf `pwd`/$$p $(CB_INSTALL)/$$p; \
		$(MAKE) cleaner

### Helpers ###
clean:	
		@rm -f *.o *dummy* *.bak
		@echo "* Removed junk."
### some reason under cygwin progs are not removed without ".exe"???
CYGWIN_EXE = 	$(PROGS:=.exe)
cleaner:	clean
		@rm -f $(PROGS) $(CYGWIN_EXE) a.out
		@echo "* Removed executables in source dir:  `pwd`."
uninstall:	cleaner
		dir=$(CB_INSTALL); \
        	if test -d $$dir; then \
		  cd $(CB_INSTALL); rm -f $(PROGS); \
		  echo "* Removed executables in install dir: $(CB_INSTALL)."; fi;
		dir=$(INSTALL_DIR); \
        	if test -d $$dir; then \
		  cd $(INSTALL_DIR); rm -f $(PROGS) $(CYGWIN_EXE); \
		  echo "* Removed executables in install dir: $(INSTALL_DIR)."; fi;

### How to make object files ###
.cc.o:		
	$(CC) $(CFLAGS) -c -o $(@) $<

### EOF.

