# Created by: Volker Theile <votdev@gmx.de>
# $FreeBSD$

PORTNAME=	ushare
PORTVERSION=	1.1a
PORTREVISION=	10
CATEGORIES=	net
MASTER_SITES=	http://ushare.geexbox.org/releases/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Lightweight UPnP (TM) A/V Media Server

LIB_DEPENDS=	libupnp.so:${PORTSDIR}/devel/upnp

HAS_CONFIGURE=	yes
USES=		gettext gmake pkgconfig tar:bzip2
LDFLAGS+=	-L${LOCALBASE}/lib -lintl

CFLAGS+=	-I${LOCALBASE}/include -I${WRKSRC}

MAN1=		${PORTNAME}.1

OPTION_DEFINE=	LIBDLNA
LIBDLNA_DESC=	DLNA (PS3) support

NO_STAGE=	yes
.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MLIBDLNA}
LIB_DEPENDS+=	libdlna.so:${PORTSDIR}/devel/libdlna
CONFIGURE_ARGS=	--enable-dlna
.endif

do-install:
	${INSTALL_SCRIPT} ${WRKSRC}/src/${PORTNAME} ${PREFIX}/bin
	${CP} ${WRKSRC}/scripts/${PORTNAME}.conf \
		${PREFIX}/etc/${PORTNAME}.conf.sample
	${INSTALL_SCRIPT} ${WRKSRC}/scripts/${PORTNAME} ${PREFIX}/etc/rc.d
	${INSTALL_MAN} ${WRKSRC}/src/${PORTNAME}.1 ${PREFIX}/man/man1

post-install:
	${CP} -np ${PREFIX}/etc/${PORTNAME}.conf.sample \
		${PREFIX}/etc/${PORTNAME}.conf || ${TRUE}

.include <bsd.port.mk>
