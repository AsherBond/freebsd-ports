# Created by: Kai Wang <kaiw27@gmail.com>
# $FreeBSD$

PORTNAME=	mpd
PORTVERSION=	1.0.1
PORTREVISION=	2
CATEGORIES=	lang
MASTER_SITES=	http://www.cs.arizona.edu/mpd/download/ \
		http://crypto.riken.go.jp/pub/NetBSD/packages/distfiles/mpd-language/
DISTNAME=	${PORTNAME}.${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Concurrent programming language

ONLY_FOR_ARCHS=	i386
ONLY_FOR_ARCHS_REASON=	uses assembly code for the target machine

# net/mpd
CONFLICTS=	mpd-[^1]*
NO_LATEST_LINK=	yes

USES=		gmake tar:tgz

OPTIONS_DEFINE=	X11 DOCS
OPTIONS_DEFAULT=	X11

MAN1=		mpd.1 mpdl.1 mpdm.1 mpdprof.1
MAN3=		mpdanimator.3 mpdgetopt.3 mpdwin.3
MAN5=		mpdmap.5 mpdtrace.5

NO_STAGE=	yes
.include <bsd.port.pre.mk>

.if ! ${PORT_OPTIONS:MX11}
PLIST_SUB+=	X11="@comment "
.else
PLIST_SUB+=	X11=""
USE_XORG=	x11
.endif

post-patch:
	@${REINPLACE_CMD} -Ee \
		"s%^(CCPATH =) .*%\1 `${WHICH} ${CC}`%; \
		 s%^(MPDSRC =) .*%\1 ${WRKSRC}%; \
		 s%^((MPD(CMD|LIB)|MAN[135]) =) /usr/local%\1 ${PREFIX}%" \
		 ${WRKSRC}/Configuration
.if ${PORT_OPTIONS:MX11}
	@${REINPLACE_CMD} -Ee 's%^(XINCL =) .*%\1 ${LOCALBASE}/include%' \
		${WRKSRC}/Configuration
.else
	@${REINPLACE_CMD} -Ee 's%^(XINCL =) .*%\1%' ${WRKSRC}/Configuration
.endif

pre-install:
	@${MKDIR} ${PREFIX}/lib/mpd

post-install:
.if ${PORT_OPTIONS:MDOCS}
	@${MKDIR} ${DOCSDIR}
	@${INSTALL_DATA} ${WRKSRC}/doc/* ${DOCSDIR}
	@${MKDIR} ${EXAMPLESDIR}
	@${CP} -pR ${WRKSRC}/vsuite/examples/* ${EXAMPLESDIR}
.endif

.include <bsd.port.post.mk>
