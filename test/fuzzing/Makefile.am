# Process this file with automake to produce Makefile.in

NULL =
EXTRA_DIST =
CLEANFILES =
DISTCLEANFILES =
MAINTAINERCLEANFILES =

# Convenience targets:
lib:
	@$(MAKE) $(AM_MAKEFLAGS) -C $(top_builddir)/src fuzzing

$(top_builddir)/src/libharfbuzz-fuzzing.la: lib

EXTRA_DIST += \
	README \
	run-fuzzer-tests.py \
	CMakeLists.txt \
	$(NULL)

check_PROGRAMS = \
	hb-fuzzer \
	$(NULL)

AM_CPPFLAGS = \
	-DHB_DISABLE_DEPRECATED \
	-I$(top_srcdir)/src/ \
	-I$(top_builddir)/src/ \
	$(NULL)
LDADD = \
	$(top_builddir)/src/libharfbuzz-fuzzing.la \
	$(NULL)

hb_fuzzer_SOURCES = \
	hb-fuzzer.hh \
	hb-fuzzer.cc \
	main.cc \
	$(NULL)
hb_fuzzer_LDADD = \
	$(LDADD) \
	$(NULL)
hb_fuzzer_CPPFLAGS = \
	$(AM_CPPFLAGS) \
	$(NULL)
hb_fuzzer_DEPENDENCIES = \
	lib \
	$(NULL)

AM_TESTS_ENVIRONMENT = \
	EXEEXT="$(EXEEXT)"; \
	export EXEEXT; \
	srcdir="$(srcdir)"; \
	export srcdir; \
	builddir="$(builddir)"; \
	export builddir; \
	$(NULL)

if AUTOMAKE_OLDER_THAN_1_13
TESTS_ENVIRONMENT = \
	$(AM_TESTS_ENVIRONMENT) \
	$(TESTS_LOG_COMPILER) \
	$(NULL)
endif

check:
	$(srcdir)/run-fuzzer-tests.py

-include $(top_srcdir)/git.mk
