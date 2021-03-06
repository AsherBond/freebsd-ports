# Created by: Jason Helfman <jgh@FreeBSD.org>
# $FreeBSD$

PORTNAME=	libvirt
PORTVERSION=	1.2.6
PORTREVISION=	2
CATEGORIES=	devel
MASTER_SITES=	http://libvirt.org/sources/ \
		ftp://libvirt.org/libvirt/

MAINTAINER=	jgh@FreeBSD.org
COMMENT=	Toolkit to interact with virtualization capabilities

LICENSE=	LGPL3

LIB_DEPENDS=	libcurl.so:${PORTSDIR}/ftp/curl \
		libgcrypt.so:${PORTSDIR}/security/libgcrypt \
		libxml2.so:${PORTSDIR}/textproc/libxml2 \
		libgnutls.so:${PORTSDIR}/security/gnutls \
		libssh2.so:${PORTSDIR}/security/libssh2
BUILD_DEPENDS=	dnsmasq:${PORTSDIR}/dns/dnsmasq
RUN_DEPENDS=	dnsmasq:${PORTSDIR}/dns/dnsmasq

OPTIONS_DEFINE=	DOCS NLS QEMU
OPTIONS_DEFINE_amd64=	BHYVE
QEMU_DESC=	QEMU driver
BHYVE_DESC=	bhyve driver

OPTIONS_SUB=	yes

QEMU_CONFIGURE_WITH=	qemu yajl
QEMU_CFLAGS=	-I${LOCALBASE}/include
QEMU_LIB_DEPENDS=	libyajl.so:${PORTSDIR}/devel/yajl
QEMU_RUN_DEPENDS=	dmidecode:${PORTSDIR}/sysutils/dmidecode \
			qemu-io:${PORTSDIR}/emulators/qemu-devel

BHYVE_CONFIGURE_WITH=	bhyve

NLS_USES=	gettext
NLS_CONFIGURE_ENABLE=	nls
NLS_CONFIGURE_ON=	--with-libintl-prefix=${LOCALBASE}

USE_RC_SUBR=	libvirtd

GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--without-sasl \
		--without-avahi \
		--without-polkit \
		--without-hal \
		--without-udev \
		--without-netcf \
		--without-sysctl \
		--without-lxc \
		--without-uml \
		--with-ssh2

# workaround to override pkg-config calls
# random_data fix can be removed when 8.x is eol
CONFIGURE_ENV=	SSH2_LIBS="-L${LOCALBASE}/lib -lssh2 -lssl" \
		SSH2_CFLAGS="-I${LOCALBASE}/include" \
		ac_cv_type_struct_random_data=""

# limit production release x.x.x
PORTSCOUT=	limit:\d+\.\d+\.\d+$$

LDFLAGS+=	-L${LOCALBASE}/lib -fstack-protector

USES=		charsetfix pathfix gmake pkgconfig perl5
USE_PERL5=	build
USE_LDCONFIG=	yes
SHLIB_VER=	1002
PLIST_SUB=	PORTVERSION="-${PORTVERSION}" \
		SHLIB_VER=${SHLIB_VER}
PORTDOCS=	*
STRIP_FILES=	libvirt.so.${SHLIB_VER} \
		libvirt-qemu.so.${SHLIB_VER} \
		libvirt-lxc.so.${SHLIB_VER} \
		libvirt/lock-driver/lockd.so \
		libvirt/connection-driver/libvirt_driver_vbox.so \
		libvirt/connection-driver/libvirt_driver_secret.so \
		libvirt/connection-driver/libvirt_driver_storage.so

.include <bsd.port.options.mk>

.if ${OSVERSION} >= 1000000
OPTIONS_DEFAULT_amd64=	BHYVE
.endif

#work around an options bug (thanks mat@)
.if ${ARCH} != amd64
PLIST_SUB+=	BHYVE="@comment "
.endif

post-patch:
.if ${OSVERSION} < 900000
	@${REINPLACE_CMD} -e 's|-Wmissing-include-dirs||' \
		${WRKSRC}/configure
.endif
	@${MV} ${WRKSRC}/daemon/libvirtd.conf ${WRKSRC}/daemon/libvirtd.conf.sample
	@${REINPLACE_CMD} -e 's|libvirtd\.conf|libvirtd.conf.sample|' \
		${WRKSRC}/daemon/Makefile.in

	@${MV} ${WRKSRC}/src/libvirt.conf ${WRKSRC}/src/libvirt.conf.sample
	@${REINPLACE_CMD} -e 's|conf_DATA = libvirt.conf|conf_DATA = libvirt.conf.sample|' \
		${WRKSRC}/src/Makefile.in

	@${MV} ${WRKSRC}/src/qemu/qemu.conf ${WRKSRC}/src/qemu/qemu.conf.sample
	@${REINPLACE_CMD} -e 's|qemu.conf |qemu.conf.sample |' \
		${WRKSRC}/src/Makefile.in
	@${REINPLACE_CMD} -e 's|qemu.conf$$|qemu.conf.sample|' \
		${WRKSRC}/src/Makefile.in

	@${REINPLACE_CMD} -e 's|cp $$(DESTDIR)|cp -f $$(DESTDIR)|' \
		${WRKSRC}/src/Makefile.in

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
.for doc in AUTHORS ChangeLog INSTALL NEWS README TODO
	${INSTALL_DATA} ${WRKSRC}/${doc} ${STAGEDIR}${DOCSDIR}
.endfor

.for lib in ${STRIP_FILES}
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/${lib}
.endfor

regression-test: build
	@cd ${WRKSRC} && ${SETENV} ${MAKE_ENV} ${MAKE_CMD} check

.include <bsd.port.mk>
