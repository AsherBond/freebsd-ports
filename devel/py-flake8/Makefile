# Created by: William Grzybowski <william88@gmail.com>
# $FreeBSD$

PORTNAME=	flake8
PORTVERSION=	2.2.2
CATEGORIES=	devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	wg@FreeBSD.org
COMMENT=	Code checking using pep8 and pyflakes

LICENSE=	MIT

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}mccabe>=0.2.1:${PORTSDIR}/devel/py-mccabe \
		${PYTHON_PKGNAMEPREFIX}pep8>=1.5.7:${PORTSDIR}/devel/pep8 \
		${PYTHON_PKGNAMEPREFIX}pyflakes>=0.8.1:${PORTSDIR}/devel/py-pyflakes

USE_PYTHON=		yes
USE_PYDISTUTILS=	yes
PYDISTUTILS_AUTOPLIST=	yes

.include <bsd.port.mk>
