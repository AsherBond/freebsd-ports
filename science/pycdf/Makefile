# Created by: wenheping@gmail.com
# $FreeBSD$

PORTNAME=	pycdf
PORTVERSION=	0.6.3
PORTREVISION=	3
CATEGORIES=	science python
MASTER_SITES=	SF/pysclint/${PORTNAME}/${PORTNAME}-${PORTVERSION}b
DISTNAME=	${PORTNAME}-0.6-3b

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Python Interface to the Unidata NetCDF Library

BUILD_DEPENDS=	${PYTHON_SITELIBDIR}/numpy:${PORTSDIR}/math/py-numpy
LIB_DEPENDS=	libnetcdf.so:${PORTSDIR}/science/netcdf
RUN_DEPENDS:=	${BUILD_DEPENDS}

LDFLAGS+=	"-L${LOCALBASE}/lib"

USE_PYTHON=	yes
USE_PYDISTUTILS=	yes
PYDISTUTILS_AUTOPLIST=	yes
WRKSRC=		${WRKDIR}/${DISTNAME}

.include <bsd.port.mk>
