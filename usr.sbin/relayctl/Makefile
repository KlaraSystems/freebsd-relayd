#	$OpenBSD: Makefile,v 1.6 2014/01/18 05:54:51 martynas Exp $

.PATH:		${.CURDIR}/../relayd

PROG=		relayctl
SRCS=		log.c relayctl.c parser.c

MAN=		relayctl.8

LDADD=		-lutil
DPADD=		${LIBUTIL}
CFLAGS+=	-Wall -Werror -I${.CURDIR} -I${.CURDIR}/../relayd
# BEGIN FreeBSD-relayd
CFLAGS+=	-D__dead=""
CFLAGS+=	-I${.CURDIR}/../../lib/libevent
CFLAGS+=	-I${.CURDIR}/../../lib/libutil
# END FreeBSD-relayd
CFLAGS+=	-Wstrict-prototypes -Wmissing-prototypes
CFLAGS+=	-Wmissing-declarations
CFLAGS+=	-Wshadow -Wpointer-arith -Wcast-qual
CFLAGS+=	-Wsign-compare
CDIAGFLAGS=

.include <freebsd.mk>
.include <bsd.prog.mk>
