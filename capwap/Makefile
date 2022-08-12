include $(TOPDIR)/rules.mk

# Name, version and release number
# The name and version of your package are used to define the variable to point to the build directory of your package: $(PKG_BUILD_DIR)
PKG_NAME:=capwap
PKG_VERSION:=1.0.0
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

USE_SOURCE_DIR:=$(TOPDIR)/noc_src/capwap

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=Nova
  CATEGORY:=Nova
  TITLE:=$(PKG_NAME)
  DEPENDS:=+libnl +libopenssl
endef

define Package/$(PKG_NAME)/description
	open capwap
endef

# cd ${USE_SOURCE_DIR} && \
# make -j all VERBOSE=1 SYSROOT=${STAGING_DIR} CC=${TARGET_CC} AR=${TARGET_AR} LD=${TARGET_CC} 
define Build/Compile
	$(call Build/Compile/Default,)
endef

define Build/Clean
	$(call Build/Clean/Default,)
	cd ${USE_SOURCE_DIR} && \
	make -j1 clean
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/data/bin
	$(INSTALL_DIR) $(1)/data/config/capwap
	$(INSTALL_DIR) $(1)/etc/init.d

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/WTP $(1)/data/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/AC 	$(1)/data/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/WUA $(1)/data/bin/

	${CP} $(PKG_BUILD_DIR)/config.ac 		$(1)/data/config/capwap/
	${CP} $(PKG_BUILD_DIR)/settings.ac.txt 	$(1)/data/config/capwap/
	
	${CP} $(PKG_BUILD_DIR)/config.wtp 		$(1)/data/config/capwap/
	${CP} $(PKG_BUILD_DIR)/settings.wtp.txt	$(1)/data/config/capwap/

	${CP} $(PKG_BUILD_DIR)/root.pem			$(1)/data/config/capwap/
	${CP} $(PKG_BUILD_DIR)/server.pem		$(1)/data/config/capwap/
	${CP} $(PKG_BUILD_DIR)/client.pem		$(1)/data/config/capwap/

	${CP} $(PKG_BUILD_DIR)/.env				$(1)/data/config/capwap/

	$(CP) ./files/* $(1)/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
