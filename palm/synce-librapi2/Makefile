# Created by: Sam Lawrance <boris@brooknet.com.au>
# $FreeBSD$

PORTNAME=	librapi2
PORTVERSION=	0.14
CATEGORIES?=	palm
MASTER_SITES=	SF/synce/SynCE/${PORTVERSION}
PKGNAMEPREFIX?=	synce-

MAINTAINER=	ports@FreeBSD.org
COMMENT?=	Utilities/libraries to make RAPI calls on WinCE devices

LIB_DEPENDS+=	libsynce.so:${PORTSDIR}/palm/synce-libsynce

CONFLICTS=	popular-[0-9]*

GNU_CONFIGURE=	yes
USE_AUTOTOOLS=	libtool
USES=		pathfix iconv pkgconfig
USE_LDCONFIG=	yes
CONFIGURE_ARGS=	${ICONV_CONFIGURE_BASE} --with-libsynce="${LOCALBASE}"

NO_STAGE=	yes
.include <bsd.port.pre.mk>

.if defined(RAPI_SLAVE) && ${RAPI_SLAVE} == "pythonb"
CONFIGURE_ARGS+=	--enable-python-bindings
.else
CONFIGURE_ARGS+=	--disable-python-bindings

MAN1=		pcp.1 pkillall.1 pls.1 pmkdir.1 \
		pmv.1 prm.1 prmdir.1 prun.1 \
		psettime.1 pshortcut.1 pstatus.1 \
		rapiconfig.1 synce-install-cab.1 \
		synce-list-programs.1 synce-registry.1 \
		synce-remove-program.1
MAN3=		rapi_connection_from_name.3

post-patch:
.for f in synce-install-cab.in synce-remove-program.in
	@${REINPLACE_CMD} -e 's|bin/bash|bin/sh|' ${WRKSRC}/script/${f}
.endfor

.endif

.include <bsd.port.post.mk>
