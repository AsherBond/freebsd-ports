# Created by: Hye-Shik Chang <perky@python.or.kr>
# $FreeBSD$

PORTNAME=	kmess
PORTVERSION=	2.0.6.2
PORTREVISION=	5
CATEGORIES=	net-im kde
MASTER_SITES=	SF/${PORTNAME}/Latest%20versions/${PORTVERSION}/

MAINTAINER=	syncer@gmail.com
COMMENT=	MSN Messenger client for KDE

LIB_DEPENDS=	libqca.so:${PORTSDIR}/devel/qca
RUN_DEPENDS=	qca-ossl>=2.0.0.b3:${PORTSDIR}/security/qca-ossl

LATEST_LINK=	${PORTNAME}-kde4

USE_GNOME=	libxml2 libxslt
USE_KDE4=	kdehier kdeprefix kdelibs libkonq automoc4
USE_QT4=	qmake_build moc_build rcc_build uic_build
USES=		cmake gettext tar:bzip2

.include <bsd.port.mk>
