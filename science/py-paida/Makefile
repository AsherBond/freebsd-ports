# Created by: Vsevolod Stakhov <vsevolod@highsecure.ru>
# $FreeBSD$

PORTNAME=	paida
PORTVERSION=	3.2.1.2.10
PORTREVISION=	1
CATEGORIES=	science python
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/${PORTNAME}-3.2.1_2.10.1
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
DISTNAME=	${PORTNAME}-3.2.1_2.10.1

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}tkinter>0:${PORTSDIR}/x11-toolkits/py-tkinter

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Pure Python scientific analysis package

USE_PYTHON=	yes
USE_PYDISTUTILS=	yes
PYDISTUTILS_AUTOPLIST=	yes

.include <bsd.port.mk>
