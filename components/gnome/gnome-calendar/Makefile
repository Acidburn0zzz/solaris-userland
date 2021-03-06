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
# Copyright (c) 2016, 2018, Oracle and/or its affiliates. All rights reserved.
#

BUILD_BITS=		64
COMPILER=		gcc
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gnome-calendar
COMPONENT_VERSION=	3.24.0
COMPONENT_PROJECT_URL=	https://wiki.gnome.org/Apps/Calendar
COMPONENT_ARCHIVE_HASH= \
	sha256:8a21f51e10ce491e4a492e21c47de29a9ba1b568f4e2fd6f4e33616609d413d0
COMPONENT_BUGDB=	gnome/applications
COMPONENT_ANITYA_ID=	10906

TPNO=			35138

TEST_TARGET= $(NO_TESTS)

include $(WS_MAKE_RULES)/gnome-component.mk

# Assumes GNU msgfmt in PATH.
CONFIGURE_ENV += PATH="$(GNUBIN):$(PATH)"

# evolution-data-server requires nss/nspr, but Solaris doesn't include a 64-bit
# pkg-config file for it, so we workaround this by using the one-off copy in the
# evolution-data-server component directory
PKG_CONFIG_PATHS += $(WS_COMPONENTS)/gnome/evolution-data-server

REQUIRED_PACKAGES += gnome/gsettings-desktop-schemas
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/desktop/evolution-data-server
REQUIRED_PACKAGES += library/desktop/gtk3
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/gnome/gnome-online-accounts
REQUIRED_PACKAGES += library/libical
REQUIRED_PACKAGES += system/library/math
