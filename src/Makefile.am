AM_CFLAGS = $(VARNISHAPI_CFLAGS) $(CODE_COVERAGE_CFLAGS) -I$(top_srcdir)/src/foreign \
	-Wall \
	-Werror \
	-Wall \
	-Wno-format-y2k \
	-Wstrict-prototypes \
	-Wmissing-prototypes \
	-Werror=missing-field-initializers \
	-Wpointer-arith \
	-Wreturn-type \
	-Wwrite-strings \
	-Wcast-qual \
	-Wswitch \
	-Wshadow \
	-Wunused-parameter \
	-Wcast-align \
	-Wchar-subscripts \
	-Wnested-externs \
	-Wextra \
	-Wno-sign-compare

AM_CPPFLAGS = $(CODE_COVERAGE_CPPFLAGS)
AM_LDFLAGS = $(VARNISHAPI_LIBS) $(VMOD_LDFLAGS) $(CODE_COVERAGE_LDFLAGS)

vmod_LTLIBRARIES = \
	libvmod_cookie.la \
	libvmod_header.la \
	libvmod_saintmode.la \
	libvmod_softpurge.la \
	libvmod_tcp.la \
	libvmod_var.la \
	libvmod_vsthrottle.la \
	libvmod_xkey.la

dist_man_MANS = \
	vmod_cookie.3 \
	vmod_header.3 \
	vmod_saintmode.3 \
	vmod_softpurge.3 \
	vmod_tcp.3 \
	vmod_var.3 \
	vmod_vsthrottle.3 \
	vmod_xkey.3

generated_docs = $(dist_man_MANS:.3=.rst)

libvmod_cookie_la_SOURCES = vmod_cookie.c
libvmod_header_la_SOURCES = vmod_header.c
libvmod_vsthrottle_la_SOURCES = vmod_vsthrottle.c
libvmod_saintmode_la_SOURCES = vmod_saintmode.c
libvmod_softpurge_la_SOURCES = vmod_softpurge.c foreign/hash/hash_slinger.h
libvmod_tcp_la_SOURCES = vmod_tcp.c
libvmod_var_la_SOURCES = vmod_var.c
libvmod_xkey_la_SOURCES = vmod_xkey.c

nodist_libvmod_cookie_la_SOURCES = vcc_cookie_if.c vcc_cookie_if.h
nodist_libvmod_header_la_SOURCES = vcc_header_if.c vcc_header_if.h
nodist_libvmod_vsthrottle_la_SOURCES = vcc_vsthrottle_if.c vcc_vsthrottle_if.h
nodist_libvmod_saintmode_la_SOURCES = vcc_saintmode_if.c vcc_saintmode_if.h
nodist_libvmod_softpurge_la_SOURCES = vcc_softpurge_if.c vcc_softpurge_if.h
nodist_libvmod_tcp_la_SOURCES = vcc_tcp_if.c vcc_tcp_if.h
nodist_libvmod_var_la_SOURCES = vcc_var_if.c vcc_var_if.h
nodist_libvmod_xkey_la_SOURCES = vcc_xkey_if.c vcc_xkey_if.h

@BUILD_VMOD_COOKIE@
@BUILD_VMOD_HEADER@
@BUILD_VMOD_SAINTMODE@
@BUILD_VMOD_SOFTPURGE@
@BUILD_VMOD_TCP@
@BUILD_VMOD_VAR@
@BUILD_VMOD_VSTHROTTLE@
@BUILD_VMOD_XKEY@

rst-docs: $(generated_docs)
	cp $(generated_docs) $(top_srcdir)/docs/

doctest:
	for i in *.vcc; do \
		../test-vclsnippet $$i; \
		rst2html --halt=2 --exit-status=2 $$i 1>/dev/null; \
	done;

AM_TESTS_ENVIRONMENT = \
	PATH="$(VMOD_TEST_PATH)" \
	LD_LIBRARY_PATH="$(VARNISH_LIBRARY_PATH)"
TEST_EXTENSIONS = .vtc
VTC_LOG_COMPILER = varnishtest -v
AM_VTC_LOG_FLAGS = \
	-Dvmod_builddir=$(abs_top_builddir)/src \
	-Dvmod_directors="directors from \"$(VARNISHAPI_VMODDIR)/libvmod_directors.so\""

TESTS = $(VMOD_TESTS)

EXTRA_DIST = \
	foreign \
	vtree.h \
	$(VMOD_TESTS) \
	vmod_cookie.vcc \
	vmod_header.vcc \
	vmod_saintmode.vcc \
	vmod_softpurge.vcc \
	vmod_tcp.vcc \
	vmod_var.vcc \
	vmod_vsthrottle.vcc \
	vmod_xkey.vcc
