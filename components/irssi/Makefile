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
# Copyright (c) 2015, 2018, Oracle and/or its affiliates. All rights reserved.
#
BUILD_BITS= 64
include ../../make-rules/shared-macros.mk

COMPONENT_NAME=         irssi
COMPONENT_VERSION=	1.0.7
COMPONENT_PROJECT_URL=	https://irssi.org/
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=\
    sha256:732291e4e39fd928da2a599757c4309fe75bc769d0a783149b7a8e5e928ec987
COMPONENT_ARCHIVE_URL=	https://github.com/irssi/irssi/releases/download/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_SIG_URL=	$(COMPONENT_ARCHIVE_URL).asc
COMPONENT_ANITYA_ID=	1404

TPNO=		41222

TEST_TARGET= $(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

# Part of the build just runs "cc" (not the path that configure finds).
COMPONENT_BUILD_ENV +=  PATH=$(dir $(CC)):$(PATH)

CONFIGURE_ENV += "ac_cv_path_perlpath=$(PERL)"

CONFIGURE_OPTIONS +=    --sysconfdir=$(ETCDIR)
CONFIGURE_OPTIONS +=    --with-perl
CONFIGURE_OPTIONS +=    --with-proxy
CONFIGURE_OPTIONS +=    --with-perl-lib=$(USRDIR)/perl5/vendor_perl/$(PERL_VERSION)

REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/ncurses
REQUIRED_PACKAGES += library/security/openssl
REQUIRED_PACKAGES += $(PERL_PKG)
