# Created by: Maxim Sobolev <sobomax@FreeBSD.org>
# $FreeBSD$

PORTNAME=	lib3ds
PORTVERSION=	1.3.0
PORTREVISION=	3
CATEGORIES=	graphics
MASTER_SITES=	GOOGLE_CODE

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Library for handling 3DS (3D Studio) files

LICENSE=	LGPL21 # (or later)

USES=		zip
USE_GL=		glut
GNU_CONFIGURE=	yes
USE_LDCONFIG=	yes

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

.include <bsd.port.mk>
