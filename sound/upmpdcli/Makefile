#
# Copyright (C) 2010-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=upmpdcli
PKG_SOURCE_VERSION:=v0.6.1
PKG_VERSION:=0.6.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://github.com/medoc92/upmpdcli.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/upmpdcli/Default
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=An UPnP front-end to MPD, the Music Player Daemon
  URL:=https://github.com/medoc92/upmpdcli
endef

define Package/libupnpp
$(call Package/upmpdcli/Default)
 SECTION:=libs
 CATEGORY:=Libraries
 TITLE+= libraries
 DEPENDS:= +libstdcpp +libupnp +libmpdclient +libexpat
endef

define Package/upmpdcli
$(call Package/upmpdcli/Default)
  DEPENDS:= +libupnpp
endef

define Package/upmpdcli/description
  upmpdcli implements an UPnP Media Renderer, using MPD to perform the real work.
endef

define Package/libupnpp/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/.libs/libupnpp*.so $(1)/usr/lib/
endef

define Package/upmpdcli/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/.libs/upmpdcli $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/upmpdcli.init $(1)/etc/init.d/upmpdcli
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/upmpd/upmpdcli.conf $(1)/etc/upmpdcli.conf
	$(INSTALL_DIR) $(1)/usr/share/upmpdcli
	$(CP) $(PKG_BUILD_DIR)/upmpd/*.xml $(1)/usr/share/upmpdcli
endef

define Package/upmpdcli/conffiles
/etc/upmpdcli.conf
endef

$(eval $(call BuildPackage,libupnpp))
$(eval $(call BuildPackage,upmpdcli))
