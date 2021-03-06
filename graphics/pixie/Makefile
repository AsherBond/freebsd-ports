# Created by: Igor Pokrovsky <tiamat@comset.net>
# $FreeBSD$

PORTNAME=	pixie
PORTVERSION=	2.2.6
PORTREVISION=	10
CATEGORIES=	graphics
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/Pixie%20${PORTVERSION}
DISTNAME=	Pixie-src-${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Photorealistic renderer with Pixar's RenderMan-like interface

LICENSE=	LGPL21 # (or later)

LIB_DEPENDS=	libIlmImf.so:${PORTSDIR}/graphics/OpenEXR \
		libtiff.so:${PORTSDIR}/graphics/tiff \
		libfltk_gl.so:${PORTSDIR}/x11-toolkits/fltk

USE_GL=		glu
USES=		bison libtool pathfix tar:tgz
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--includedir=${PREFIX}/include/pixie \
		--libdir=${PREFIX}/lib/pixie \
		--with-docdir=${DOCSDIR} \
		--with-shaderdir=${DATADIR}/shaders \
		--with-ribdir=${DATADIR}/ribs \
		--with-texturedir=${DATADIR}/textures \
		--with-displaysdir=${PREFIX}/lib/pixie/displays \
		--with-modulesdir=${PREFIX}/lib/pixie/modules \
		--with-openexr-prefix=${LOCALBASE} \
		--enable-openexr-threads
WRKSRC=		${WRKDIR}/Pixie
INSTALL_TARGET=	install-strip
USE_LDCONFIG=	${PREFIX}/lib/${PORTNAME}

PORTDOCS=	*

CFLAGS+=	-fPIC
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

sparc64_BROKEN=	Does not compile on sparc64

OPTIONS_DEFINE=	DOCS

.include <bsd.port.pre.mk>

.if ${OSVERSION} < 1000033
BUILD_DEPENDS+=	${LOCALBASE}/bin/flex:${PORTSDIR}/textproc/flex
CONFIGURE_ENV+=	ac_cv_path_FLEX="${LOCALBASE}/bin/flex"
.endif

post-patch:
	@${REINPLACE_CMD} -e '/test/s|==|=|g ; \
		 s|-lpthread|-pthread|g' ${WRKSRC}/configure
	@${REINPLACE_CMD} -e '/^SUBDIRS/s|doc||g ; \
		 /^install-data-am:/s|install-nobase_docDATA||g' \
		 ${WRKSRC}/Makefile.in
	@${REINPLACE_CMD} -e '/^includedir/s|=.*$$|= @includedir@|g' \
		${WRKSRC}/src/ri/Makefile.in \
		${WRKSRC}/src/sdr/Makefile.in

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	(cd ${WRKSRC} && ${INSTALL_DATA} AUTHORS ChangeLog DEVNOTES NEWS \
		README ${STAGEDIR}${DOCSDIR})
	(cd ${WRKSRC}/doc && ${COPYTREE_SHARE} . ${STAGEDIR}${DOCSDIR} \
		'! -name "*Makefile*"')

.include <bsd.port.post.mk>
