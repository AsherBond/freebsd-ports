# Created by: Robert Noland <rnoland@FreeBSD.org>
# $FreeBSD$

PORTNAME=	simple-ccsm
PORTVERSION=	0.8.8
CATEGORIES=	x11-wm
MASTER_SITES=	http://releases.compiz.org/${PORTVERSION}/

MAINTAINER=	freebsd-ports@dan.me.uk
COMMENT=	Python/GTK based settings manager for CompizConfig

RUN_DEPENDS=	${LOCALBASE}/libdata/pkgconfig/compizconfig-python.pc:${PORTSDIR}/x11-wm/compizconfig-python

USES=		gettext gmake pkgconfig tar:bzip2
USE_GNOME=	pygtk2
USE_PYTHON=	2

INSTALLS_EGGINFO=	yes

INSTALLS_ICONS=	yes

do-install:
	@(cd ${WRKSRC}; ${PYTHON_CMD} setup.py install --root=${STAGEDIR} --prefix=${PREFIX})

.include <bsd.port.mk>
