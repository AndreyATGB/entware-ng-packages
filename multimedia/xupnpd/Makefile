#
# Copyright (C) 2013-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xupnpd
PKG_REV:=5c08c051caa0062cc1c401b2d26d1f36dffe9c55
PKG_VERSION:=2016-07-06
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/clark15b/xupnpd.git
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_MIRROR_HASH:=333e9938556c9a02b28732b5512626b991c65eaf0eb60d38e29f72ec513d312f

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=LICENSE

PKG_MAINTAINER:=Álvaro Fernández Rojas <noltari@gmail.com>

include $(INCLUDE_DIR)/package.mk

LUA_FLAGS:=-llua

define Build/Compile
	(cd $(PKG_BUILD_DIR)/src; $(TARGET_CC) -v $(LUA_FLAGS) $(TARGET_CFLAGS) -fno-exceptions -fno-rtti -DWITH_URANDOM $(TARGET_CPPFLAGS) $(TARGET_LDFLAGS) -lm -ldl -lcrypt -o xupnpd *.c *.cpp)
endef

define Package/xupnpd
  SECTION:=multimedia
  CATEGORY:=Multimedia
  DEPENDS:=+liblua
  TITLE:=eXtensible UPnP agent
  URL:=http://xupnpd.org/
endef

define Package/xupnpd/conffiles
/opt/share/xupnpd/xupnpd.lua
/opt/share/xupnpd/config
/opt/share/xupnpd/playlists
endef

define Package/xupnpd/description
xupnpd - eXtensible UPnP agent
This program is a light DLNA Media Server which provides ContentDirectory:1 service for sharing IPTV unicast streams over local area network (with udpxy for multicast to HTTP unicast conversion).
The program shares UTF8-encoded M3U playlists with links over local area network as content of the directory.
You can watch HDTV broadcasts (multicast or unicast) and listen Internet Radio in IP network without transcoding and PC.
endef

define Package/xupnpd/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/xupnpd $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S94xupnpd $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/share/xupnpd
	$(CP) $(PKG_BUILD_DIR)/src/*.lua $(1)/opt/share/xupnpd
	$(INSTALL_DIR) $(1)/opt/share/xupnpd/ui
	$(CP) $(PKG_BUILD_DIR)/src/ui/* $(1)/opt/share/xupnpd/ui
	$(INSTALL_DIR) $(1)/opt/share/xupnpd/www
	$(CP) $(PKG_BUILD_DIR)/src/www/* $(1)/opt/share/xupnpd/www
	$(INSTALL_DIR) $(1)/opt/share/xupnpd/playlists
	$(CP) $(PKG_BUILD_DIR)/src/playlists/* $(1)/opt/share/xupnpd/playlists
	$(INSTALL_DIR) $(1)/opt/share/xupnpd/plugins
	$(CP) $(PKG_BUILD_DIR)/src/plugins/* $(1)/opt/share/xupnpd/plugins
	$(INSTALL_DIR) $(1)/opt/share/xupnpd/config
	$(INSTALL_DIR) $(1)/opt/share/xupnpd/localmedia
	$(INSTALL_DIR) $(1)/opt/share/xupnpd/profiles
	$(CP) $(PKG_BUILD_DIR)/src/profiles/* $(1)/opt/share/xupnpd/profiles
endef

$(eval $(call BuildPackage,xupnpd))
