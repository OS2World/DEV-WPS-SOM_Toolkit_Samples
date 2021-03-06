#
#   COMPONENT_NAME: somx
#
#   ORIGINS: 27
#
#
#    25H7912  (C)  COPYRIGHT International Business Machines Corp. 1992,1996
#   All Rights Reserved
#   Licensed Materials - Property of IBM
#   US Government Users Restricted Rights - Use, duplication or
#   disclosure restricted by GSA ADP Schedule Contract with IBM Corp.
#
#   @(#) 1.11.1.4 src/somples.os2/somd/cpp/event/makefile, somples.somd, som3.0, s309651d 12/19/96 13:49:50 [12/24/96 08:46:19]


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

#
# This make file has settings for IBM VisualAge C++ version 3.x for OS/2
# It is may be used with the nmake program.
#

#  Makefile for DSOM "event" samples (os2)

# General settings
SYS          = OS2
CC           = icc
CPPC         = icc
SC           = sc
LINKER       = ilink
IMPLIB       = implib
RM           = del
OBJ          = obj
CFLAGS       = $(DLL_CFLAGS)
CPPFLAGS     = $(DLL_CPPFLAGS)
SCFLAGS      =
TARGETS      = $(DLL_TARGET).$(DLL_EXT) $(EXE_TARGET).$(EXE_EXT) eventsvr.exe consumer.exe
CLEANFILES   = $(DLL_TARGET).$(DLL_LIBEXT) $(DLL_TARGET).$(DLL_DEF) $(DLL_INITMOD).* $(TARGETS)

# EXE build settings
EXE_CFLAGS   = -W3 -c -Ti+ -Q+ -Gm+ -Sm -Ss+
EXE_CPPFLAGS = -W3 -c -Ti+ -Q+ -Gm+ -Sm
EXE_LFLAGS   = /nofr /exepack /packd /packc /align:4 /stack:360000 /pm:vio /noe /noi /nol
EXE_OBJS     =  eventcli.obj
EXE_SYSOBJS  =
EXE_LIBS     = eventc os2386 somtk
EXE_TARGET   = eventcli
EXE_EXT      = exe
EXE_IDLS     =
EXE_CSRC     =
EXE_CPPSRC   = eventcli.cpp

# DLL build settings
DLL_INITMOD  = sinitmod
DLL_CFLAGS   = -W3 -c -Ti+ -Q+ -Gm+ -Ge- -Sm -Ss+
DLL_CPPFLAGS = -W3 -c -Ti+ -Q+ -Gm+ -Ge- -Sm
DLL_LFLAGS   = /dll /noe /stack:360000
DLL_OBJS     =  CELL.obj EVENTCH.obj EVENTCOM.obj sinitmod.obj
DLL_SYSOBJS  =
DLL_LIBS     = os2386.lib somtk.lib
DLL_TARGET   = eventc
DLL_EXT      = dll
DLL_LIBEXT   = lib
DLL_DEF      = def
DLL_IDLS     = CELL.IDL EVENTCH.IDL EVENTCOM.IDL
DLL_CSRC     =
DLL_CPPSRC   = CELL.cpp EVENTCH.cpp EVENTCOM.cpp

all: $(SOMBASE)\include\somxh.bld $(TARGETS) somdimpl

# DLL target
$(DLL_TARGET).$(DLL_EXT): $(DLL_OBJS) $(DLL_TARGET).$(DLL_LIBEXT)
        $(LINKER) $(DLL_LFLAGS) $(DLL_OBJS) $(DLL_SYSOBJS) /OUT:$@ $(DLL_LIBS) $(DLL_TARGET).$(DLL_DEF)
        sc $(SCFLAGS) -sir -u -mnolock *.idl

# DLL "Import" library target
$(DLL_TARGET).$(DLL_LIBEXT): $(DLL_TARGET).$(DLL_DEF)
        $(IMPLIB) $(DLL_TARGET).$(DLL_LIBEXT) $(DLL_TARGET).$(DLL_DEF)

# DLL exports file
$(DLL_TARGET).$(DLL_DEF): $(DLL_IDLS)
        $(SC) -s$(DLL_DEF) -mdll=$(DLL_TARGET) $(DLL_IDLS)

# DLL SOMInitModule function
$(DLL_INITMOD).$(OBJ): $(DLL_INITMOD).c

$(DLL_INITMOD).c: $(DLL_IDLS)
        $(SC) -simod -mdll=$(DLL_TARGET) -mimod=$@ $(DLL_IDLS)

# EXE target
$(EXE_TARGET).$(EXE_EXT): $(EXE_OBJS) eventc.lib
        $(LINKER) $(EXE_LFLAGS) $(EXE_OBJS) $(EXE_SYSOBJS),$@,NUL,$(EXE_LIBS);

eventsvr.$(EXE_EXT): eventsvr.obj eventc.lib
        $(LINKER) $(EXE_LFLAGS) eventsvr.obj $(EXE_SYSOBJS),$@,NUL,$(EXE_LIBS);

consumer.$(EXE_EXT): consumer.obj eventc.lib
        $(LINKER) $(EXE_LFLAGS) consumer.obj $(EXE_SYSOBJS),$@,NUL,$(EXE_LIBS);

# Clean up files that can be re-built
clean: cleanup cleanimpl

cleanup:
        -del *.$(OBJ) *.ih *.h *.xih *.xh *.ir $(CLEANFILES) *.rep  >nul 2>&1

# Cleanup the DSOM Implementation Repository.
cleanimpl:
        -regimpl -D -i cellServer2
        -erase somdimpl

$(SOMBASE)\include\somxh.bld:
        @echo This sample requires that the SOM toolkit C++ bindings have been built
        @echo with the somxh command.
        @exit 1

# Build the DSOM Implementation Repository.
somdimpl:
        -regimpl -A -i cellServer2 -p eventsvr.exe
        -regimpl -a -i cellServer2 -c Cell -c EventChannelAdmin::ConsumerAdmin -c EventChannelAdmin::EventChannel -c EventChannelAdmin::SupplierAdmin -c EventComm::Consumer -c EventComm::Supplier -c EventComm::EventConnection
        -regimpl -L -i cellServer2
    @echo "" > somdimpl

# Suffix rules for building source files
.SUFFIXES: .$(OBJ) .cpp .c .xih .xh .ih .h .idl

.cpp.$(OBJ):
        $(CPPC) $(CPPFLAGS) $<


.c.$(OBJ):
        $(CC) $(CFLAGS) $<


.idl.xih:
        $(SC) $(SCFLAGS) -sxih $<


.idl.xh:
        $(SC) $(SCFLAGS) -sxh $<


.idl.ih:
        $(SC) $(SCFLAGS) -sih $<


.idl.h:
        $(SC) $(SCFLAGS) -sh $<


# Dependencies follow
eventcli.obj: eventcli.cpp cell.xh eventcom.xih EVENTCOM.xh
        $(CPPC) $(EXE_CPPFLAGS) eventcli.cpp

eventsvr.obj: eventsvr.cpp cell.xh eventcom.xih EVENTCOM.xh eventch.xh
        $(CPPC) $(EXE_CPPFLAGS) eventsvr.cpp

consumer.obj: consumer.cpp eventcom.xih EVENTCOM.xh eventch.xh
        $(CPPC) $(EXE_CPPFLAGS) consumer.cpp

CELL.ih: CELL.IDL eventcom.idl
CELL.h: CELL.IDL eventcom.idl

EVENTCH.ih: EVENTCH.IDL eventcom.idl
EVENTCH.h: EVENTCH.IDL eventcom.idl

EVENTCOM.ih: EVENTCOM.IDL
EVENTCOM.h: EVENTCOM.IDL

CELL.obj: CELL.cpp cell.xih CELL.xh eventcom.xih EVENTCOM.xh
        $(CPPC) $(DLL_CPPFLAGS) CELL.cpp

EVENTCH.obj: EVENTCH.cpp eventcom.xih EVENTCOM.xh eventch.xih EVENTCH.xh
        $(CPPC) $(DLL_CPPFLAGS) EVENTCH.cpp

EVENTCOM.obj: EVENTCOM.cpp eventcom.xih EVENTCOM.xh
        $(CPPC) $(DLL_CPPFLAGS) EVENTCOM.cpp




