include $(TOPDIR)/rules.mk

PKG_NAME:=letmecreate
PKG_VERSION:=1.0
PKG_LICENSE:=BSD-3-Clause
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/francois-berder/LetMeCreate
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/letmecreate
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=LetMeCreate
endef

define Package/letmecreate/config
	source "$(SOURCE)/Config.in"
endef

CMAKE_OPTIONS += $(if $(CONFIG_LETMECREATE_BUILD_EXAMPLES),-DBUILD_EXAMPLES=ON)

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR)/usr/include/letmecreate
	$(CP) $(PKG_BUILD_DIR)/include/* $(STAGING_DIR)/usr/include/

	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/lib/*.so $(STAGING_DIR)/usr/lib/
endef

define Package/letmecreate/install
	if [ -d "$(PKG_BUILD_DIR)/examples/bin/" ]; then \
		mkdir -p $(1)/usr/bin/letmecreate_examples; \
		$(INSTALL_BIN) $(PKG_BUILD_DIR)/examples/bin/* $(1)/usr/bin/letmecreate_examples; \
	fi

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/lib/*.so $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/include/letmecreate
	$(CP) $(PKG_BUILD_DIR)/include/* $(1)/usr/include/letmecreate
endef

$(eval $(call BuildPackage,letmecreate))
