#
# Copyright (C) 2017 Daniel Engberg <daniel.engberg.lists@pyret.net>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pcsc-tools
PKG_VERSION=1.5.2
PKG_RELEASE:=1
PKG_MAINTAINER:=Daniel Engberg <daniel.engberg.lists@pyret.net>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://ludovic.rousseau.free.fr/softwares/pcsc-tools/
PKG_HASH:=ff4e087c76700aa5a25dd7d0bc4f55bb4a5e71cd4f0d6b5301babe0b434f86fc

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/pcsc-tools
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libpcsclite
  TITLE:=pcsc-tools
  URL:=http://ludovic.rousseau.free.fr/softwares/pcsc-tools/
endef

define Package/pcsc-tools/description
  Tools that are used to test a PC/SC driver, card or reader.
  Only includes pcsc_scan without ATR analysis for now.
endef

define Package/pcsc-tools/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pcsc_scan $(1)/opt/bin
endef

$(eval $(call BuildPackage,pcsc-tools))
