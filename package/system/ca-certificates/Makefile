#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=ca-certificates
PKG_VERSION:=20151214

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://ftp.debian.org/debian/pool/main/c/ca-certificates
PKG_MD5SUM:=2233bfa64af6f58f5eca9735b6742818
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/ca-certificates
  SECTION:=base
  CATEGORY:=Base system
  TITLE:=System CA certificates
endef

define Build/Install
	mkdir -p \
		$(PKG_INSTALL_DIR)/usr/sbin \
		$(PKG_INSTALL_DIR)/usr/share/ca-certificates
	$(call Build/Install/Default,)
endef

define Package/ca-certificates/install
	$(INSTALL_DIR) $(1)/etc/ssl/certs
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/ca-certificates/*/*.crt $(1)/etc/ssl/certs/

	for CERTFILE in `ls -1 $(1)/etc/ssl/certs`; do \
		HASH=`openssl x509 -hash -noout -in $(1)/etc/ssl/certs/$$$$CERTFILE` ; \
		SUFFIX=0 ; \
		while [ -h "$(1)/etc/ssl/certs/$$$$HASH.$$$$SUFFIX" ]; do \
			let "SUFFIX += 1" ; \
		done ; \
		$(LN) "$$$$CERTFILE" "$(1)/etc/ssl/certs/$$$$HASH.$$$$SUFFIX" ; \
	done
endef

$(eval $(call BuildPackage,ca-certificates))
