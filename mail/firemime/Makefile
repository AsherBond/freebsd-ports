# Created by: Dean Hollister <dean@odyssey.apana.org.au>
# $FreeBSD$

PORTNAME=	firemime
PORTVERSION=	0.9.4
PORTREVISION=	1
CATEGORIES=	mail devel
MASTER_SITES=	http://www.firestuff.org/projects/ \
		http://www.wa.apana.org.au/~dean/sources/ \
		ftp://ftp.wa.apana.org.au/pub/pc/unix/packages/

MAINTAINER= ports@FreeBSD.org
COMMENT=	Callback-based interface for parsing MIME-encoded messages

USES=	tar:bzip2
HAS_CONFIGURE=	yes
USE_LDCONFIG=	yes
WRKSRC=		${WRKDIR}/${PORTNAME}

MAN1=		mimedump.1
MAN3=		firemime_decode_body.3 firemime_get_full_header.3 firemime_get_header.3 \
		firemime_param_value.3 firemime_parse.3 firemime_strerror.3 \
		firemime_strip_comments.3 firemime_strip_markup.3 libfiremime.3

NO_STAGE=	yes
.include <bsd.port.pre.mk>

post-patch:
	@${REINPLACE_CMD} -e 's|(unsigned char) dest-\>s\[o++\] = c|dest-\>s\[o++\] = (char) c|' \
		${WRKSRC}/firemime.c

pre-configure:
	@-${RM} -r ${WRKSRC}/firemake/*.orig

post-install:
	${LN} -s libfiremime.so.0.9.4 ${PREFIX}/lib/libfiremime.so.0

.include <bsd.port.post.mk>
