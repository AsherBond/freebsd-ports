# Created by: erik@smluc.org
# $FreeBSD$

PORTNAME=	qscheme
PORTVERSION=	0.5.1
PORTREVISION=	6
CATEGORIES=	lang scheme
MASTER_SITES=	http://www.sof.ch/dan/qscheme/files/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Small and fast Scheme interpreter

BUILD_DEPENDS=	${LOCALBASE}/lib/libavcall.a:${PORTSDIR}/devel/ffcall\
		${LOCALBASE}/lib/libpcre.a:${PORTSDIR}/devel/pcre \
		${LOCALBASE}/lib/libgmp.a:${PORTSDIR}/math/gmp
LIB_DEPENDS=	libgetline.so:${PORTSDIR}/devel/libgetline

USES=		gmake perl5
USE_PERL5=	build
GNU_CONFIGURE=	yes
PLIST_SUB+=	PORTVERSION="${PORTVERSION}"

CONFIGURE_ARGS=	--with-pcre-dir=${LOCALBASE}/lib \
		--with-pcre-inc=${LOCALBASE}/include \
		--with-avcall-dir=${LOCALBASE}/lib \
		--with-avcall-inc=${LOCALBASE}/include \
		--with-gmp-dir=${LOCALBASE}/lib \
		--with-gmp-inc=${LOCALBASE}/include

NO_STAGE=	yes
post-patch:
	${REINPLACE_CMD} \
		-e "s,^LIBS = @LIBS@,& ${PTHREAD_LIBS} -L${LOCALBASE}/lib -lgetline," \
		-e "s,^CFLAGS = @CFLAGS@,& ${PTHREAD_CFLAGS}," \
		${WRKSRC}/Makefile.in
	${REINPLACE_CMD} \
		-e "s,-lpthread,${PTHREAD_LIBS},g" ${WRKSRC}/configure

.include <bsd.port.pre.mk>

.if ${ARCH} == "ia64" || ${ARCH} == "amd64" || ${ARCH} == "sparc64"
# because it uses static pcre lib, which is compiled without -fPIC. pcre problem likely.
BROKEN=		Does not build on amd64, ia64, or sparc64
.endif

.include <bsd.port.post.mk>
