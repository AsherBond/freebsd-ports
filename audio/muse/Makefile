# Created by: ijliao
# $FreeBSD$

PORTNAME=	MuSE
PORTVERSION=	0.9.2
PORTREVISION=	14
CATEGORIES=	audio
MASTER_SITES=	http://files.dyne.org/.xsend.php?file=muse/releases/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Multiple Streaming Engine

LICENSE=	GPLv2

LIB_DEPENDS=	libvorbis.so:${PORTSDIR}/audio/libvorbis \
		libogg.so:${PORTSDIR}/audio/libogg

OPTIONS_DEFINE=	X11 LAME SNDFILE DOCS
OPTIONS_DEFAULT=X11

USES=		gettext gmake
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--disable-debug --disable-lubrify --disable-rpath

CPPFLAGS+=	-I${LOCALBASE}/include -DHAVE_SYS_UIO_H ${PTHREAD_CFLAGS}
LDFLAGS+=	-L${LOCALBASE}/lib -lintl ${PTHREAD_LIBS}

PORTDOCS=	AUTHORS ChangeLog NEWS KNOWN-BUGS README TODO USAGE
PLIST_FILES=	bin/muse man/man1/muse.1.gz
.for lang in es it
PLIST_FILES+=	share/locale/${lang}/LC_MESSAGES/muse.mo
.endfor

X11_USE=		GNOME=gtk20
X11_CONFIGURE_OFF=	--without-x --with-rubik

LAME_LIB_DEPENDS=	libmp3lame.so:${PORTSDIR}/audio/lame
LAME_CONFIGURE_ENV=	ac_cv_header_lame_lame_h=no

SNDFILE_LIB_DEPENDS=	libsndfile.so:${PORTSDIR}/audio/libsndfile

.include <bsd.port.options.mk>

post-patch:
	@${REINPLACE_CMD} -e 's|machine/soundcard.h|sys/soundcard.h|' \
		${WRKSRC}/src/portaudio/pa_unix_oss.c
.if empty(PORT_OPTIONS:MSNDFILE)
	@${REINPLACE_CMD} -e '/sndfile >=/s|$$PKG_CONFIG|${FALSE}|' \
		${WRKSRC}/configure
.endif

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S,^,${WRKSRC}/,} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
