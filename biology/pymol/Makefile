# Created by: Nakata Maho <chat95@mbox.kyoto-inet.or.jp>
# $FreeBSD$

PORTNAME=	pymol
PORTVERSION=	${VERSION}.${SVNREVISION}
PORTREVISION=	3
CATEGORIES=	biology python
MASTER_SITES=	${MASTER_SITE_LOCAL:S|%SUBDIR%|maho/pymol|}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Free and Open-Source molecular modeling system

BUILD_DEPENDS=	${PYNUMERIC}
RUN_DEPENDS=	${PYNUMERIC} \
		${PYTHON_SITELIBDIR}/Pmw:${PORTSDIR}/x11-toolkits/py-Pmw
LIB_DEPENDS=	libpng15.so:${PORTSDIR}/graphics/png \
		libfreetype.so:${PORTSDIR}/print/freetype2

VERSION=	1.5.0.1
SVNREVISION=	3978

WRKSRC=		${WRKDIR}/pymol-${PORTVERSION}
USE_GL=		glut glew
USES=		gmake tar:bzip2
USE_PYTHON=	yes
PLIST_SUB=	PYMOL_VER=${VERSION} PYTHON_VER=${PYTHON_VER}

NO_STAGE=	yes
pre-build:
	@${REINPLACE_CMD} -e "s+%%LOCALBASE%%+${LOCALBASE}+"  ${WRKSRC}/setup.py

#do build process actually installs some files, so omitted.
do-build:

do-install:
	@(cd ${BUILD_WRKSRC}; ${SETENV} ${MAKE_ENV} ${PYTHON_CMD} ${PYSETUP} install)
	@(cd ${BUILD_WRKSRC}; ${SETENV} ${MAKE_ENV} ${PYTHON_CMD} setup2.py install)
	@${INSTALL_SCRIPT} ${WRKSRC}/pymol ${PREFIX}/bin/pymol

#maintainance
do-fetch-svn:
	#svn ls https://pymol.svn.sourceforge.net/svnroot/pymol/tags
	#http://pymol.svn.sourceforge.net/viewvc/pymol/trunk/
	${RM} -rf pymol-${VERSION}.${SVNREVISION}
	svn -r ${SVNREVISION} export http://pymol.svn.sourceforge.net/svnroot/pymol/trunk/pymol pymol-${VERSION}.${SVNREVISION}
	tar cvfj pymol-${VERSION}.${SVNREVISION}.tar.bz2 pymol-${VERSION}.${SVNREVISION}
	scp pymol-${VERSION}.${SVNREVISION}.tar.bz2 freefall.freebsd.org:public_distfiles/pymol/

.include <bsd.port.mk>
