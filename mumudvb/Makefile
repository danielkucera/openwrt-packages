#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mumudvb
PKG_VERSION:=snapshot-20190121
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/braice/MuMuDVB.git
PKG_SOURCE_VERSION:=a8840c73bd148c66258f7bc51a413e456b7caab3
PKG_MIRROR_HASH:=ad1b0e1e0ace23fad4de1d0a30fce131269d84fdfcd15a293ecc8ad480935f73

PKG_MAINTAINER:=Daniel Kucera <github@danman.eu>

#PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/mumudvb
  TITLE:=MuMuDVB
  URL:=https://github.com/braice/MuMuDVB
  SECTION:=multimedia
  CATEGORY:=Multimedia
#  DEPENDS := 
endef

define Build/Configure
        cd $(PKG_BUILD_DIR) && \
	sed -i 's/^AM_ICONV//' configure.ac && \
        autoreconf -i && \
        $(call Build/Configure/Default,--with-linux-headers=$(LINUX_DIR))
endef

define Package/mumudvb/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/mumudvb $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/mumudvb.init $(1)/etc/init.d/mumudvb
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_BIN) ./files/mumudvb.conf $(1)/etc/mumudvb.conf
endef

$(eval $(call BuildPackage,mumudvb))
