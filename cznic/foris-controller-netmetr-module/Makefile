#
# Copyright (C) 2018 CZ.NIC z. s. p. o. (https://www.nic.cz/)
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=foris-controller-netmetr-module
PKG_VERSION:=0.3
PKG_RELEASE:=1
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://gitlab.labs.nic.cz/turris/foris-controller-netmetr-module.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILE:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../foris-controller/files/foris-controller-module.mk

$(call include_mk, python-package.mk)

define Package/$(PKG_NAME)
	TITLE:=$(PKG_NAME)
	DEPENDS:=\
		+foris-controller +netmetr
	MAINTAINER:=CZ.NIC <packaging@turris.cz>
endef

define Package/$(PKG_NAME)/description
 This is a netmetr module for foris-controller
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
endef

#
# Package install definition
$(eval $(call ForisControllerModule,$(PKG_NAME)))

define Package/$(PKG_NAME)/postinst
#!/bin/sh
set -x
if [ -z "$${IPKG_INSTROOT}" ]; then
	/etc/init.d/foris-controller restart
	netmetr
fi
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
