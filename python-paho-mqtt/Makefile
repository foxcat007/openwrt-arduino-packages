#
# Copyright (C) 2010-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=paho-mqtt
PKG_VERSION:=1.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pypi.python.org/packages/82/d9/7064d3a0a1d62756a1a809c85b99f864c641b66de84c15458f72193b7708
PKG_MD5SUM:=9100a6aa706ab699d414ec02705a21eb66f436184691d0bf1f2a85a6213c6c1f

PKG_LICENSE:=EPL-1.0
PKG_LICENSE_FILES:=LICENSE.txt
PKG_MAINTAINER:=

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/python-paho-mqtt
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=python-paho-mqtt
  URL:=http://www.eclipse.org/paho/
  DEPENDS:=+python-base +python-xml +python-openssl +libopenssl
endef

define Package/python-paho-mqtt/description
MQTT version 3.1.1 client class
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix="/usr" --root="$(PKG_INSTALL_DIR)")
endef

define Package/python-paho-mqtt/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(1)$(PYTHON_PKG_DIR)
endef

$(eval $(call BuildPackage,python-paho-mqtt))
