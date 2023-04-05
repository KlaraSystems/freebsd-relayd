#	$OpenBSD: Makefile,v 1.35 2020/10/26 16:52:06 martijn Exp $

PROG=		relayd
SRCS=		parse.y
SRCS+=		agentx_control.c ca.c carp.c check_icmp.c check_script.c \
		check_tcp.c check_tls.c config.c control.c hce.c log.c \
		name2id.c pfe.c pfe_filter.c pfe_route.c proc.c relay.c \
		relay_http.c relay_udp.c relayd.c shuffle.c ssl.c util.c
# BEGIN FreeBSD-relayd
# Currently, relayd does not support SNMP traps on FreeBSD.
SRCS:=		${SRCS:Nagentx_control.c}
# Currently, relayd does not support CARP demote on FreeBSD.
SRCS:=		${SRCS:Ncarp.c}
# Currently, relayd does not support modifying routing tables on FreeBSD.
SRCS:=		${SRCS:Npfe_route.c}
# END FreeBSD-relayd
MAN=		relayd.8 relayd.conf.5

LDADD=		-lagentx -levent -ltls -lssl -lcrypto -lutil
DPADD=		${LIBAGENTX} ${LIBEVENT} ${LIBSSL} ${LIBCRYPTO} ${LIBUTIL}
CFLAGS+=	-Wall -I${.CURDIR}
# BEGIN FreeBSD-relayd
# Pass the right LibreSSL library.
LDADD:=		${LDALL:N-lssl} ${LIBSSL}
# Pass the right libcrypto implementation.
LDADD:=		${LDALL:N-lcrypto} ${LIBCRYPTO}

# Set LIBEVENT and LIBUTIL to the appropriate build artifacts.
LIBEVENT=	${.CURDIR}/../../lib/libevent/libevent.a
LIBUTIL=	${.CURDIR}/../../lib/libutil/libutil.a
# END FreeBSD-relayd
DPADD=		${LIBEVENT} ${LIBSSL} ${LIBCRYPTO} ${LIBUTIL}
CFLAGS+=	-Wall -I${.CURDIR} -I${.CURDIR}/../snmpd
# BEGIN FreeBSD-relayd
# Currently, relayd does not support SNMP traps on FreeBSD.
CFLAGS:=	${CFLAGS:N-I${.CURDIR}/../snmpd}

CFLAGS+=	-D__dead=""
CFLAGS+=	-I${.CURDIR}/../../lib/libevent
CFLAGS+=	-I${.CURDIR}/../../lib/libutil
CFLAGS+=	-I${OPENSSLINCDIR}
# END FreeBSD-relayd
CFLAGS+=	-Wstrict-prototypes -Wmissing-prototypes
CFLAGS+=	-Wmissing-declarations
CFLAGS+=	-Wshadow -Wpointer-arith
CFLAGS+=	-Wsign-compare -Wcast-qual
YFLAGS=

.include <freebsd.mk>
.include <bsd.prog.mk>
