# Created by: bsam
# $FreeBSD$

PORTNAME=		upx
PORTVERSION=		3.03
CATEGORIES=		archivers linux
MASTER_SITES=		CRITICAL/rpm/${LINUX_RPM_ARCH}/fedora/${LINUX_DIST_VER}
PKGNAMEPREFIX=		linux-f10-
DISTNAME=		${PORTNAME}-${PORTVERSION}-${RPMVERSION}

MAINTAINER=		emulation@FreeBSD.org
COMMENT=		UPX, a high-performance executable packer (Linux Fedora 10)

CONFLICTS=		linux-upx-[0-9]* linux-f8-upx-[0-9]*

USE_LINUX_RPM=		yes
USE_LINUX_APPS=		ucl
LINUX_DIST_VER=		10
RPMVERSION=		1.fc10
BRANDELF_FILES=		usr/bin/upx

PLIST_FILES=		usr/bin/upx usr/share/man/man1/upx.1.gz
DOCSDIR=		${PREFIX}/usr/share/doc/${PORTNAME}-${PORTVERSION}
PORTDOCS=		BUGS COPYING LICENSE NEWS PROJECTS README README.1ST \
			THANKS TODO elf-to-mem.txt filter.txt loader.txt selinux.txt
DESCR=			${.CURDIR}/../${PORTNAME}/pkg-descr

OPTIONS_DEFINE=		DOCS

.include <bsd.port.mk>
