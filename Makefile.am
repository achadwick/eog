if ENABLE_JPEG
jpeg_DIRS = jpegutils
endif

SUBDIRS = $(jpeg_DIRS) src plugins help data doc po

ACLOCAL_AMFLAGS = -I m4 ${ACLOCAL_FLAGS}

EXTRA_DIST = 			\
	HACKING			\
	MAINTAINERS		\
	ChangeLog-2.6		\
	ChangeLog-2.18		\
	ChangeLog.pre-git	\
	meson.build		\
	meson_options.txt	\
	meson_post_install.py	\
	po/meson.build		\
	tests

DISTCLEANFILES =

DISTCHECK_CONFIGURE_FLAGS = --enable-gtk-doc --enable-installed-tests

MAINTAINERCLEANFILES = \
	$(GITIGNORE_MAINTAINERCLEANFILES_TOPLEVEL) \
	$(GITIGNORE_MAINTAINERCLEANFILES_M4_LIBTOOL) \
	$(GITIGNORE_MAINTAINERCLEANFILES_M4_GETTEXT) \
	$(srcdir)/config.h.in \
	$(srcdir)/gtk-doc.make

@BEHAVE_INSTALLED_TESTS_RULE@
INSTALLED_TESTS=about undo sidepane fullscreen wallpaper screenshot_tour1 screenshot_tour2
INSTALLED_TESTS_TYPE=session-exclusive

-include $(top_srcdir)/git.mk

# This is the last commit before the ChangeLog was converted
CHANGELOG_START = 6a7944721e667a5c2d87e841917d850aea885019

dist-hook:
	@if test -d "$(srcdir)/.git"; \
	then \
		echo Creating ChangeLog && \
		( cd "$(top_srcdir)" && \
		  echo '# Generated by Makefile. Do not edit.'; echo; \
		  $(top_srcdir)/missing --run git log -M -C --stat \
		  $(CHANGELOG_START)..) > ChangeLog.tmp \
		&& mv -f ChangeLog.tmp $(top_distdir)/ChangeLog \
		|| ( rm -f ChangeLog.tmp ; \
		     echo Failed to generate ChangeLog >&2 ); \
	else \
		echo A git clone is required to generate a ChangeLog >&2; \
	fi
