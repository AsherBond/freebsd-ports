# Created by: Hokan <hokan@me.umn.edu>
# $FreeBSD$

PORTNAME=	news
PORTVERSION=	1.2
CATEGORIES=	sysutils
MASTER_SITES=	http://www.menet.umn.edu/~hokan/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Print news items

NO_STAGE=	yes
.include <bsd.port.pre.mk>

ALL_TARGET=	news
NEWSHOME=	${PREFIX}/news

MAN1=	news.1
MANCOMPRESSED=	no
PLIST_FILES=	bin/news

post-patch:
	${REINPLACE_CMD} -e 's|CC \= gcc|MAKE_DEPEND = $${CC}|' ${WRKSRC}/${MAKEFILE}
	${REINPLACE_CMD} -e 's|\/var\/news|${NEWSHOME}|' ${WRKSRC}/${MAKEFILE}

do-install:
	${MKDIR} ${NEWSHOME}
	${INSTALL_PROGRAM} ${WRKSRC}/news ${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/news.1 ${MAN1PREFIX}/man/man1
	@${MV} ${WRKSRC}/sample.news.item ${WRKSRC}/news.item.sample
	@if [ ! -e "${NEWSHOME}/news.item" ]; then \
		${ECHO_MSG} "	Installing local news file: ${NEWSHOME}/news.item"; \
		${INSTALL_DATA} ${WRKSRC}/news.item.sample ${NEWSHOME}/news.item ;\
	else \
		${ECHO_MSG} "	Preserving local news file: ${NEWSHOME}/news.item"; \
	fi;
	${MKDIR} ${EXAMPLESDIR} && ${INSTALL_DATA} ${WRKSRC}/news.item.sample ${EXAMPLESDIR}

.include <bsd.port.post.mk>
