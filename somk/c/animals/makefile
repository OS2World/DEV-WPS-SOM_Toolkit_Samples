#
#   COMPONENT_NAME: somx
#
#   ORIGINS: 27
#
#
#   25H7912  (C)  COPYRIGHT International Business Machines Corp. 1992,1996
#   All Rights Reserved
#   Licensed Materials - Property of IBM
#   US Government Users Restricted Rights - Use, duplication or
#   disclosure restricted by GSA ADP Schedule Contract with IBM Corp.
#
#   @(#) 1.3 src/somples.os2/somk/c/animals/makefile, somples.somk, som3.0, s309651d 12/19/96 13:49:48 [12/24/96 08:46:19]

# DISCLAIMER OF WARRANTIES.
# The following [enclosed] code is sample code created by IBM
# Corporation. This sample code is not part of any standard or IBM
# product and is provided to you solely for the purpose of assisting
# you in the development of your applications.  The code is provided
# "AS IS". IBM MAKES NO WARRANTIES, EXPRESS OR IMPLIED, INCLUDING BUT
# NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
# FOR A PARTICULAR PURPOSE, REGARDING THE FUNCTION OR PERFORMANCE OF
# THIS CODE.  IBM shall not be liable for any damages arising out of
# your use of the sample code, even if they have been advised of the
# possibility of such damages.
#
# DISTRIBUTION.
# This sample code can be freely distributed, copied, altered, and
# incorporated into other software, provided that it bears the above
# Copyright notice and DISCLAIMER intact.

OBJS       = animals.obj main.obj
TARGET     = animals.exe

CC       = icc
CFLAGS   = -c /W0
INCLUDEPATH = -I. -I$(SOMBASE)\include

SC         = $(SOMBASE)\bin\sc
SCFLAGS     =

LINKER      = ilink
LDFLAGS     = /noe /debug /PM:VIO
LIBLIST     = $(SOMBASE)\lib\somtk.lib

.SUFFIXES: .obj .c .idl .h .ih

.c.obj:
	  $(CC) $(INCLUDEPATH) $(CFLAGS) $<
.idl.h:
	  sc -sh $(SCFLAGS) $*.idl
.idl.ih:
	  sc -sih $(SCFLAGS) $*.idl

$(TARGET): $(SOMBASE)\include\somcorba.bld $(OBJS)
	$(LINKER) $(LDFLAGS) $(OBJS) $(LIBLIST) /OUT:$(TARGET)
	$(TARGET)

clean:
	-del *.obj *.exe *.map *.h *.ih $(CLEANFILES) >nul 2>&1

$(SOMBASE)\include\somcorba.bld:
	@echo This sample requires the CORBA-style C bindings
	@echo created using the somcorba command.
	@exit 1

animals.ih: animals.idl
animals.h: animals.idl
animals.obj: animals.c animals.h animals.ih
main.obj: main.c animals.h


