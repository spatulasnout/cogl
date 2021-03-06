include $(top_srcdir)/build/autotools/Makefile.am.silent

NULL =

CLEANFILES =
DISTCLEANFILES =

EXTRA_DIST =

source_c = \
	cogl-pango-display-list.c   \
	cogl-pango-fontmap.c        \
	cogl-pango-render.c         \
	cogl-pango-glyph-cache.c    \
	cogl-pango-pipeline-cache.c \
	$(NULL)

source_h = cogl-pango.h

source_h_priv = \
	cogl-pango-display-list.h   \
	cogl-pango-private.h        \
	cogl-pango-glyph-cache.h    \
	cogl-pango-pipeline-cache.h \
	$(NULL)

lib_LTLIBRARIES = libcogl-pango.la

libcogl_pango_la_SOURCES = $(source_c) $(source_h) $(source_h_priv)
libcogl_pango_la_CFLAGS = $(COGL_DEP_CFLAGS) $(COGL_EXTRA_CFLAGS) $(MAINTAINER_CFLAGS)
libcogl_pango_la_LIBADD = $(COGL_DEP_LIBS) $(COGL_EXTRA_LDFLAGS)
libcogl_pango_la_LIBADD += $(top_builddir)/cogl/libcogl.la
libcogl_pango_la_LDFLAGS = \
	-export-dynamic \
	-export-symbols-regex "^cogl_pango_.*"
	-no-undefined \
	-version-info @COGL_LT_CURRENT@:@COGL_LT_REVISION@:@COGL_LT_AGE@

INCLUDES = \
	-DG_DISABLE_SINGLE_INCLUDES	\
	-DCLUTTER_COMPILATION		\
	-DG_LOG_DOMAIN=\"CoglPango\"	\
	-I$(top_srcdir)/cogl		\
	-I$(top_srcdir)/cogl/winsys	\
	-I$(top_srcdir)			\
	-I$(top_builddir)

cogl_pangoheadersdir = $(includedir)/cogl/cogl-pango
cogl_pangoheaders_HEADERS = $(source_h)

pc_files = cogl-pango-1.0.pc \
	   cogl-pango-$(COGL_API_VERSION)-experimental.pc

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = $(pc_files)

EXTRA_DIST += cogl-pango.pc.in
DISTCLEANFILES += $(pc_files)

-include $(INTROSPECTION_MAKEFILE)

INTROSPECTION_GIRS =

if HAVE_INTROSPECTION
INTROSPECTION_COMPILER_ARGS=--includedir=$(top_builddir)/cogl

CoglPango-1.0.gir: libcogl-pango.la Makefile

CoglPango_1_0_gir_NAMESPACE = CoglPango
CoglPango_1_0_gir_VERSION = 1.0
CoglPango_1_0_gir_LIBS = libcogl-pango.la
CoglPango_1_0_gir_FILES = $(source_h) $(source_c)
CoglPango_1_0_gir_CFLAGS = $(INCLUDES) $(AM_CPPFLAGS) $(COGL_DEP_CFLAGS)
CoglPango_1_0_gir_INCLUDES = Pango-1.0 PangoCairo-1.0
CoglPango_1_0_gir_EXPORT_PACKAGES = cogl-pango-1.0
CoglPango_1_0_gir_SCANNERFLAGS = \
	--warn-all \
	--identifier-prefix=CoglPango \
	--symbol-prefix=cogl_pango \
	--c-include='cogl-pango/cogl-pango.h' \
	--include-uninstalled=$(top_builddir)/cogl/Cogl-1.0.gir

INTROSPECTION_GIRS += CoglPango-1.0.gir

girdir = $(datadir)/gir-1.0
gir_DATA = $(INTROSPECTION_GIRS)

typelibdir = $(libdir)/girepository-1.0
typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)

CLEANFILES += $(gir_DATA) $(typelib_DATA)
endif
