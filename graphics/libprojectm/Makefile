# $FreeBSD$

PORTNAME=	libprojectM
PORTVERSION=	2.0.1
PORTREVISION=	2
CATEGORIES=	graphics audio
MASTER_SITES=	SF/${PORTNAME:tl:S/lib//}/${PORTVERSION}/
DISTNAME=	${PORTNAME:S/lib//}-${DISTVERSION}-Source

MAINTAINER=	crees@FreeBSD.org
COMMENT=	Awesome music visualiser

LICENSE=	LGPL21

LIB_DEPENDS=	libftgl.so:${PORTSDIR}/graphics/ftgl \
		libGLEW.so:${PORTSDIR}/graphics/glew \
		libfreetype.so:${PORTSDIR}/print/freetype2

USES=		cmake
CFLAGS+=	-I${LOCALBASE}/include -L${LOCALBASE}/lib
USE_LDCONFIG=	yes

post-patch:
# Install config.inp.sample instead of overwriting user's file.
# Needs to be specific enough not to rename config.inp.in too!
# Also correct pkgconfig destination dir -- fiddly
	@${REINPLACE_CMD} -e 's/config.inp\([\" ]\)/config.inp.sample\1/' \
			-e 's#\(/lib\)[^}]*}\(/pkgconfig\)#\1data\2#' \
		${WRKSRC}/CMakeLists.txt
	@${REINPLACE_CMD} -e 's#/usr/X11R6#${LOCALBASE}#' \
		${WRKSRC}/cmake/FindFreetype2.cmake
# Fix empty libdir in pkgconfig file to stop vlc complaining
	@${REINPLACE_CMD} -e 's#^\(libdir=\).*#\1${PREFIX}/lib#' \
		${WRKSRC}/${PORTNAME}.pc.in

.include <bsd.port.mk>
