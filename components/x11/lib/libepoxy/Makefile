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
# Copyright (c) 2018, Oracle and/or its affiliates. All rights reserved.
#

BUILD_BITS =            64_and_32
COMPILER=		gcc
include ../../../../make-rules/shared-macros.mk

COMPONENT_NAME=		libepoxy
COMPONENT_VERSION=	1.4.0
COMPONENT_PROJECT_URL=  https://github.com/anholt/libepoxy
COMPONENT_ARCHIVE=	$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_URL=  $(COMPONENT_PROJECT_URL)/archive/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH= \
	sha256:935c74d4f8bdb1d2435f58ea95ac2a470368123e8e6f0618f6bc147c0956701b
COMPONENT_BUGDB=        x11/libraries
COMPONENT_ANITYA_ID=	6090
TPNO=			34679

# Tests need work to compile
TEST_TARGET = $(SKIP_TEST)

FIX_PC_FILES=epoxy.pc.in

include $(WS_MAKE_RULES)/x11-component.mk

COMPONENT_PREP_ACTION +=(cd $(@D); $(AUTORECONF_ENV) autoreconf -fiv);

REQUIRED_PACKAGES += x11/library/mesa
