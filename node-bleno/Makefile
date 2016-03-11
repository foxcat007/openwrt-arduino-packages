#
# Copyright (C) 2014 Arduino LLC
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=bleno
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=0.3.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NPM_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=http://registry.npmjs.org/$(PKG_NPM_NAME)/-/
PKG_MD5SUM:=eac90d8b6eb9053928d8fe65ba5640ed

PKG_BUILD_DEPENDS:=node
PKG_NODE_VERSION:=0.12.7

include $(INCLUDE_DIR)/package.mk

define Package/node-bleno
  DEPENDS:=+node +bluez-libs
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=A node.js module for implementing BLE (Bluetooth low energy) peripherals
  URL:=https://www.npmjs.org/package/bleno
endef

define Package/node-bleno/description
 A node.js module for implementing BLE (Bluetooth low energy) peripherals
endef

define Build/Prepare
	/bin/tar xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR) --strip-components 1
	$(Build/Patch)
endef

EXTRA_LDFLAGS="-L$(TOOLCHAIN_DIR)/lib/ -Wl,-rpath-link $(TOOLCHAIN_DIR)/lib/" \

define Build/Compile
	$(MAKE_FLAGS) \
	npm_config_arch=$(CONFIG_ARCH) \
	npm_config_nodedir=$(BUILD_DIR)/node-v$(PKG_NODE_VERSION)/ \
	PREFIX="$(PKG_INSTALL_DIR)/usr/" \
	$(STAGING_DIR)/hoot-$(BOARD)/usr/in/npm install -g $(PKG_BUILD_DIR)
endef

define Package/node-bleno/install
	mkdir -p $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules $(1)/usr/lib/
endef

$(eval $(call BuildPackage,node-bleno))

