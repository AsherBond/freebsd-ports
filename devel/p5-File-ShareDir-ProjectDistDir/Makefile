# $FreeBSD$

PORTNAME=	File-ShareDir-ProjectDistDir
PORTVERSION=	0.5.2
PORTREVISION=	1
CATEGORIES=	devel perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	kuriyama@FreeBSD.org
COMMENT=	Perl extension for set-and-forget using a directory in projects root

LICENSE=	ART10 GPLv1
LICENSE_COMB=	dual

RUN_DEPENDS=	p5-File-ShareDir>0:${PORTSDIR}/devel/p5-File-ShareDir \
		p5-Path-Class>0:${PORTSDIR}/devel/p5-Path-Class \
		p5-Path-FindDev>0:${PORTSDIR}/devel/p5-Path-FindDev \
		p5-Path-IsDev>0:${PORTSDIR}/devel/p5-Path-IsDev \
		p5-Path-Tiny>0:${PORTSDIR}/devel/p5-Path-Tiny \
		p5-Sub-Exporter>0:${PORTSDIR}/devel/p5-Sub-Exporter
BUILD_DEPENDS:=	${RUN_DEPENDS}

USES=	perl5
USE_PERL5=	modbuild

.include <bsd.port.pre.mk>

.if ${PERL_LEVEL} < 501400
TEST_DEPENDS+=	p5-Test-Simple>=0.98:${PORTSDIR}/devel/p5-Test-Simple
.endif

.include <bsd.port.post.mk>
