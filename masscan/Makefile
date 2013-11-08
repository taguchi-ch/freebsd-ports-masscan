# Created by: Chie Taguchi <taguchi.ch@gmail.com>
# $FreeBSD$

PORTNAME=	masscan
PORTVERSION=	1.0
CATEGORIES=	security
MASTER_SITES=	https://github.com/robertdavidgraham/masscan/archive/
DISTNAME=       ${PORTVERSION}

MAINTAINER=	taguchi.ch@gmail.com
COMMENT=	Very fast port scanner

LICENSE=        GPLv3

BASE_WRKSRC=    ${WRKDIR}/${PORTNAME}-${PORTVERSION}
WRKSRC=		${BASE_WRKSRC}
USE_GMAKE=      yes
MAKE_ENV+=	LIBS="${LIBS}" \
		INCLUDES="${INCLUDES}" \
		FLAGS2="${FLAGS2}"
FETCH_ARGS=     -Fpr

MAN8=           masscan.8

.include <bsd.port.pre.mk>

LIBS=           -lpcap -lm ${PTHREAD_LIBS}
INCLUDES=       -I.
FLAGS2=

pre-build:
	${REINPLACE_CMD} -e "s|gcc -dumpmachine|uname -s|" ${WRKSRC}/Makefile
	${REINPLACE_CMD} -e "s|CC = gcc|CC ?= gcc|" ${WRKSRC}/Makefile

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/bin/masscan ${STAGEDIR}${PREFIX}/bin/masscan
	${INSTALL_MAN} ${WRKSRC}/doc/masscan.8 ${STAGEDIR}${MANPREFIX}/man/man8/

regression-test: build
		${WRKSRC}/bin/masscan --selftest

.include <bsd.port.post.mk>
