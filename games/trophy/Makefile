# Created by: Jean-Yves Lefort <jylefort@brutele.be>
# $FreeBSD$

PORTNAME=	trophy
PORTVERSION=	2.0.3
PORTREVISION=	3
CATEGORIES=	games
MASTER_SITES=	SF

MAINTAINER=	makc@FreeBSD.org
COMMENT=	Single player racing game

LICENSE=	GPLv2

LIB_DEPENDS=	libclanCore.so:${PORTSDIR}/devel/clanlib1

USES=		pkgconfig

GNU_CONFIGURE=	yes
CPPFLAGS+=	-I${LOCALBASE}/include
LIBS+=		-L${LOCALBASE}/lib

PORTDOCS=	AUTHORS COPYING ChangeLog README TODO

OPTIONS_DEFINE=	DOCS

.include <bsd.port.options.mk>

pre-configure:
	${REINPLACE_CMD} -e "/^icondir =/s,icons,pixmaps," \
		${WRKSRC}/resources/Makefile.in

post-install:
.if ${PORT_OPTIONS:MDOCS}
	${MKDIR} ${STAGEDIR}${DOCSDIR} && \
	cd ${WRKSRC} && ${INSTALL_DATA} ${PORTDOCS} ${STAGEDIR}${DOCSDIR}
.endif

.include <bsd.port.mk>
