# $FreeBSD$

PORTNAME=	acpica
PORTVERSION=	20140724
CATEGORIES=	sysutils devel
MASTER_SITES=	https://acpica.org/sites/acpica/files/ \
		LOCAL
MASTER_SITE_SUBDIR=	jkim
PKGNAMESUFFIX=	-tools
DISTNAME=	${PORTNAME}-unix2-${PORTVERSION}

MAINTAINER=	jkim@FreeBSD.org
COMMENT=	Tools from the ACPI Component Architecture (ACPICA) project

LICENSE=	BSD3CLAUSE GPLv2
LICENSE_COMB=	dual

USES=		bison gmake
YACC=		${LOCALBASE}/bin/bison

ACPICA_TOOLS=	acpibin acpidump acpiexec acpihelp acpinames acpisrc
ACPICA_TOOLS+=	acpixtract iasl

PLIST_FILES=	${ACPICA_TOOLS:S,^,bin/,}
WRKSRC_SUBDIR=	generate/unix

MAKE_ARGS=	HOST=_FreeBSD NOOPT=TRUE PROGS="${ACPICA_TOOLS}"
MAKE_ARGS+=	CC="${CC}" LEX="${FLEX}" YACC="${YACC}"

do-install:
	@${INSTALL_PROGRAM} ${ACPICA_TOOLS:S,^,${WRKSRC}/bin/,} \
	    ${STAGEDIR}${PREFIX}/bin

.include <bsd.port.mk>
