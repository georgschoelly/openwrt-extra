include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=cifsd
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/namjaejeon/cifsd.git
PKG_SOURCE_DATE:=2019-02-08
PKG_SOURCE_VERSION:=04a898c9c40f3b8e556c9c57226f8c29fce8c337
PKG_MIRROR_HASH:=4c9c76fef75bb2ca8a6aa0f61583041664166b9009698cba1d8a8cd8358b0763

PKG_MAINTAINER:=Andy Walsh <andy.walsh44+github@gmail.com>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

define KernelPackage/fs-cifsd
	SUBMENU:=Filesystems
	TITLE:=CIFS/SMB kernel server support
	FILES:=$(PKG_BUILD_DIR)/cifsd.$(LINUX_KMOD_SUFFIX)
	DEPENDS+= \
		+kmod-nls-base \
		+kmod-nls-utf8 \
		+kmod-crypto-md4 \
		+kmod-crypto-md5 \
		+kmod-crypto-hmac \
		+kmod-crypto-ecb \
		+kmod-crypto-des \
		+kmod-crypto-sha256 \
		+kmod-crypto-cmac \
		+kmod-crypto-sha512 \
		+kmod-crypto-aead \
		+kmod-crypto-ccm
	KCONFIG:= \
		CONFIG_KEYS=y \
		CONFIG_CRYPTO_ARC4=y
endef

define KernelPackage/fs-cifsd/description
	Kernel module for a CIFS/SMBv2,3 fileserver.
endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		ARCH="$(LINUX_KARCH)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		M="$(PKG_BUILD_DIR)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		CONFIG_CIFS_SERVER=m \
		modules
endef

$(eval $(call KernelPackage,fs-cifsd))
