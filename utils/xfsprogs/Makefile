#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xfsprogs
PKG_VERSION:=5.8.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@KERNEL/linux/utils/fs/xfs/xfsprogs
PKG_HASH:=8ef46ed9e6bb927f407f541dc4324857c908ddf1374265edc910d23724048c6b

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_CPE_ID:=cpe:/a:sgi:xfsprogs

include $(INCLUDE_DIR)/package.mk

define Package/xfsprogs/default
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Filesystem
  DEPENDS:=+libuuid +libpthread
  URL:=https://xfs.org/
endef

define Package/xfs-admin
$(call Package/xfsprogs/default)
  TITLE:=Utilities for changing parameters of an XFS filesystems
endef

define Package/xfs-mkfs
$(call Package/xfsprogs/default)
  TITLE:=Utility for creating XFS filesystems
endef

define Package/xfs-fsck
$(call Package/xfsprogs/default)
  TITLE:=Utilities for checking and repairing XFS filesystems
endef

define Package/xfs-growfs
$(call Package/xfsprogs/default)
  TITLE:=Utility for increasing the size of XFS filesystems
endef

CONFIGURE_ARGS += \
	--disable-gettext \
	--disable-blkid \
	--disable-readline \
	--disable-editline \
	--disable-termcap \
	--disable-lib64 \
	--disable-librt \
	--disable-ubisan \
	--disable-addrsan \
	--disable-threadsan \
	--disable-scrub \
	--disable-libicu

TARGET_CFLAGS += -DHAVE_MAP_SYNC

define Package/xfs-admin/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/xfs_db $(1)/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/xfs_admin $(1)/sbin
endef

define Package/xfs-mkfs/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/sbin/mkfs.xfs $(1)/usr/sbin
endef

define Package/xfs-fsck/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/sbin/xfs_repair $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/xfs_db $(1)/usr/sbin
endef

define Package/xfs-growfs/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/xfs_growfs $(1)/usr/sbin
endef

$(eval $(call BuildPackage,xfs-admin))
$(eval $(call BuildPackage,xfs-mkfs))
$(eval $(call BuildPackage,xfs-fsck))
$(eval $(call BuildPackage,xfs-growfs))
