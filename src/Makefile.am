bin_PROGRAMS    = macopix
SUBDIRS = icons
macopix_SOURCES   =\
	 main.c macos_getwin.c callbacks.c pixmap.c gui.c balloon.c clock.c configfile.c utils.c gtkut.c mail.c pop.c md5c.c md5ify.c nokkari.c bmp.c bmpwrite.c sockmsg.c codeconv.c unmime.c base64.c quoted-printable.c unlha.c untar.c trayicon.c alpha.c ssl.c sslmanager.c dnd.c resources.c http-client.c intl.h main.h configfile.h libpop.h md5.h nokkari.h gtkut.h bmp.h sockmsg.h codeconv.h unmime.h base64.h quoted-printable.h tar32api.h ssl.h resources.h

if HAVE_WINDRES
MACOPIX_RES = macopix.res
macopix.res: macopix_res.rc
	$(WINDRES) $< -O coff -o $@
else
MACOPIX_RES = 
endif

EXTRA_DIST = \
	macopix_res.rc.in\
        gresource.xml\
        macopix.ico\
	tar64.dll\
	tar32.dll

BUILT_SOURCES=resources.c resources.h

INCLUDES        = $(GTK_CFLAGS) $(GLIB_CFLAGS) $(GNUTLS_CFLAGS)\
		  $(DISABLE_DEPRECATED) $(OSX_CADD) $(GTKMAC_CFLAGS)
LDADD           = $(GTK_LIBS) $(GLIB_LIBS) $(WINMM_LIBS)\
                   $(MACOPIX_RES)  $(WINSOCK_LIBS) $(UNLHA32_LIBS)  $(TAR32_LIBS) $(GNUTLS_LIBS) $(WIN32_ICONV_LIBS) $(OSX_LDADD) $(GTKMAC_LIBS) $(LIBICONV)
AM_CPPFLAGS = -DLOCALEDIR=\""$(localedir)"\" \
	      -DCOMMON_DIR=\""$(commondir)"\" \
	      -DPREFIX_DIR=\""$(prefixdir)"\" \
	      -DTHEMEDIR=\""$(themedir)"\"

resource_files=$(shell $(GLIB_COMPILE_RESOURCES) --sourcedir=$(srcdir) --generate-dependencies $(srcdir)/gresource.xml)

resources.h:
	$(AM_V_GEN) $(GLIB_COMPILE_RESOURCES) --target=$@ --sourcedir=$(srcdir) --generate-header $(srcdir)/gresource.xml

resources.c: gresource.xml $(resource_files) resources.h
	$(AM_V_GEN) $(GLIB_COMPILE_RESOURCES) --target=$@ --sourcedir=$(srcdir) --generate-source $(srcdir)/gresource.xml

