# Created by: Masanori OZAWA (ozawa@ongs.co.jp)
# $FreeBSD$

PORTNAME=	fusenshi
PORTVERSION=	0.9.0
PORTREVISION=	12
CATEGORIES=	deskutils
MASTER_SITES=	http://www.ongs.co.jp/projects/fusenshi/

MAINTAINER=	ozawa@ongs.co.jp
COMMENT=	Post-it(R) like application with network support

LIB_DEPENDS=	libgtkmm-2.4.so:${PORTSDIR}/x11-toolkits/gtkmm24 \
		libgtksourceview-1.0.so:${PORTSDIR}/x11-toolkits/gtksourceview

USES=		pkgconfig tar:tgz
USE_GNOME=	libxml2
MAKE_JOBS_UNSAFE=	yes

.ifdef WITHOUT_SSL
MAKE_ARGS+=	WITHOUT_SSL=yes
.else
LIB_DEPENDS+=	libgnutls.so:${PORTSDIR}/security/gnutls
.endif

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/fusenshi

.include <bsd.port.mk>
