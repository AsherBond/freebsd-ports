# $FreeBSD$

PORTNAME=	kanagram
PORTVERSION=	${KDE4_VERSION}
PORTREVISION=	1
CATEGORIES=	games kde
MASTER_SITES=	KDE/${KDE4_BRANCH}/${PORTVERSION}/src
DIST_SUBDIR=	KDE/${PORTVERSION}

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Letter order game for KDE 4

USE_KDE4=	kdehier kdelibs kdeprefix libkdeedu automoc4
USES=		cmake:outsource tar:xz
USE_QT4=	xml corelib declarative gui opengl script xml \
		moc_build qmake_build rcc_build uic_build
USE_LDCONFIG=	yes

.include <bsd.port.mk>
