# Created by: thierry@pompo.net
# $FreeBSD$

PORTNAME=	mei
PORTVERSION=	1.0.4
PORTREVISION=	1
CATEGORIES=	science parallel
MASTER_SITES=	http://code-saturne.org/releases/

MAINTAINER=	thierry@FreeBSD.org
COMMENT=	Code_Saturne Mathematical Expression Interpreter

LICENSE=	LGPL21

LIB_DEPENDS=	libbft.so:${PORTSDIR}/science/bft
BUILD_DEPENDS=	swig:${PORTSDIR}/devel/swig13

USES=		libtool
USE_LDCONFIG=	yes
USE_PYTHON=	yes
GNU_CONFIGURE=	yes
CONFIGURE_ENV=	ac_cv_path_PYEXE=${PYTHON_CMD}
CONFIGURE_ARGS=	--with-bft=${LOCALBASE}
INSTALL_TARGET=	install-strip

.if defined(MAINTAINER_MODE)
regression-test:
	(cd ${WRKSRC}/tests &&	\
	${MAKE} check &&	\
	./mei_test )
.endif

.include <bsd.port.mk>
