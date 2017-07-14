#
# Copyright (C) 2010-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=paho-mqtt
PKG_VERSION:=1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pypi.python.org/packages/source/p/paho-mqtt/
PKG_HASH:=0f7a629efe6e3a2c61b59d3550aa9f2c4529b5689a65fde45e6f1ac36b9a261e

PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=EPL-1.0
PKG_LICENSE_FILES:=LICENSE.txt

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/python-paho-mqtt
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=python-paho-mqtt
  URL:=http://www.eclipse.org/paho/
  DEPENDS:=+python-light +python-xml +python-openssl +libopenssl
endef

define Package/python-paho-mqtt/description
 MQTT version 3.1/3.1.1 client class
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
endef

define Package/python-paho-mqtt/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(1)$(PYTHON_PKG_DIR)
endef

$(eval $(call BuildPackage,python-paho-mqtt))
