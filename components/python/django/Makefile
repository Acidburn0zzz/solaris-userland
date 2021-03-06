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
# Copyright (c) 2013, 2018, Oracle and/or its affiliates. All rights reserved.
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		Django
COMPONENT_VERSION=	1.11.1
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
    sha256:0809402ff678e7d726ef23ef0d6dc4f62cce1f9d8788c015bcc45de8e6d83a07
COMPONENT_ARCHIVE_URL=	$(call pypi_url)
COMPONENT_PROJECT_URL=	http://www.djangoproject.com/
COMPONENT_BUGDB=	python-mod/django
COMPONENT_ANITYA_ID=	3828

TPNO=			35473

# Depends on python-imaging which is not Python 3 ready.
PYTHON_VERSIONS=	$(PYTHON2_VERSIONS)

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/setup.py.mk
include $(WS_MAKE_RULES)/ips.mk

# Replace "#!/usr/bin/env ..." shebang lines with properly versioned ones.
COMPONENT_POST_BUILD_ACTION = \
    /usr/bin/find $(BUILD_DIR)/$(MACH)-$(PYTHON_VERSION)/lib/django -name *.py \
	-exec $(GSED) -i -e 's/env python/python$(PYTHON_VERSION)/' "{}" \; ;

COMPONENT_POST_INSTALL_ACTION = \
    (cd $(PROTO_DIR)/usr/bin ; \
     $(MV) -f django-admin.py django-admin-$(PYTHON_VERSION))

# add 1 extra transform to get rid of the facet created on
# locale/__init__.py
PUBLISH_TRANSFORMS +=	$(COMPONENT_DIR)/django-locale-transform

# reset the test environment to only contain PATH, PYTHONPATH, and LC_ALL
# (because many tests need to be able to access non-ASCII codepoints).
COMPONENT_TEST_DIR=	$(SOURCE_DIR)/tests
COMPONENT_TEST_ARGS +=	--settings test_sqlite
COMPONENT_TEST_ENV=	PYTHONPATH=$(SOURCE_DIR)
COMPONENT_TEST_ENV +=	LC_ALL=en_US.UTF-8

ASLR_MODE = $(ASLR_NOT_APPLICABLE)

# common targets
build:		$(BUILD_NO_ARCH)

install:	$(INSTALL_NO_ARCH)

# The tests are failing in non-consistent way. Usually there is
#  - bunch of locking issues "IOError: [Errno 9] Bad file number"
#  - test_use_for_related_fields_on_geomanager fails because we don't have GDAL
#    library
#  - test_urllib2_urlopen
#  - bunch of "HTTPError: HTTP Error 502: cannotconnect"
#  - test_project_template_tarball_url
#  - test_custom_project_template_from_tarball_by_url
test:		$(TEST_NO_ARCH)
COMPONENT_TEST_ARGS += --parallel=1
COMPONENT_TEST_ARGS += --verbosity=3

# To run single test you can just add it's name like here:
# COMPONENT_TEST_ARGS += admin_scripts.tests.StartProject
COMPONENT_TEST_MASTER = $(COMPONENT_TEST_RESULTS_DIR)/results-all.master

COMPONENT_TEST_TRANSFORMS += \
	` : Disable normal test output ` \
	'-n ' \
	'-e "s/^Ran .* tests in.*/Tests were executed/g"' \
	'-e "/Tests were executed/p"'

system-test:	$(SYSTEM_TESTS_NOT_IMPLEMENTED)

REQUIRED_PACKAGES += library/python/setuptools-27
REQUIRED_PACKAGES += text/gnu-gettext
