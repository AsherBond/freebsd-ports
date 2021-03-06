# Created by: torstenb@FreeBSD.org
# $FreeBSD$

PORTNAME=	mc
PORTVERSION=	4.8.12
PORTREVISION=	2
CATEGORIES=	misc shells
MASTER_SITES=	http://ftp.midnight-commander.org/ \
		http://ftp.osuosl.org/pub/midnightcommander/ \
		SF/nemysisfreebsdp/misc/:icons
DISTFILES=	${PORTNAME}-${DISTVERSION}${EXTRACT_SUFX} \
		${PORTNAME}.png:icons
EXTRACT_ONLY=	${PORTNAME}-${DISTVERSION}${EXTRACT_SUFX}

MAINTAINER=	nemysis@FreeBSD.org
COMMENT=	Midnight Commander, a free Norton Commander Clone

LICENSE=	GPLv3

LIB_DEPENDS=	libssh2.so:${PORTSDIR}/security/libssh2

CONFLICTS=	mc-light-4*

USES=		gmake shebangfix perl5 pkgconfig tar:xz libtool
SHEBANG_FILES=	misc/mcedit.menu configure configure.ac \
		${WRKSRC}/src/vfs/extfs/helpers/s3+.in \
		${WRKSRC}/src/vfs/extfs/helpers/uc1541.in
python_OLD_CMD=	@PYTHON@
USE_GNOME=	glib20
GNU_CONFIGURE=	yes
CONFIGURE_ENV=	ZIP=${UNZIP_CMD} UNZIP=${UNZIP_CMD}

OPTIONS_DEFINE=	DOCS EDITOR ICONV NLS SMB SUBSHELL X11

OPTIONS_SINGLE=	SCREEN
OPTIONS_SINGLE_SCREEN=	SLANG NCURSES

OPTIONS_DEFAULT=	EDITOR ICONV SLANG SMB SUBSHELL X11

EDITOR_DESC=	Build with internal editor
SUBSHELL_DESC=	Build with subshell support

OPTIONS_SUB=	yes

EDITOR_CONFIGURE_WITH=	internal-edit

ICONV_USES=		iconv
ICONV_CONFIGURE_ENABLE=	charset

NLS_CONFIGURE_ENABLE=	nls
NLS_USES=		gettext

SLANG_LIB_DEPENDS=	libslang.so:${PORTSDIR}/devel/libslang2

SMB_CONFIGURE_ENABLE=	vfs-smb
SMB_CONFIGURE_ON=	--with-smb-configdir=${LOCALBASE}/etc \
			--with-smb-codepagedir=${LOCALBASE}/etc/codepages

SUBSHELL_CONFIGURE_WITH=	subshell

X11_CONFIGURE_ENABLE=	x

SUB_FILES=	pkg-message

PORTDOCS=	*

DOCSRCDIR1=	${WRKSRC}
DOC_FILES1=	AUTHORS NEWS README

DOCSRCDIR2=	${WRKSRC}/doc
DOCSDIR2=	${DOCSDIR}/doc
DOC_FILES2=	FAQ HACKING MAINTAINERS *.txt

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MNLS}
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
.endif

.if${PORT_OPTIONS:MX11}
USE_XORG=	x11 xext
.endif

.if ${PORT_OPTIONS:MSLANG}
CONFIGURE_ARGS+=--with-screen=slang --with-slang-includes=${LOCALBASE}/include
.endif

.if ${PORT_OPTIONS:MNCURSES}
CONFIGURE_ARGS+=--with-screen=ncurses
.endif

post-patch:
	${REINPLACE_CMD} -e 's|missing-parameter-type|unused-variable|; \
		s|but-set-variable|variable|' \
		${WRKSRC}/configure
	@${REINPLACE_CMD} -e 's|SUBDIRS = intl|SUBDIRS =|' ${WRKSRC}/Makefile.in

post-install:
	${INSTALL_DATA} ${_DISTDIR}/${PORTNAME}.png \
		${STAGEDIR}${PREFIX}/share/pixmaps/
	${INSTALL_DATA} ${FILESDIR}/${PORTNAME}.desktop ${STAGEDIR}${DESKTOPDIR}

	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${DOC_FILES1:S|^|${DOCSRCDIR1}/|} ${STAGEDIR}${DOCSDIR}
	@${MKDIR} ${STAGEDIR}${DOCSDIR2}
	${INSTALL_DATA} ${DOC_FILES2:S|^|${DOCSRCDIR2}/|} ${STAGEDIR}${DOCSDIR2}

.include <bsd.port.mk>
