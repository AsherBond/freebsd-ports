# Created by: Mark Pulford <mark@kyne.com.au>
# $FreeBSD$

PORTNAME=	bubblemon-dockapp
PORTVERSION=	1.46
PORTREVISION=	6
CATEGORIES=	sysutils
MASTER_SITES=	http://www.ne.jp/asahi/linux/timecop/software/ \
		LOCAL/ehaupt
DISTNAME=	${PORTNAME}-${PORTVERSION:S/0$//}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	X eye candy for displaying CPU and memory load in a dock

USES=		gmake
USE_GNOME=	gtk12
MAKE_ARGS+=	PREFIX="${PREFIX}"

PORTDOCS=	README

NO_STAGE=	yes
post-patch:
	${REINPLACE_CMD} -e "s@CC = gcc@CC = ${CC}@g; \
		s@-O3 -ansi -Wall@${CFLAGS} -Wall@g; \
		s@PREFIX = /usr/local@PREFIX = ${PREFIX}@g; \
		s@gtk-config@${GTK_CONFIG}@g; s@-lgtk@-lgtk-1.2@g; \
		s@-c -g kmem -m 2755 -o root@-s -c -g kmem -m 2755 -o root@g" \
		${WRKSRC}/Makefile
	${REINPLACE_CMD} -e 's|-lkvm||g' ${WRKSRC}/Makefile.FreeBSD

post-install:
	${MKDIR} ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/misc/wak.wav ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/misc/wakwak.sh ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/doc/Xdefaults.sample ${EXAMPLESDIR}
.if !defined(NOPORTDOCS)
	${MKDIR} ${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/README ${DOCSDIR}
.endif

.include <bsd.port.mk>
