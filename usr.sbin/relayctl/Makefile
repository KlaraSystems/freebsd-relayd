#	$OpenBSD: Makefile,v 1.8 2015/11/21 12:37:42 reyk Exp $

.PATH:		${.CURDIR}/../relayd

PROG=		relayctl
SRCS=		log.c util.c relayctl.c parser.c
# BEGIN FreeBSD-relayd
# XXX: For some reason, bmake is unable to handle the log.o file from relayd
# correctly. Work around that.
SRCS:=		${SRCS:Nlog.c}
# END FreeBSD-relayd

MAN=		relayctl.8

LDADD=		-lutil
DPADD=		${LIBUTIL}
# BEGIN FreeBSD-relayd
# XXX: For some reason, bmake is unable to handle the log.o file from relayd
# correctly. Work around that.
LDADD+=		${.CURDIR}/../relayd/log.o
DPADD+=		${.CURDIR}/../relayd/log.o
# Pass the right libutil implementation.
LIBUTIL=	${.CURDIR}/../../lib/libutil/libutil.a
LDADD:=		${LDADD:N-lutil} ${LIBUTIL}
# END FreeBSD-relayd
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
