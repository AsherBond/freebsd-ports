# Created by: Dereckson <dereckson@gmail.com>
# $FreeBSD$

PORTNAME=	komodo-ide
PORTVERSION=	6.1.1
CATEGORIES=	editors
MASTER_SITES=	http://downloads.activestate.com/Komodo/releases/${PORTVERSION}/
DISTNAME=	Komodo-IDE-${PORTVERSION}-61234-linux-libcpp6-x86

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Multi-language editor from ActiveState

CONFLICTS=	komodo-edit-*

ONLY_FOR_ARCHS=	i386 amd64
NO_BUILD=	yes
USE_LINUX=	f10
USE_LINUX_APPS=	gtk2 jpeg dbusglib alsalib
USE_LDCONFIG=	yes
USE_PYTHON=	yes

LICENSE=	AKIDELA
LICENSE_FILE=	${WRKSRC}/license.txt
LICENSE_NAME=	ActiveState Komodo IDE license agreement
LICENSE_PERMS=

NO_STAGE=	yes
.include <bsd.port.pre.mk>

.if defined(BATCH) || defined(PACKAGE_BUILDING)
IGNORE='You must accept the license prior to building.'
.endif

.if ${OSVERSION} < 800000
BROKEN=		fails to install
.endif

do-install:
	${MKDIR} ${DESKTOPDIR}
	cd ${WRKSRC} && ${SH} install.sh -I ${DATADIR} -s
	${LN} -sf ${DATADIR}/bin/komodo ${PREFIX}/bin/
	${LN} -sf ${DATADIR}/share/desktop/komodo-ide-6.desktop ${DESKTOPDIR}/

.include <bsd.port.post.mk>
