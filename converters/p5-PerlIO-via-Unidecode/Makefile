# Created by: Dmitry Marakasov <amdmi3@FreeBSD.org>
# $FreeBSD$

PORTNAME=	PerlIO-via-Unidecode
PORTVERSION=	1.01
CATEGORIES=	converters perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	amdmi3@FreeBSD.org
COMMENT=	Perlio layer for Unidecode

BUILD_DEPENDS=	p5-Text-Unidecode>=0:${PORTSDIR}/converters/p5-Text-Unidecode
RUN_DEPENDS=	p5-Text-Unidecode>=0:${PORTSDIR}/converters/p5-Text-Unidecode

USES=		perl5
USE_PERL5=	configure

.include <bsd.port.mk>
