#
# Copyright (C) 2014 Arduino LLC
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=arduino-firmata
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=0.3.4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/shokai/node-arduino-firmata.git
PKG_SOURCE_VERSION:=3e9bd3648ba63338a29b3bd7d682b3ed1fbcd6b6
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz

PKG_BUILD_DEPENDS:=node
PKG_NODE_VERSION:=0.12.7

PKG_MAINTAINER:=John Crispin <blogic@openwrt.org>
PKG_LICENSE:=MIT
PKG_LICENSE_FILE:=LICENSE.txt

include $(INCLUDE_DIR)/package.mk

define Package/node-arduino-firmata
  DEPENDS:=+node +node-serialport
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Node.js package to access serial ports for reading and writing
  URL:=https://www.npmjs.org/package/serialport
endef

define Package/node-arduino-firmata/description
 Node.js package to access serial ports for reading and writing OR Welcome your robotic JavaScript overlords. Better yet, program them!
endef

define Build/Prepare
	/bin/tar xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR) --strip-components 1
	$(Build/Patch)
endef

EXTRA_LDFLAGS="-L$(TOOLCHAIN_DIR)/lib/ -Wl,-rpath-link $(TOOLCHAIN_DIR)/lib/" \

define Build/Compile
	CC="$(TOOLCHAIN_DIR)/bin/mips-openwrt-linux-gcc" \
	CXX="$(TOOLCHAIN_DIR)/bin/mips-openwrt-linux-g++" \
	AR="$(TOOLCHAIN_DIR)/bin/mips-openwrt-linux-ar" \
	RANLIB="$(TOOLCHAIN_DIR)/bin/mips-openwrt-linux-ranlib" \
	LINK="$(TOOLCHAIN_DIR)/bin/mips-openwrt-linux-g++" \
	LD="$(TOOLCHAIN_DIR)/bin/mips-openwrt-linux-g++" \
	PATH="/usr/bin/:$(PATH)" \
	GYPFLAGS="-Dv8_use_mips_abi_hardfloat=false -Dv8_can_use_fpu_instructions=false" \
	CFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS) $(TARGET_CPPFLAGS) $(EXTRA_CPPFLAGS)" \
	CXXFLAGS="$(TARGET_CXXFLAGS) $(EXTRA_CXXFLAGS) $(TARGET_CPPFLAGS) $(EXTRA_CPPFLAGS)" \
	LDFLAGS="-L$(TOOLCHAIN_DIR)/lib/ -Wl,-rpath-link $(TOOLCHAIN_DIR)/lib/" \
	npm_config_arch=mips \
	npm_config_nodedir=$(BUILD_DIR)/node-v$(PKG_NODE_VERSION)/ \
	PREFIX="$(PKG_INSTALL_DIR)/usr/" \
	npm install -g $(PKG_BUILD_DIR)
endef

define Package/node-arduino-firmata/install
	mkdir -p $(1)/usr/lib/node
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/* $(1)/usr/lib/node
	rm -rf $(1)/usr/lib/node/arduino-firmata/node_modules/serialport/ 
	$(CP) -r ./files/* $(1)/
endef

$(eval $(call BuildPackage,node-arduino-firmata))

