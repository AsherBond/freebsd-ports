# $FreeBSD$

PORTNAME=	ktp-approver
PORTVERSION=	${KTP_VERSION}
PORTREVISION=	2
CATEGORIES=	net-im kde
MASTER_SITES=	${MASTER_SITE_KDE}
MASTER_SITE_SUBDIR=	${KTP_BRANCH}/kde-telepathy/${PORTVERSION}/src

MAINTAINER=	avilla@FreeBSD.org
COMMENT=	KDE instant messaging notifier

LIB_DEPENDS=	libtelepathy-qt4.so:${PORTSDIR}/net-im/telepathy-qt4 \
		libktpcommoninternalsprivate.so:${PORTSDIR}/net-im/ktp-common-internals
RUN_DEPENDS=	${KDE4_PREFIX}/bin/ktp-contactlist:${PORTSDIR}/net-im/ktp-contact-list

USE_KDE4=	kdehier kdeprefix kdelibs automoc4
USE_QT4=	corelib moc_build qmake_build rcc_build uic_build
USES=		cmake gettext tar:bzip2

.include <bsd.port.mk>
