# $FreeBSD$

PORTNAME=	fusefs-kmod
PORTVERSION=	0.263233
CATEGORIES=	sysutils kld

MAINTAINER=	dpejesh@yahoo.com
COMMENT=	FUSE kernel module

MASTER_SITES=	https://googledrive.com/host/0B0OQnKtejJEMQlpoTy11SG1nN2s/

ONLY_FOR_ARCHS=	amd64 i386

WRKSRC=		${WRKDIR}

USE_RC_SUBR=	fusefs
USES=		kmod uidfix

BUILD_DEPENDS=	fusefs-libs>2.4.1:${PORTSDIR}/sysutils/fusefs-libs

MAKE_ENV=	BINDIR="${PREFIX}/sbin" \
		MANDIR="${MANPREFIX}/man/man"

SUB_LIST+=	KMODDIR=${KMODDIR}
SUB_FILES=	pkg-message

.include <bsd.port.pre.mk>

.if ${OSVERSION} >= 800000 && ${OSVERSION} < 900000
EXTRA_PATCHES+=	${FILESDIR}/extra-patch-8-fuse_vfsops.c
EXTRA_PATCHES+=	${FILESDIR}/extra-patch-8-fuse_vnops.c
.endif
.if ${OSVERSION} >= 900000 && ${OSVERSION} < 1000000
EXTRA_PATCHES+=	${FILESDIR}/extra-patch-9-fuse_vfsops.c
EXTRA_PATCHES+=	${FILESDIR}/extra-patch-9-fuse_vnops.c
.endif
.if ${OSVERSION} >= 1000000
IGNORE=		integrated into base
.endif

do-build:
	cd ${WRKDIR}/modules/fuse; ${MAKE}
	cd ${WRKDIR}/mount_fusefs; ${MAKE}

do-install:
	${INSTALL_KLD} ${WRKSRC}/modules/fuse/fuse.ko ${STAGEDIR}${KMODDIR}
	${INSTALL_MAN} ${WRKSRC}/mount_fusefs/mount_fusefs.8 ${STAGEDIR}${PREFIX}/man/man8
	${INSTALL_PROGRAM} ${WRKSRC}/mount_fusefs/mount_fusefs ${STAGEDIR}${PREFIX}/sbin

post-install:
	${CAT} ${PKGMESSAGE}

SVN_REV=	263233
SVN_MIRROR?=	http://svn.freebsd.org/base
EXPDIR=		${WRKSRC}/src
maintainer-tar:
	${MKDIR} ${EXPDIR}
	cd ${EXPDIR} && svn export -r ${SVN_REV} ${SVN_MIRROR}/head/sys/fs/fuse/ fs/fuse
	cd ${EXPDIR} && svn export -r ${SVN_REV} ${SVN_MIRROR}/head/sys/modules/fuse/ modules/fuse
	cd ${EXPDIR} && svn export -r ${SVN_REV} ${SVN_MIRROR}/head/sbin/mount_fusefs mount_fusefs
	cd ${EXPDIR} && svn export -r ${SVN_REV} ${SVN_MIRROR}/head/sbin/mount/getmntopts.c mount_fusefs/getmntopts.c
	cd ${EXPDIR} && svn export -r ${SVN_REV} ${SVN_MIRROR}/head/sbin/mount/mntopts.h mount_fusefs/
	cd ${EXPDIR} && ${TAR} --uname root --uid 0 --gname wheel --gid 0 -zcvf ${DISTDIR}/${PORTNAME}-0.${SVN_REV}${EXTRACT_SUFX} fs modules mount_fusefs

maintainer-check:
	@new=`svn log -ql 1 ${SVN_MIRROR}@HEAD head/sys/fs/fuse | ${GREP} -v ^- | ${SED} -e 's| .*||; s|r||'`;\
	old="${SVN_REV}";\
	if [ "$${new}" -gt "$${old}" ]; then ${ECHO_MSG} "New fuse rev: r$${new} (was $${old})"; fi

.include <bsd.port.post.mk>
