#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=serdisplib
PKG_VERSION:=2.02
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://svn.code.sf.net/p/serdisplib/code/serdisplib/trunk
#PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=svn
PKG_SOURCE_VERSION:=HEAD

#PKG_MD5SUM:=4eb17cd70aa963c30a237d426ac24449

include $(INCLUDE_DIR)/package.mk

define Package/serdisplib
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=A display control library
  URL:=http://serdisplib.sourceforge.net/
  DEPENDS:=+libusb-compat
endef

define Package/serdisplib/description
	serdisplib is a library to drive serial and parallel displays
	with built-in controllers.
endef

CONFIGURE_ARGS+= \
	--enable-shared \
	--enable-static \

TARGET_CFLAGS += $(FPIC)

define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		CFLAGS="$(TARGET_CFLAGS) -Wall -Wno-implicit -I../include -I.." \
		all
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/include/serdisplib $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/lib/libserdisp.{a,so*} $(1)/usr/lib/
endef

define Package/serdisplib/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/lib/libserdisp.so.* $(1)/usr/lib
endef

$(eval $(call BuildPackage,serdisplib))
