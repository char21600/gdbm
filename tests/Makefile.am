# This file is part of GDBM.                                   -*- autoconf -*-
# Copyright (C) 2011 Free Software Foundation, Inc.
#
# GDBM is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2, or (at your option)
# any later version.
#
# GDBM is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GDBM. If not, see <http://www.gnu.org/licenses/>. */

EXTRA_DIST = \
 $(TESTSUITE_AT)\
 testsuite\
 package.m4

DISTCLEANFILES       = atconfig
MAINTAINERCLEANFILES = Makefile.in $(TESTSUITE)


## ------------ ##
## package.m4.  ##
## ------------ ##

$(srcdir)/package.m4: $(top_srcdir)/configure.ac $(srcdir)/Makefile
	$(AM_V_GEN){                                      \
	  echo '# Signature of the current package.'; \
	  echo 'm4_define([AT_PACKAGE_NAME],      [@PACKAGE_NAME@])'; \
	  echo 'm4_define([AT_PACKAGE_TARNAME],   [@PACKAGE_TARNAME@])'; \
	  echo 'm4_define([AT_PACKAGE_VERSION],   [@PACKAGE_VERSION@])'; \
	  echo 'm4_define([AT_PACKAGE_STRING],    [@PACKAGE_STRING@])'; \
	  echo 'm4_define([AT_PACKAGE_BUGREPORT], [@PACKAGE_BUGREPORT@])'; \
	} >$(srcdir)/package.m4

#

## ------------ ##
## Test suite.  ##
## ------------ ##

TESTSUITE_AT = \
 create00.at\
 fetch00.at\
 fetch01.at\
 version.at

TESTSUITE = $(srcdir)/testsuite
M4=m4

AUTOTEST = $(AUTOM4TE) --language=autotest
$(TESTSUITE): package.m4 $(TESTSUITE_AT)
	$(AUTOTEST) -I $(srcdir) testsuite.at -o $@.tmp
	mv $@.tmp $@

atconfig: $(top_builddir)/config.status
	cd $(top_builddir) && ./config.status tests/$@

clean-local:
	test ! -f $(TESTSUITE) || $(SHELL) $(TESTSUITE) --clean

check-local: atconfig atlocal $(TESTSUITE)
	$(SHELL) $(TESTSUITE)

# Run the test suite on the *installed* tree.
#installcheck-local:
#	$(SHELL) $(TESTSUITE) AUTOTEST_PATH=$(exec_prefix)/bin

## ------------ ##
## num2word     ##
## ------------ ##

check_PROGRAMS = \
 gtdump\
 gtfetch\
 gtload\
 num2word

INCLUDES = -I$(top_srcdir)/src -I$(top_builddir)/src
gtload_LDADD = ../src/libgdbm.la
gtdump_LDADD = ../src/libgdbm.la
gtfetch_LDADD = ../src/libgdbm.la



