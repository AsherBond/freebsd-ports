# Created by: jbacon
# $FreeBSD$

############################################################################
# http://www.bic.mni.mcgill.ca/software/minc/
# is the ultimate source for MINC, and will always contain the latest
# source release.  If this port is not up to date enough for you,
# you can download the latest sources and build manually.  On FreeBSD,
# you must configure with the environment variable LDFLAGS set to
# ${LOCALBASE}/lib so that the configure script will find libnetcdf.
# Of course, the netcdf port must be installed first.

PORTNAME=	minc
PORTVERSION=	1.5.1
PORTREVISION=	1
CATEGORIES=	science biology
MASTER_SITES=	http://www.nitrc.org/frs/downloadlink.php/400/

MAINTAINER=	jwbacon@tds.net
COMMENT=	Medical Imaging NetCDF

BROKEN=		Fails to build

LIB_DEPENDS=	libnetcdf.so:${PORTSDIR}/science/netcdf

USE_AUTOTOOLS=	libtool
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
CONFIGURE_ARGS=	--enable-static=yes --enable-shared=yes

CONFLICTS=	minc-2* zh-tk-[0-9]*

WRKSRC=		${WRKDIR}/${PORTNAME}-1.5

MAN1=	dcm2mnc.1 \
	ecattominc.1 \
	invert_raw_image.1 \
	minc_modify_header.1 \
	mincaverage.1 \
	minccalc.1 \
	mincconcat.1 \
	minccopy.1 \
	mincdiff.1 \
	mincedit.1 \
	mincexpand.1 \
	mincextract.1 \
	mincheader.1 \
	minchistory.1 \
	mincinfo.1 \
	minclookup.1 \
	mincmakescalar.1 \
	mincmakevector.1 \
	mincmath.1 \
	mincpik.1 \
	mincresample.1 \
	mincreshape.1 \
	mincstats.1 \
	minctoecat.1 \
	minctoraw.1 \
	mincview.1 \
	mincwindow.1 \
	mnc2nii.1 \
	nii2mnc.1 \
	rawtominc.1 \
	transformtags.1 \
	upet2mnc.1 \
	voxeltoworld.1 \
	xfmconcat.1 \
	xfminvert.1

MAN3=	ParseArgv.3

NO_STAGE=	yes
post-install:
	@${CAT} ${PKGMESSAGE}

.include <bsd.port.mk>
