#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#

#
# Copyright (c) 2011, 2018, Oracle and/or its affiliates. All rights reserved.
#
BUILD_BITS= 64
include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		tcpdump
COMPONENT_VERSION=	4.9.2
COMPONENT_PROJECT_URL=	https://www.tcpdump.org/
COMPONENT_ARCHIVE_HASH=	\
    sha256:798b3536a29832ce0cbb07fafb1ce5097c95e308a6f592d14052e1ef1505fe79
COMPONENT_ARCHIVE_URL=	$(COMPONENT_PROJECT_URL)release/$(COMPONENT_ARCHIVE)
COMPONENT_SIG_URL=	$(COMPONENT_ARCHIVE_URL).sig
COMPONENT_ANITYA_ID=	4947

TPNO=			37776

# Enable adiheap and adistack security extensions
ADIHEAP_MODE =	$(ADIHEAP_ENABLE)
ADISTACK_MODE =	$(ADISTACK_ENABLE)

SYSTEM_TEST_TARGET= configure $(SYSTEM_TEST_64)
include $(WS_MAKE_RULES)/common.mk

ifeq ($(OS_VERSION),11.3)
# Prevent macro redefinition error
CFLAGS += -D _NETINET_IP_H
endif

# Rebuild the configure script so the man pages are normalized.
COMPONENT_PREP_ACTION = (cd $(@D); autoconf);

# fix my alignment issues instead of falling over on sparc
studio_ALIGN.sparc.64=-xmemalign=16i
CONFIGURE_OPTIONS.sparc += ac_cv___attribute__=no

# lazyloading (indirectly enabled by -Bdirect) seems to cause problems with
# libpcap device enumeration.
LD_B_DIRECT=

CONFIGURE_OPTIONS += --enable-ipv6=yes
CONFIGURE_OPTIONS += --with-user=nobody
CONFIGURE_OPTIONS += --without-crypto

COMPONENT_TEST_TRANSFORMS += \
	'-e "/Entering directory/d" ' \
	'-e "/Leaving directory/d" ' \
	'-e "/cd tests/d" '

COMPONENT_PRE_TEST_ACTION = \
        ($(CP) -r $(SOURCE_DIR)/tests $(@D)/.)

# We don't want to build tcpdump, so override the equivalent of "gmake check"
# in the main Makefile.
COMPONENT_SYSTEM_TEST_CMD =	./TESTrun.sh
COMPONENT_SYSTEM_TEST_DIR =	$(@D)/tests
COMPONENT_SYSTEM_TEST_ENV +=	TCPDUMP_BIN=$(USRSBINDIR)/tcpdump
COMPONENT_SYSTEM_TEST_TARGETS =
COMPONENT_PRE_SYSTEM_TEST_ACTION = \
        ($(CP) -r $(SOURCE_DIR)/tests $(@D)/.)

REQUIRED_PACKAGES += system/library/libpcap
