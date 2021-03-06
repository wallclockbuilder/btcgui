# This file exists purely for convenience and will check for a
# installed GTK that is compatible with gotk3, calling either
# go build or go get with the correct build tags.

VALID_MAJOR=	3
VALID_MINORS=	6 8 10 12
GTK_VERSION=	$(shell pkg-config --modversion gtk+-3.0)
GTK_MAJOR=	$(shell echo ${GTK_VERSION} | cut -f 1 -d '.')
GTK_MINOR=	$(shell echo ${GTK_VERSION} | cut -f 2 -d '.')
GTK_TAG=	gtk_${GTK_MAJOR}_${GTK_MINOR}

all: install

check-gtk:
ifeq (,$(GTK_VERSION))
	@echo "Cannot find GTK."
	@exit 1
endif
ifneq ($(GTK_MAJOR),$(VALID_MAJOR))
	@echo "Unsupported GTK major version."
	@exit 1
endif
ifeq (,$(findstring $(GTK_MINOR), $(VALID_MINORS)))
	@echo "Unsupported GTK minor version."
	@exit 1
endif

build: check-gtk
	go build -tags=${GTK_TAG} ./...

install: check-gtk
	go get -tags=${GTK_TAG} ./...

update: check-gtk
	go get -u -tags=${GTK_TAG} ./...
