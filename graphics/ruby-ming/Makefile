# Created by: Akinori MUSHA aka knu <knu@idaemons.org>
# $FreeBSD$

PORTNAME=	ming
PORTVERSION=	0.4.3.${RUBY_MING_VERSION}
PORTREVISION=	3
CATEGORIES+=	graphics ruby
MASTER_SITES=	RF
MASTER_SITE_SUBDIR=	mingruby
PKGNAMEPREFIX?=	${RUBY_PKGNAMEPREFIX}
DISTNAME=	${PORTNAME}-ruby-${RUBY_MING_VERSION}
DIST_SUBDIR=	ruby

MAINTAINER=	don@na.rim.or.jp
COMMENT=	Yet another Ming module for Ruby

LIB_DEPENDS?=	libming.so:${PORTSDIR}/graphics/ming

RUBY_MING_VERSION=	0.2.1

USE_RUBY=	yes
USE_RUBY_SETUP=	yes
CONFIGURE_ARGS=	-- --with-ming-include=${PREFIX}/include/ming --with-ming-lib=${PREFIX}/lib

WRKSRC=		${WRKDIR}/${PORTNAME}-ruby

DOCS=	ChangeLog INSTALL LGPL NEWS README TODO

DEPRECATED=	RubyForge shutdown May 15 2014
EXPIRATION_DATE=	2014-09-20

OPTIONS_DEFINE=	DOCS

post-install:
	${MKDIR} ${STAGEDIR}${RUBY_MODEXAMPLESDIR}
	(cd ${WRKSRC}/examples/ && ${COPYTREE_SHARE} \* ${STAGEDIR}${RUBY_MODEXAMPLESDIR})
	${MKDIR} ${STAGEDIR}${RUBY_MODDOCDIR}
.for f in ${DOCS}
	${INSTALL_DATA} ${WRKSRC}/${f} ${STAGEDIR}${RUBY_MODDOCDIR}/
.endfor

.include <bsd.port.pre.mk>

.if ${RUBY_VER} >= 2.0
BROKEN=		Does not build with Ruby 2.0 or newer
.endif

.include <bsd.port.post.mk>
