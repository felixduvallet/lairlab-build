REPO := https://googletest.googlecode.com/svn/trunk/
CHECKOUT_DIR := googletest-read-only

# Figure out where to build the software.
#   Use BUILD_PREFIX if it was passed in.
#   If not, search up to four parent directories for a 'build' directory.
#   Otherwise, use ./build.
ifeq "$(BUILD_PREFIX)" ""
BUILD_PREFIX:=$(shell for pfx in .. ../.. ../../.. ../../../..; do d=`pwd`/$$pfx/build;\
               if [ -d $$d ]; then echo $$d; exit 0; fi; done; echo `pwd`/build)
endif

.PHONY: configure build install

.NOTPARALLEL:  all

all : $(CHECKOUT_DIR)/build/Makefile build install

build:
	$(MAKE) -C $(CHECKOUT_DIR)/build all

# NOTE: copy files directly here, since gtest's cmake does not do this for us.
install:
	@cp $(CHECKOUT_DIR)/build/libgtest_main.a ${BUILD_PREFIX}/lib
	@cp $(CHECKOUT_DIR)/build/libgtest.a ${BUILD_PREFIX}/lib
	@svn export --force $(CHECKOUT_DIR)/include/gtest ${BUILD_PREFIX}/include/gtest/
	echo "Installed libs and include to ${BUILD_PREFIX}"

$(CHECKOUT_DIR)/build/Makefile:
	$(MAKE) configure

configure: $(CHECKOUT_DIR)/CMakeLists.txt
	@echo "\nBUILD_PREFIX: $(BUILD_PREFIX)\n\n"

	@mkdir -p $(CHECKOUT_DIR)/build

	@cd $(CHECKOUT_DIR)/build && cmake -DCMAKE_INSTALL_PREFIX=$(BUILD_PREFIX) ../

# Default to a less-verbose build.  If you want all the gory compiler output,
# run "make VERBOSE=1"
$(VERBOSE).SILENT:

# build quietly by default.  For a verbose build, run "make VERBOSE=1"
$(VERBOSE).SILENT:


$(CHECKOUT_DIR)/CMakeLists.txt:
	@svn checkout $(REPO) $(CHECKOUT_DIR)

clean:
	if [ -d ${CHECKOUT_DIR}/build ]; then \
	$(MAKE) -C ${CHECKOUT_DIR}/build clean; \
	fi

	rm -fr ${CHECKOUT_DIR}
