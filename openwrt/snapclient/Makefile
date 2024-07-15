#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME := snapclient
PKG_VERSION := 0.28.0
PKG_RELEASE := $(PKG_SOURCE_VERSION)
PKG_USE_MIPS16 := 0

# PKG_MIRROR_HASH=skip
PKG_MIRROR_HASH:=253a3efa37bb82884b0364902821c70c40f958035cf15ffd436995c2a566a17d
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/badaix/snapcast.git
PKG_SOURCE_VERSION:=v0.28.0
PKG_BUILD_DIR:=$(BUILD_DIR)/snapcast-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS += -DBUILD_TESTS=OFF

define Package/snapcast/Default
	SECTION := sound
	CATEGORY := Sound
	TITLE := Synchronous multiroom audio player
	DEPENDS := +AUDIO_SUPPORT:alsa-lib +libstdcpp +libavahi-client +libatomic +libogg +libflac +libopus +boost +libsoxr
	URL := https://github.com/badaix/snapcast
endef

define Package/snapcast/description/Default
	Synchronous audio player
endef

define Package/snapclient
	$(call Package/snapcast/Default)
	TILE += Snapclient
	DEPENDS += +libvorbisidec +libsoxr
	DEFAULT := y
endef

define Package/snapclient/description
	$(call Package/snapcast/description/Default)
	Snapcast client
endef

define Package/snapclient/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/snapclient $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/snapclient.init $(1)/etc/init.d/snapclient
	$(INSTALL_DIR) $(1)/etc/default
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/extras/package/debian/snapclient.default $(1)/etc/default/snapclient
endef

$(eval $(call BuildPackage,snapclient))

