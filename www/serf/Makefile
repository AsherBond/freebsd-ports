# Created by: Craig Rodrigues <rodrigc@FreeBSD.org>
# $FreeBSD$

PORTNAME=	serf
PORTVERSION=	1.3.7
CATEGORIES=	www
MASTER_SITES=	http://serf.googlecode.com/svn/src_releases/

MAINTAINER=	lev@FreeBSD.org
COMMENT=	Serf HTTP client library

LICENSE=	APACHE20

LIB_DEPENDS+=	libapr-1.so:${PORTSDIR}/devel/apr1

USES=		scons tar:bzip2
USE_OPENSSL=	yes
USE_LDCONFIG=	yes

# support for subversion-static,
SUB_FILES=	libserf-1.la

OPTIONS_DEFINE=	DOCS GSSAPI

SCONS_ARGS=	APR=${LOCALBASE}/bin/apr-1-config
SCONS_ARGS+=	APU=${LOCALBASE}/bin/apu-1-config
SCONS_ARGS+=	OPENSSL=${OPENSSLBASE}
SCONS_ARGS+=	PREFIX=${PREFIX}
SCONS_ARGS+=	CC=${CC}
SCONS_ARGS+=	CFLAGS="${CFLAGS}"
INSTALL_TARGET=	install --install-sandbox=${STAGEDIR}

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MGSSAPI}
SCONS_ARGS+=	GSSAPI="/usr"
.endif

do-build:
	@(cd ${WRKSRC} && ${SETENV} ${MAKE_CMD} ${SCONS_ARGS})

do-install:
	@(cd ${WRKSRC} && ${SENTENV} ${MAKE_CMD} ${SCONS_ARGS} ${INSTALL_TARGET})

post-patch:
	@${REINPLACE_CMD} -e '/^Requires.private/d' ${WRKSRC}/build/serf.pc.in

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/design-guide.txt ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${SUB_FILES:S|^|${WRKDIR}/|} ${STAGEDIR}${PREFIX}/lib
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/libserf-1.so

regression-test check: build
	@(cd ${WRKSRC} && ${MAKE_CMD} check)

.include <bsd.port.mk>
