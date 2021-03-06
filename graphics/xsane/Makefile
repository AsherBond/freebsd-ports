# Created by: Dominik Brettnacher <domi@nonsensss.de>
# $FreeBSD$

PORTNAME=	xsane
PORTVERSION=	0.999
PORTREVISION=	2
CATEGORIES=	graphics
MASTER_SITES=	http://www.xsane.org/download/

MAINTAINER=	koalative@gmail.com
COMMENT=	Gtk-based X11 frontend for SANE (Scanner Access Now Easy)

LICENSE=	GPLv2

LIB_DEPENDS=	libjpeg.so:${PORTSDIR}/graphics/jpeg \
		libpng15.so:${PORTSDIR}/graphics/png \
		libtiff.so:${PORTSDIR}/graphics/tiff \
		libfreetype.so:${PORTSDIR}/print/freetype2 \
		liblcms.so:${PORTSDIR}/graphics/lcms
BUILD_DEPENDS=	scanimage:${PORTSDIR}/graphics/sane-backends
RUN_DEPENDS:=	${BUILD_DEPENDS}

USES=		gmake pkgconfig
USE_GNOME=	gtk20 gdkpixbuf2
GNU_CONFIGURE=	yes

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

PORTDOCS=	*.html *.jpg

OPTIONS_DEFINE=	DOCS GIMP NLS
GIMP_DESC=	GIMP plugin support
OPTIONS_DEFAULT=	GIMP

OPTIONS_SUB=	yes

GIMP_RUN_DEPENDS=	${LOCALBASE}/bin/gimp:${PORTSDIR}/graphics/gimp-app
GIMP_CONFIGURE_ENABLE=	gimp2 gimp
NLS_CONFIGURE_ENABLE=	nls
NLS_USES=		gettext
NLS_LIBS=		-L${LOCALBASE}/lib -lintl

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MGIMP}
SUB_FILES+=	pkg-message
.endif

post-patch:
	@${REINPLACE_CMD} -e 's| $$(DESTDIR)$$(sbindir)||' \
		-e 's|$$(DESTDIR)$$(xsanedocdir)||' ${WRKSRC}/src/Makefile.in
	@${REINPLACE_CMD} -e 's|@POSUB@ doc|@POSUB@|' ${WRKSRC}/Makefile.in

post-install:
	${INSTALL_MAN} ${WRKSRC}/doc/${PORTNAME}.man ${STAGEDIR}${MAN1PREFIX}/man/man1/${PORTNAME}.1
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/doc/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
