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
#   @(#) 1.1 src/somples.os2/somk/cpp/simple/makefile, somples.somk, som3.0 12/2/96 14:12:11 [12/24/96 07:41:08]

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

OBJS       = main.obj simple.obj
TARGET     = test.exe

CPPC       = icc
CPPFLAGS   = -c
INCLUDEPATH = -I. -I$(SOMBASE)\include

SC         = $(SOMBASE)\bin\sc
SCFLAGS     = 

LINKER      = ilink
LDFLAGS     = /noe /debug /PM:VIO 
LIBLIST     = $(SOMBASE)\lib\somtk.lib

.SUFFIXES: .obj .cpp .idl .xh .xih

.cpp.obj:
	  $(CPPC) $(INCLUDEPATH) $(CPPFLAGS) $<
.idl.xh:
	  sc -sxh $(SCFLAGS) $*.idl
.idl.xih:
	  sc -sxih $(SCFLAGS) $*.idl

$(TARGET): $(SOMBASE)\include\somxh.bld $(OBJS)
	$(LINKER) $(LDFLAGS) $(OBJS) $(LIBLIST) /OUT:test.exe
	$(TARGET)

clean:
	-del *.obj *.exe *.map *.xh *.xih $(CLEANFILES) >nul 2>&1

$(SOMBASE)\include\somxh.bld:
	@echo This sample requires the C++ bindings
	@echo created using the somxh command.
	@exit 1

simple.obj: simple.xh simple.xih simple.cpp
main.obj: simple.xh main.cpp

