# $FreeBSD$

PORTNAME=	widgets
DISTVERSION=	${QT5_VERSION}
PORTREVISION=	1
CATEGORIES=	x11-toolkits
PKGNAMEPREFIX=	qt5-

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Qt C++ widgets module

USE_QT5=	core gui qmake_build buildtools_build
QT_DIST=	base
USE_XORG=	x11
HAS_CONFIGURE=	yes
USE_LDCONFIG=	${PREFIX}/${QT_LIBDIR_REL}

BUILD_WRKSRC=	${WRKSRC}/src/${PORTNAME}
INSTALL_WRKSRC=	${BUILD_WRKSRC}

MORE_WRKSRCS=	src/plugins/accessible/${PORTNAME} \
		src/tools/uic

QT_DEFINES=	ACCESSIBILITY WIDGETS XSYNC
QT_CONFIG=	accessibility accessibility-atspi-bridge xlib

OPTIONS_DEFINE=	GTK2

GTK2_DESC=	GTK+-based Qt theme
GTK2_USE=	GNOME=gtk20
GTK2_CONFIGURE_ON=	-gtkstyle
GTK2_CONFIGURE_OFF=	-no-gtkstyle

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MGTK2}
QT_DEFINES+=	STYLE_GTK
QT_CONFIG+=	gtkstyle
.else
QT_DEFINES+=	-STYLE_GTK
QT_CONFIG+=	-gtkstyle
.endif

post-configure:
.for d in ${MORE_WRKSRCS}
	@cd ${WRKSRC}/${d} && \
		${SETENV} ${QMAKE_ENV} ${WRKSRC}/bin/qmake ${QMAKE_ARGS}
.endfor

pre-build:
	@cd ${WRKSRC}/src/tools/uic && \
		${SETENV} ${MAKE_ENV} ${MAKE} ${MAKE_FLAGS} ${MAKEFILE} \
		${_MAKE_JOBS} ${MAKE_ARGS} ${ALL_TARGET}

post-build:
	@cd ${WRKSRC}/src/plugins/accessible/${PORTNAME} && \
		${SETENV} ${MAKE_ENV} ${MAKE} ${MAKE_FLAGS} ${MAKEFILE} \
		${_MAKE_JOBS} ${MAKE_ARGS} ${ALL_TARGET}

post-install:
.for d in ${MORE_WRKSRCS}
	@cd ${WRKSRC}/${d} && \
		${SETENV} ${MAKE_ENV} ${MAKE} ${MAKE_FLAGS} ${MAKEFILE} \
		${MAKE_ARGS} ${INSTALL_TARGET}
.endfor
	${INSTALL_DATA} ${BUILD_WRKSRC}/dialogs/images/qtlogo-64.png \
		${STAGEDIR}${PREFIX}/share/pixmaps/qt5logo.png

.include <bsd.port.mk>
