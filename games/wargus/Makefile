# Created by: Travis Poppe <tlp@liquidx.org>
# $FreeBSD$

PORTNAME=	wargus
PORTVERSION=	2.2.5.5
PORTREVISION=	1
CATEGORIES=	games
MASTER_SITES=	http://launchpadlibrarian.net/59493162/
DISTNAME=	${PORTNAME}_${PORTVERSION}
EXTRACT_SUFX=	.orig.tar.gz

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Warcraft 2 mod that allows you to play Warcraft 2 with Stratagus

LICENSE=	GPLv2

LIB_DEPENDS=	libpng15.so:${PORTSDIR}/graphics/png
RUN_DEPENDS=	stratagus:${PORTSDIR}/games/stratagus

NOT_FOR_ARCHS=	sparc64
USES=		pathfix gmake pkgconfig
USE_GNOME=	gtk20
WRKSRC=		${WRKDIR}/${PORTNAME}-${PORTVERSION}
SUB_FILES=	${PORTNAME} pkg-message

MAKE_ARGS+=	CFLAGS+="-I${LOCALBASE}/include -I${LOCALBASE}/include/libpng15" LDFLAGS+=-L${LOCALBASE}/lib

do-install:
	${INSTALL_SCRIPT} ${WRKDIR}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin
	cd ${WRKSRC} && ${COPYTREE_SHARE} "campaigns contrib maps scripts" ${STAGEDIR}${DATADIR}
	${INSTALL_PROGRAM} ${WRKSRC}/wartool ${STAGEDIR}${DATADIR}
	${INSTALL_SCRIPT} ${WRKSRC}/build.sh ${STAGEDIR}${DATADIR}

.include <bsd.port.mk>
