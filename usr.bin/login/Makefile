# 	@(#)Makefile	8.1 (Berkeley) 7/19/93
# $FreeBSD$

.include <src.opts.mk>
.include <src.tools.mk>

PACKAGE=	runtime

CONFS=	fbtab login.conf login.access
PROG=	login
SRCS=	login.c login_fbtab.c
CFLAGS+=-DLOGALL
LIBADD=	util pam

WARNS?=	5

.if ${MK_AUDIT} != "no"
SRCS+=	login_audit.c
CFLAGS+= -DUSE_BSM_AUDIT
LIBADD+=	bsm System notify
.endif

.if ${MK_SETUID_LOGIN} != "no"
BINOWN=	root
BINMODE=4555
PRECIOUSPROG=
.endif

.include <bsd.endian.mk>
afterinstallconfig:
	${CAP_MKDB_CMD} ${CAP_MKDB_ENDIAN} ${DESTDIR}/etc/login.conf
.if defined(NO_ROOT) && defined(METALOG)
	echo ".${DISTBASE}/etc/login.conf.db type=file mode=0644 uname=root gname=wheel" | \
		cat -l >> ${METALOG}
.endif

.include <bsd.prog.mk>
