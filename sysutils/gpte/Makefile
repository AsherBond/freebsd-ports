# Created by: Valentin Nechayev <netch@segfault.kiev.ua>
# $FreeBSD$

PORTNAME=	gpte
PORTVERSION=	1.0
CATEGORIES=	sysutils
MASTER_SITES=	ftp://segfault.kiev.ua/pub/

MAINTAINER=	netch@segfault.kiev.ua
COMMENT=	Simple command-line GPT partition editor

PLIST_FILES=	bin/gpte \
		man/man8/gpte.8.gz

post-extract:
	cd ${WRKSRC} && ${CP} Makefile.bsd Makefile

.include <bsd.port.mk>
