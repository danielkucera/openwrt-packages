#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=ljalves-media
PKG_VERSION:=snapshot-20181207
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/danielkucera/ljalves-media.git
PKG_SOURCE_VERSION:=f279cf5271c6270bfd0220db3db519632c5ac719
PKG_MIRROR_HASH:=1bcb18348310fc744b8a5ee1e693fc69b3f11b6fde71c53246d61ab38e347ba4

PKG_MAINTAINER:=Daniel Kucera <github@danman.eu>

include $(INCLUDE_DIR)/package.mk

define KernelPackage/ljalves-media
  SUBMENU:=Multimedia
  TITLE:=Multimedia kernel drivers by ljalves
  URL:=https://github.com/ljalves/media_build
  DEPENDS:=+kmod-i2c-algo-bit
  FILES:= \
	  $(PKG_BUILD_DIR)/media_build/v4l/*.ko
endef

define Build/Compile
	cp files/DVB_SAA716X_TBS.config $(PKG_BUILD_DIR)/media_build/v4l/.config
	cd $(PKG_BUILD_DIR)/media_build && \
	unset TOPDIR && \
	$(MAKE) release DIR=$(KERNEL_BUILD_DIR)/linux-4.14.63/ && \
	$(MAKE) dir DIR=../media && \
	$(MAKE) -j10 CROSS_COMPILE=mipsel-openwrt-linux-musl- ARCH=mips
endef

define KernelPackage/ljalves-media/install
	$(INSTALL_DIR) $(1)/lib/firmware
	$(INSTALL_DATA) files/dvb-fe-cx24117.fw $(1)/lib/firmware/dvb-fe-cx24117.fw
endef

$(eval $(call KernelPackage,ljalves-media))
