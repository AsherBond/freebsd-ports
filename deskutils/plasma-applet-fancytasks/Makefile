# Created by: Gvozdikov Veniamin <g.veniamin@googlemail.com>
# $FreeBSD$

PORTNAME=	fancytasks
PORTVERSION=	1.1.0
PORTREVISION=	5
CATEGORIES=	deskutils
MASTER_SITES=	http://kde-look.org/CONTENT/content-files/
PKGNAMEPREFIX=	plasma-applet-
DISTNAME=	99737-${PORTNAME}-${PORTVERSION}

MAINTAINER=	vg@FreeBSD.org
COMMENT=	Plasmoid fancy representation of your tasks and launchers

LICENSE=	GPLv2

USES=		cmake tar:bzip2
USE_KDE4=	automoc4 kdeprefix kdelibs workspace qimageblitz
USE_QT4=	qmake_build moc_build rcc_build uic_build

WRKSRC=		${WRKDIR}/${PORTNAME}-${PORTVERSION}

.include <bsd.port.mk>
