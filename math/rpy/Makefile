# Created by: ijliao
# $FreeBSD$

PORTNAME=	rpy
PORTVERSION=	1.0.3
PORTREVISION=	32
CATEGORIES=	math
MASTER_SITES=	SF

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Python interface to the R Programming Language

LICENSE=	GPLv2 LGPL21 MPL
LICENSE_COMB=	dual

BUILD_DEPENDS=	${PYTHON_SITELIBDIR}/numpy:${PORTSDIR}/math/py-numpy \
		R:${PORTSDIR}/math/R
RUN_DEPENDS=	${PYTHON_SITELIBDIR}/numpy:${PORTSDIR}/math/py-numpy \
		R:${PORTSDIR}/math/R

USE_PYTHON=	yes
USE_PYDISTUTILS=	yes
PYDISTUTILS_AUTOPLIST=	yes
LDFLAGS+=	-L${LOCALBASE}/lib/R/modules -L${LOCALBASE}/lib/R/lib

post-patch:
	@${REINPLACE_CMD} -e 's,^statichere ,,' ${WRKSRC}/src/rpymodule.c
	@${REINPLACE_CMD} -e 's|/usr/share|${LOCALBASE}/lib|' ${WRKSRC}/setup.py

pre-configure:
	@(if [ ! -e ${LOCALBASE}/lib/R/lib/libR.so ] ; then \
	${ECHO_MSG} "==> ${PKGNAME} requires math/R to be built WITH_LIBR" ; \
	exit 1; fi)

.include <bsd.port.mk>
