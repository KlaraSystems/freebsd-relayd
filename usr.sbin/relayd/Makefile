#	$OpenBSD: Makefile,v 1.27 2014/04/21 14:57:17 reyk Exp $

PROG=		relayd
SRCS=		parse.y
SRCS+=		agentx.c ca.c carp.c check_icmp.c check_script.c \
		check_tcp.c config.c control.c hce.c log.c name2id.c \
		pfe.c pfe_filter.c pfe_route.c proc.c \
		relay.c relay_http.c relay_udp.c relayd.c \
		shuffle.c snmp.c ssl.c ssl_privsep.c
# BEGIN FreeBSD-relayd
# Currently, relayd does not support SNMP traps on FreeBSD.
SRCS:=		${SRCS:Nagentx.c}
SRCS:=		${SRCS:Nsnmp.c}
# Currently, relayd does not support CARP demote on FreeBSD.
SRCS:=		${SRCS:Ncarp.c}
# Currently, relayd does not support modifying routing tables on FreeBSD.
SRCS:=		${SRCS:Npfe_route.c}
# END FreeBSD-relayd
MAN=		relayd.8 relayd.conf.5

LDADD=		-levent -lssl -lcrypto -lutil
DPADD=		${LIBEVENT} ${LIBSSL} ${LIBCRYPTO} ${LIBUTIL}
CFLAGS+=	-Wall -I${.CURDIR} -I${.CURDIR}/../snmpd
# BEGIN FreeBSD-relayd
# Currently, relayd does not support SNMP traps on FreeBSD.
CFLAGS:=	${CFLAGS:N-I${.CURDIR}/../snmpd}

CFLAGS+=	-D__dead=""
CFLAGS+=	-I${.CURDIR}/../../lib/libevent
CFLAGS+=	-I${.CURDIR}/../../lib/libutil
# END FreeBSD-relayd
CFLAGS+=	-Wstrict-prototypes -Wmissing-prototypes
CFLAGS+=	-Wmissing-declarations
CFLAGS+=	-Wshadow -Wpointer-arith
CFLAGS+=	-Wsign-compare
CLEANFILES+=	y.tab.h

.include <freebsd.mk>
.include <bsd.prog.mk>
