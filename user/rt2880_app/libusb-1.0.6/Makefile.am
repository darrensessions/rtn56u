AUTOMAKE_OPTIONS = dist-bzip2 no-dist-gzip
ACLOCAL_AMFLAGS = -I m4
DISTCLEANFILES = ChangeLog libusb-1.0.pc
EXTRA_DIST = TODO PORTING
SUBDIRS = libusb doc

if BUILD_EXAMPLES
SUBDIRS += examples
endif

pkgconfigdir=$(libdir)/pkgconfig
pkgconfig_DATA=libusb-1.0.pc

romfs: all
	cp -f libusb/.libs/libusb-1.0.so.0.0.0 .
	ln -sf libusb-1.0.so.0.0.0 libusb-1.0.so.0
	ln -sf libusb-1.0.so.0.0.0 libusb-1.0.so
	$(ROMFSINST) /lib/libusb-1.0.so.0.0.0
	$(ROMFSINST) /lib/libusb-1.0.so.0
	$(ROMFSINST) /lib/libusb-1.0.so

.PHONY: ChangeLog dist-up
ChangeLog:
	git --git-dir $(top_srcdir)/.git log > ChangeLog || touch ChangeLog

dist-hook: ChangeLog

reldir = .release/$(distdir)
dist-up: dist
	rm -rf $(reldir)
	mkdir -p $(reldir)
	cp $(distdir).tar.bz2 $(reldir)
	rsync -rv $(reldir) dsd_,libusb@frs.sourceforge.net:/home/frs/project/l/li/libusb/libusb-1.0/
	rm -rf $(reldir)

