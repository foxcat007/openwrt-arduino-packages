#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Initial port of shellinabox to OpenWrt - Jan Jaeger 25-MAR-2010

include $(TOPDIR)/rules.mk

PKG_NAME:=shellinabox
PKG_VERSION:=2.20
PKG_RELEASE:=5

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/shellinabox/shellinabox.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=05b2d3630c48dc9bca678d8158fce486c583c26b
PKG_SOURCE:=$(PKG_NAME)-$(PKG_REVISION).tar.gz

PKG_MAINTAINER:=
PKG_LICENSE:=
PKG_LICENSE_FILES:=

PKG_BUILD_DEPENDS:=+libopenssl +libpam
PKG_FIXUP:=libtool autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/shellinabox
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Shell In A Box
  DEPENDS:=+libopenssl +libpam +openssl-util +zlib
  URL:=http://shellinabox.googlecode.com
endef

define Package/shellinabox/description
 Web based AJAX terminal emulator
endef

CONFIGURE_ARGS:= \
	--host=$(GNU_TARGET_NAME) \
	--disable-runtime-loading \
	--disable-utmp

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) all
endef

define Package/shellinabox/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/shellinaboxd $(1)/usr/sbin/
	$(INSTALL_BIN) files/gen-cert.sh $(1)/usr/sbin/gen-cert

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) files/shellinabox-init.sh $(1)/etc/init.d/shellinabox-init
endef

define Package/shellianbox/prerm
!#/bin/sh

/etc/init.d/shellinabox-init stop 2> /dev/null

endef

$(eval $(call BuildPackage,shellinabox))
