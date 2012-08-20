NAME=buildsys-rpm-config
VERSION = $(shell cat VERSION)
TAGVER = $(shell cat VERSION | sed -e "s/\([0-9\.]*\).*/\1/")

ifeq ($(VERSION), $(TAGVER))
        TAG = $(TAGVER)
else
        TAG = "HEAD"
endif

all:

clean:
	rm -f *~ 

install:
	mkdir -p $(DESTDIR)/$(PREFIX)/lib/rpm/buildsys
	cp -pr * $(DESTDIR)/$(PREFIX)/lib/rpm/buildsys/
	rm -f $(DESTDIR)/$(PREFIX)/lib/rpm/buildsys/Makefile
	rm -f $(DESTDIR)/$(PREFIX)/lib/rpm/buildsys/buildsys-rpm-config.spec
	chown -R root:root $(DESTDIR)/$(PREFIX)/lib/rpm/buildsys/

tag-archive:
	git tag -a $(VERSION)

create-archive:
	git archive --format=tar --prefix=buildsys-rpm-config-$(VERSION)/ HEAD | bzip2 -9v > buildsys-rpm-config-$(VERSION).tar.bz2
	@echo "The final archive is in $(NAME)-$(VERSION).tar.bz2"

archive: tag-archive create-archive
dist: create-archive
