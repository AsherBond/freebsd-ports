# Created by: Mario Sergio Fujikawa Ferreira <lioux@FreeBSD.org>
# $FreeBSD$

PORTNAME=	os-k
PORTVERSION=	1.15
MASTER_SITES=	http://nordbryggan.se/pub/
DISTNAME=	OS-K_v115

COMMENT=	KDE OS-K iconset

BROKEN=		Unfetchable
USES=	tar:bzip2
WRKSRC=		${WRKDIR}/OS-K
PLIST_FILE_PATTERN_EXTRA=	-v "^\./(buildset|README)"

NO_STAGE=	yes
.include "${.CURDIR}/../kde-icons-noia/Makefile.icons"
