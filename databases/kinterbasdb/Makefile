# Created by: Dmytro Rud <rud@cs.uni-magdeburg.de>
# $FreeBSD$

PORTNAME=		kinterbasdb
PORTVERSION=		3.2
CATEGORIES=		databases python
MASTER_SITES=		SF/${PORTNAME}/${PORTNAME}/${PORTNAME}-${PORTVERSION}
PKGNAMEPREFIX=		${PYTHON_PKGNAMEPREFIX}
DISTNAME=		${PORTNAME}-${PORTVERSION}.src

MAINTAINER=		ports@FreeBSD.org
COMMENT=		Python extension for Firebird/Interbase(R) relational databases

BROKEN=			Does not build with modern compilers

RUN_DEPENDS=		${PYTHON_SITELIBDIR}/mx/DateTime/__init__.py:${PORTSDIR}/lang/py-mx-base

WRKSRC=			${WRKDIR}/${PORTNAME}-${PORTVERSION}

USE_FIREBIRD=		yes
USE_PYTHON=		yes
USE_PYDISTUTILS=	yes
USE_PYTHON_PREFIX=	yes

PLIST_SUB=		INSTALLDIR=lib/${PYTHON_VERSION}/site-packages/${PORTNAME}

NO_STAGE=	yes
post-extract:
	@${REINPLACE_CMD} -e "s@DEFAULT_FREEBSD_HOME_DIR = '.*'@DEFAULT_FREEBSD_HOME_DIR = '${LOCALBASE}'@" \
		${WRKSRC}/setup.py

.include <bsd.port.mk>
