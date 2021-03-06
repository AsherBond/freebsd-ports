# Created by: Piet Delport
# $FreeBSD$

PORTNAME=	mosref
PORTVERSION=	2.0.b3
CATEGORIES=	security lang scheme
MASTER_SITES=		SF/${PORTNAME}/${PORTNAME}/2.0-beta3
DISTNAME=		${PORTNAME}-2.0-beta3

MAINTAINER= ports@FreeBSD.org
COMMENT=	Secure remote execution framework using a compact Scheme-influenced VM

USES=		gmake

PORTDOCS=	ChangeLog TODO vm-implementation.tex vm-implementation.pdf

NO_STAGE=	yes
.include <bsd.port.pre.mk>

.if ${ARCH} == "amd64" && ${OSVERSION} >= 700000
BROKEN=		segmentation fault during build
.endif

# The distfile has execute bits set on everything; fix.
post-extract:
	${FIND} ${WRKSRC} -type f -exec ${CHMOD} a-x {} ";"

post-patch:
	${REINPLACE_CMD} -e 's|%%PREFIX%%|${PREFIX}|' ${WRKSRC}/bin/install.ms

post-install:
	@${MKDIR} ${DATADIR}
	${INSTALL_DATA} ${WRKSRC}/share/vimrc ${DATADIR}
.if !defined(NOPORTDOCS)
	@${MKDIR} ${DOCSDIR}
	cd ${WRKSRC} && ${INSTALL_DATA} ChangeLog TODO ${DOCSDIR}
	cd ${WRKSRC}/doc && ${INSTALL_DATA} vm-implementation.tex vm-implementation.pdf ${DOCSDIR}
.endif

.include <bsd.port.post.mk>
