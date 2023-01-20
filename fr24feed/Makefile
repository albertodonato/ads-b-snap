VERSION ?= 1.0.34-0
REPO_URL ?= https://repo-feed.flightradar24.com

SNAPCRAFT_TARGET_ARCH ?= amd64

ifeq ($(SNAPCRAFT_TARGET_ARCH), amd64)
DOWNLOAD_URL := $(REPO_URL)/linux_x86_64_binaries/fr24feed_$(VERSION)_amd64.tgz
else ifeq ($(findstring $(SNAPCRAFT_TARGET_ARCH), arm64 armhf), $(SNAPCRAFT_TARGET_ARCH))
DOWNLOAD_URL := $(REPO_URL)/rpi_binaries/fr24feed_$(VERSION)_armhf.tgz
else
$(error "unsupported architecture")
endif

BIN := fr24feed

.DEFAULT_GOAL := all

all: $(BIN)
.PHONY: all

$(BIN):
	curl -s $(DOWNLOAD_URL) | tar xvz --strip 1 --wildcards '*/$@'

clean:
	rm -f $(BIN)
.PHONY: clean

install: DESTDIR ?= /usr
install: $(BIN)
	install -d $(DESTDIR)/bin $(DESTDIR)/etc
	install fr24feed.ini $(DESTDIR)/etc
	install $(BIN) -t $(DESTDIR)/bin
.PHONY: install
