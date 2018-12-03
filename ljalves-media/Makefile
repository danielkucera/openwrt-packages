#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=ljalves-media
PKG_VERSION:=snapshot-20181203
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/danielkucera/ljalves-media.git
PKG_SOURCE_VERSION:=964fc4c9e0177fb4393bd5ea02e0f260c1f2fccb
PKG_MIRROR_HASH:=-1

PKG_MAINTAINER:=Daniel Kucera <github@danman.eu>

include $(INCLUDE_DIR)/package.mk

define KernelPackage/ljalves-media
  SUBMENU:=Multimedia
  TITLE:=Multimedia kernel drivers by ljalves
  URL:=https://github.com/ljalves/media_build
  FILES:= \
	  $(PKG_BUILD_DIR)/media_build/v4l/saa716x_budget.ko \
	  $(PKG_BUILD_DIR)/media_build/v4l/cx24117.ko \
	  $(PKG_BUILD_DIR)/media_build/v4l/saa716x_core.ko \
	  $(PKG_BUILD_DIR)/media_build/v4l/tas2101.ko
#  DEPENDS := +MINISATIP_DVBAPI:libdvbapi +MINISATIP_DVBCSA:libdvbcsa +MINISATIP_CI:libdvben50221 +MINISATIP_AES:libopenssl
endef

define Build/Compile
	cd $(PKG_BUILD_DIR)/media_build && \
	unset TOPDIR && \
	printenv && \
	$(MAKE) release DIR=$(KERNEL_BUILD_DIR)/linux-4.9.67 && \
	$(MAKE) dir DIR=../media && \
	echo "--- COMPILATION FOLLOWS ---" && \
	$(MAKE) -j10 CROSS_COMPILE=mipsel-openwrt-linux-musl- ARCH=mips CONFIG_DVB_SAA716X_BUDGET=m
endef

$(eval $(call KernelPackage,ljalves-media))
