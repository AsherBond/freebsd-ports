# Created by: Jose Alonso Cardenas Marquez <acm@FreeBSD.org>
# $FreeBSD$

PORTNAME=	loemu
PORTVERSION=	0.3.1
PORTREVISION=	9
CATEGORIES=	emulators python
MASTER_SITES=	http://loemu.pegueroles.com/dists/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Simple frontend for various game emulators

RUN_DEPENDS=	${PYTHON_SITELIBDIR}/gtk-2.0/gtk/__init__.py:${PORTSDIR}/x11-toolkits/py-gtk2 \
		${PYTHON_SITELIBDIR}/libxml2.py:${PORTSDIR}/textproc/py-libxml2 \
		${PYTHON_SITELIBDIR}/libxslt.py:${PORTSDIR}/textproc/py-libxslt

USES=		gettext
USE_PYTHON=	yes
USE_PYDISTUTILS=	yes
NO_BUILD=	yes

OPTIONS_DEFINE=	MAME SNES9X ZSNES
OPTIONS_DEFAULT=	MAME SNES9X
MAME_DESC=	Install mame emulator
SNES9X_DESC=	Install snes9x emulator
ZSNES_DESC=	Install zsnes emulator
MAME_RUN_DEPENDS=	mame:${PORTSDIR}/emulators/mame
SNES9X_RUN_DEPENDS=	snes9x:${PORTSDIR}/emulators/snes9x
ZSNES_RUN_DEPENDS=	zsnes:${PORTSDIR}/emulators/zsnes

post-patch:
.for DIRE in config loemu scripts
	@cd ${WRKSRC}/${DIRE} && \
		${FIND} * -type f -exec ${REINPLACE_CMD} -i '' -e \
			's|/share/games/|/share/|g' -e \
			's|/usr/bin/python|${PYTHON_CMD}|g' "{}" \;
.endfor
	@${REINPLACE_CMD} -e 's|%%PYTHON_CMD%%|${PYTHON_CMD}|g' \
		${WRKSRC}/setup.py

.include <bsd.port.mk>
