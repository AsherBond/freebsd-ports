# Created by: Carlo Strub
# $FreeBSD$

PORTNAME=	qbzr
PORTVERSION=	0.23.0
PORTREVISION=	4
CATEGORIES=	devel
MASTER_SITES=	http://launchpadlibrarian.net/109906138/ \
		http://www.c-s.li/ports/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Qt interface for bzr

LICENSE=	GPLv2

BUILD_DEPENDS=	bzr:${PORTSDIR}/devel/bzr \
		${PYTHON_PKGNAMEPREFIX}qt4-core>=0:${PORTSDIR}/devel/py-qt4 \
		${PYTHON_PKGNAMEPREFIX}pygments>=0:${PORTSDIR}/textproc/py-pygments \
		${PYTHON_PKGNAMEPREFIX}enchant>=0:${PORTSDIR}/textproc/py-enchant
RUN_DEPENDS=	bzr:${PORTSDIR}/devel/bzr

WRKSRC=		${WRKDIR}/${PORTNAME}

USE_PYTHON=		yes
USE_PYDISTUTILS=	yes
PYDISTUTILS_AUTOPLIST=	yes
USE_QT4=	# empty
USES=		gettext
INSTALLS_ICONS=	yes

.include <bsd.port.mk>
