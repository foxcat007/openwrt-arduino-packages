#
# Copyright (C) 2006-2012 OpenWrt.org
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bossa
PKG_VERSION:=1.6.1-arduino
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/shumatech/BOSSA.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=293b73818e113bf4544bc1aa636495f1b2f0832d
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_MIRROR_HASH:=77292609870e1f5d22d15062f150eb1029ef83d1e00c889d6bca190deb4f

PKG_MAINTAINER:=
PKG_LICENSE:=
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/bossa
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libstdcpp
  TITLE:=Utility to flash ARM microcontrollers
endef

define Package/bossa/description
 BOSSA is a flash programming utility for Atmel's SAM family of flash-based
 ARM microcontrollers. The motivation behind BOSSA is to create a simple,
 easy-to-use, open source utility to replace Atmel's SAM-BA software.
endef

define Build/Compile
	COMMON_CXXFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS) $(TARGET_CPPFLAGS) $(EXTRA_CPPFLAGS)" \
	COMMON_LDFLAGS="$(TARGET_LINKFLAGS) $(TARGET_LDFLAGS)" \
	$(MAKE) -C $(PKG_BUILD_DIR) $(TARGET_CONFIGURE_OPTS) CFLAGS="$(TARGET_CFLAGS)" bin/bossac
endef

define Package/bossa/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/bossac $(1)/usr/bin/
endef

$(eval $(call BuildPackage,bossa))
