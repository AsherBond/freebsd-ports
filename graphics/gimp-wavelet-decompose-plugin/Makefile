# Created by: Mario Sergio Fujikawa Ferreira <lioux@FreeBSD.org>
# $FreeBSD$

PORTNAME=	wavelet-decompose
DISTVERSION=	0.1.2
PORTREVISION=	1
CATEGORIES=	graphics
MASTER_SITES=	http://registry.gimp.org/files/
PKGNAMEPREFIX=	gimp-
PKGNAMESUFFIX=	-plugin

MAINTAINER=	lioux@FreeBSD.org
COMMENT=	Gimp plugin to losslessly decompose images into wavelet scales layers

LICENSE=	GPLv2

BUILD_DEPENDS=	${LOCALBASE}/libdata/pkgconfig/gimp-2.0.pc:${PORTSDIR}/graphics/gimp-app
RUN_DEPENDS=	${LOCALBASE}/libdata/pkgconfig/gimp-2.0.pc:${PORTSDIR}/graphics/gimp-app

OPTIONS_DEFINE=	NLS

USES=		gettext gmake

PLIST_SUB=	PLUGIN_DIR=${PLUGIN_DIR}
PLUGIN_DIR?=	libexec/gimp/2.2/plug-ins/

# l10n languages
LANGUAGES=	de ru it pl

# installed files
PLIST_FILES=	%%PLUGIN_DIR%%/wavelet-decompose

# installed dirs
PLIST_DIRSTRY=	libexec/gimp/2.2/plug-ins \
		libexec/gimp/2.2 \
		libexec/gimp

.include <bsd.port.options.mk>

post-patch:
	@${REINPLACE_CMD} \
		-e 's|gimptool-2.0|${LOCALBASE}/bin/gimptool-2.0|' \
		${WRKSRC}/src/Makefile
#
## l10n
# disable l10n if appropriate
.if ! ${PORT_OPTIONS:MNLS}
	@${REINPLACE_CMD} -E \
		-e 's|(^all:.*)po |\1|' \
		${WRKSRC}/Makefile
.endif

## l10n
#
.if ${PORT_OPTIONS:MNLS}
.for language in ${LANGUAGES}
PLIST_FILES+=	share/locale/${language}/LC_MESSAGES/gimp20-${PORTNAME}-plug-in.mo

PLIST_DIRSTRY+=	share/locale/${language}/LC_MESSAGES \
		share/locale/${language} \
		share/locale
.endfor
.endif

do-install:
# plugin
	@${MKDIR} ${STAGEDIR}${PREFIX}/${PLUGIN_DIR}
	${INSTALL_PROGRAM} ${WRKSRC}/src/wavelet-decompose ${STAGEDIR}${PREFIX}/${PLUGIN_DIR}
#
## l10n
#
.if ${PORT_OPTIONS:MNLS}
.for language in ${LANGUAGES}
	@${MKDIR} ${STAGEDIR}${PREFIX}/share/locale/${language}/LC_MESSAGES/
	${INSTALL_DATA} ${WRKSRC}/po/${language}.mo ${STAGEDIR}${PREFIX}/share/locale/${language}/LC_MESSAGES/gimp20-${PORTNAME}-plug-in.mo
.endfor
.endif

.include <bsd.port.mk>
