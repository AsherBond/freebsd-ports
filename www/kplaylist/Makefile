# Created by: Kevin Lo <kevlo@FreeBSD.org>
# $FreeBSD$

PORTNAME=	kplaylist
PORTVERSION=	1.8.505
PORTREVISION?=	1
CATEGORIES=	www multimedia
MASTER_SITES=	http://www.kplaylist.net/archive.php?file=1.8.505&tar=true/
DISTNAME=	${PORTNAME}.${PORTVERSION}

MAINTAINER=	kevlo@FreeBSD.org
COMMENT=	PHP based music database

RUN_DEPENDS=	lame:${PORTSDIR}/audio/lame \
		oggenc:${PORTSDIR}/audio/vorbis-tools \
		zip:${PORTSDIR}/archivers/zip

USE_PHP=	curl mysql session iconv

WRKSRC=		${WRKDIR}
WWWDIR?=	${PREFIX}/www/${PORTNAME}
NO_BUILD=	yes

PLIST_FILES=	%%WWWDIR%%/index.php
PLIST_DIRS=	%%WWWDIR%%

do-install:
	${MKDIR} ${STAGEDIR}${WWWDIR}
	@cd ${WRKSRC} && ${CP} kplaylist.1.8.505.php \
		${STAGEDIR}${WWWDIR}/index.php
	${CHOWN} -R ${WWWOWN}:${WWWGRP} ${STAGEDIR}${WWWDIR} 

.include <bsd.port.mk>
