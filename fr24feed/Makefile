VERSION ?= 1.0.48-0
REPO_URL ?= https://repo-feed.flightradar24.com

CRAFT_TARGET_ARCH ?= amd64

ifeq ($(CRAFT_TARGET_ARCH), amd64)
DOWNLOAD_URL := $(REPO_URL)/linux_binaries/fr24feed_$(VERSION)_amd64.tgz
else ifeq ($(findstring $(CRAFT_TARGET_ARCH), arm64 armhf), $(CRAFT_TARGET_ARCH))
DOWNLOAD_URL := $(REPO_URL)/rpi_binaries/fr24feed_$(VERSION)_$(CRAFT_TARGET_ARCH).tgz
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
	install fr24feed.ini -t $(DESTDIR)/etc
	install $(BIN) -t $(DESTDIR)/bin
.PHONY: install
