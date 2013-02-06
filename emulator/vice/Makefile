# 
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=vice
PKG_VERSION:=2.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.zimmers.net/anonftp/pub/cbm/crossplatform/emulators/VICE/
PKG_MD5SUM:=6737f540806205384e9129026898b0a1

include $(INCLUDE_DIR)/package.mk

define Package/vice/Default
  SUBMENU:=Vice
  SECTION:=emulator
  CATEGORY:=Emulators
  TITLE:=Vice 64
  URL:=http://www.viceteam.org/
  DEPENDS:=+libbsd +libsdl +libjpeg +libpng +zlib
endef

define Package/vice/Default/description
 VICE is a program that executes programs intended for the old 8-bit computers.
 The current version emulates the C64, the C64DTV, the C128, the VIC20, almost all
 PET models, the PLUS4 and the CBM-II (aka C610).
endef

define Package/vice
$(call Package/vice/Default)
endef

define Package/vice/description
$(call Package/vice/Default/description)
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--without-resid \
		--disable-realdevice \
		--with-sdl \
		--enable-sdlui \
		--without-oss \
		--disable-ffmpeg \
		--disable-lame \
	)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR="$(PKG_INSTALL_DIR)" install
endef

define Package/vice/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/x64 $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib/vice/C64
	$(INSTALL_DIR) $(1)/usr/lib/vice/DRIVES
	$(INSTALL_DIR) $(1)/usr/lib/vice/fonts
	$(INSTALL_DIR) $(1)/usr/lib/vice/PRINTER
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/vice/C64/* $(1)/usr/lib/vice/C64
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/vice/DRIVES/* $(1)/usr/lib/vice/DRIVES
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/vice/fonts/* $(1)/usr/lib/vice/fonts
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/vice/PRINTER/* $(1)/usr/lib/vice/PRINTER
endef

$(eval $(call BuildPackage,vice))

