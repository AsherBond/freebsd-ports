# Created by: Lars Koeller <Lars_Koeller@odie.physik2.uni-rostock.de>
# $FreeBSD$

PORTNAME=	faces
PORTVERSION=	1.7.7
PORTREVISION=	9
CATEGORIES=	mail
MASTER_SITES=	SF

MAINTAINER=	ashish@FreeBSD.org
COMMENT=	Visual mail, user, and print face server

OPTIONS_DEFINE=	X11 NAS RPLAY SOX DOCS NLS
OPTIONS_DEFAULT=	X11
X11_DESC=	X11/GTK support
RPLAY_DESC=	rplay audio support
SOX_DESC=	Sox audio support

WANT_GNOME=	yes
USE_LDCONFIG=	yes

PORTDOCS=	README

.include <bsd.port.pre.mk>

.if ! ${PORT_OPTIONS:MX11}
PLIST_SUB+=	X11="@comment "
WITH_AUDIO=	# none
.else # with X11
PLIST_SUB+=	X11=""
USE_GNOME=	gnomehack gtk12
GNU_CONFIGURE=	yes
CPPFLAGS+=	-I../compface -I${LOCALBASE}/include
LDFLAGS+=	-L../compface -L${LOCALBASE}/lib
CONFIGURE_ARGS=	--enable-imap --enable-pop \
		--enable-name-unknown --with-spooldir=/var/mail \
		--with-facedir=${DATADIR}
.endif

.if ! ${PORT_OPTIONS:MNLS}
CONFIGURE_ARGS+=--disable-nls
.endif

.ifdef WITH_NAS
 CONFIGURE_ARGS+=	--enable-audio --with-audio-cmd=${LOCALBASE}/bin/auplay
 RUN_DEPENDS=	auplay:${PORTSDIR}/audio/nas
.elifdef WITH_SOX
 CONFIGURE_ARGS+=	--enable-audio --with-audio-cmd=${LOCALBASE}/bin/play
 RUN_DEPENDS=	play:${PORTSDIR}/audio/sox
.elifdef WITH_RPLAY
 CONFIGURE_ARGS+=	--enable-audio --with-audio-cmd=${LOCALBASE}/bin/rplay
 RUN_DEPENDS=	rplay:${PORTSDIR}/audio/rplay
.endif

# I have no better idea up to now
# Install the working Makefile for compface from the old faces port
# This was much less complex an builds the shared libs, too
post-patch:
	@${REINPLACE_CMD} -e "s%/usr/local/faces%${DATADIR}%g ; \
		 s%/var/spool/mail%/var/mail%g" ${WRKSRC}/faces/faces.man
	@${LN} -sf ${WRKSRC}/faces/faces.man ${WRKSRC}/faces/faces.1
.ifdef WITH_NAS
	@${REINPLACE_CMD} -e "s%rplay%auplay%" ${WRKSRC}/faces/Faces.ad
.elifdef WITH_SOX
	@${REINPLACE_CMD} -e "s%rplay%play%" ${WRKSRC}/faces/Faces.ad
.elifdef WITH_RPLAY
	# nada
.else
	@${REINPLACE_CMD} -e "s%^faces.audioSupport.*%faces.audioSupport:		false%" ${WRKSRC}/faces/Faces.ad
.endif

do-build:
	cd ${WRKSRC}/compface && ${SETENV} ${MAKE_ENV} ${MAKE} ${MAKE_FLAGS} \
		${FILESDIR}/Makefile.compface ${MAKE_ARGS} ${ALL_TARGET}
.if ${PORT_OPTIONS:MX11}
	cd ${WRKSRC}/faces && ${SETENV} ${MAKE_ENV} ${MAKE} ${MAKE_FLAGS} \
		${MAKEFILE} ${MAKE_ARGS} ${ALL_TARGET}
.endif

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/compface/compface ${STAGEDIR}${PREFIX}/bin
	${INSTALL_PROGRAM} ${WRKSRC}/compface/uncompface ${STAGEDIR}${PREFIX}/bin
	${INSTALL_DATA} ${WRKSRC}/compface/compface.h ${STAGEDIR}${PREFIX}/include
	${INSTALL_DATA} ${WRKSRC}/compface/libcompface.a ${STAGEDIR}${PREFIX}/lib
	${INSTALL_DATA} ${WRKSRC}/compface/libcompface.so.1 ${STAGEDIR}${PREFIX}/lib
	${LN} -sf libcompface.so.1 ${STAGEDIR}${PREFIX}/lib/libcompface.so
	${INSTALL_MAN} ${WRKSRC}/compface/compface.1 ${STAGEDIR}${MANPREFIX}/man/man1
	${INSTALL_MAN} ${WRKSRC}/compface/compface.3 ${STAGEDIR}${MANPREFIX}/man/man3
	${INSTALL_SCRIPT} ${FILESDIR}/ikon2xbm ${STAGEDIR}${PREFIX}/bin
	${INSTALL_SCRIPT} ${FILESDIR}/xbm2ikon ${STAGEDIR}${PREFIX}/bin
	${INSTALL_SCRIPT} ${FILESDIR}/xbmcut48 ${STAGEDIR}${PREFIX}/bin
	${INSTALL_SCRIPT} ${FILESDIR}/xbmsize48 ${STAGEDIR}${PREFIX}/bin
.if ${PORT_OPTIONS:MX11}
	${INSTALL_PROGRAM} ${WRKSRC}/faces/faces ${STAGEDIR}${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/faces/faces.1 ${STAGEDIR}${MANPREFIX}/man/man1
	${INSTALL_DATA} ${WRKSRC}/faces/Faces.ad ${STAGEDIR}${LOCALBASE}/lib/X11/app-defaults/Faces
.endif
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/README ${STAGEDIR}${DOCSDIR}

.include <bsd.port.post.mk>
