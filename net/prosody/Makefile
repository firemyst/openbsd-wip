# $OpenBSD: Makefile,v 1.12 2010/11/19 22:31:37 espie Exp $

SHARED_ONLY=	Yes

COMMENT=	communications server for Jabber/XMPP written in Lua
DISTNAME=	prosody-0.8.2
#REVISION=	3
CATEGORIES=	net
MASTER_SITES=	http://prosody.im/downloads/source/

HOMEPAGE=	http://prosody.im/

MAINTAINER=	Jolan Luff <jolan@openbsd.org>

# MIT
PERMIT_DISTFILES_CDROM=	Yes
PERMIT_DISTFILES_FTP=	Yes
PERMIT_PACKAGE_CDROM=	Yes
PERMIT_PACKAGE_FTP=	Yes

USE_GMAKE=	Yes
USE_GROFF =	Yes
MODULES=	lang/lua
LIB_DEPENDS=	devel/libidn \
		lang/lua
RUN_DEPENDS+=	archivers/luazlib \
		devel/luaevent \
		devel/luafs \
		security/luasec \
		textproc/luaexpat
WANTLIB+=	crypto idn lua


CONFIGURE_STYLE=simple
CONFIGURE_ARGS+=--prefix="${PREFIX}" \
		--sysconfdir="${SYSCONFDIR}/prosody" \
		--datadir="/var/prosody" \
		--with-lua="${LOCALBASE}" \
		--c-compiler="${CC}" \
		--linker="${CC}" \
		--ldflags="-I/usr/include -I${LOCALBASE}/include -L/usr/lib -L${LOCALBASE}/lib -shared" \
		--cflags="${CFLAGS} -fPIC"

FAKE_FLAGS+=	CONFIG=${DESTDIR}${PREFIX}/share/examples/prosody

pre-configure:
	${SUBST_CMD} ${WRKSRC}/prosody ${WRKSRC}/prosodyctl

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/doc/prosody
	${INSTALL_DATA} ${WRKSRC}/README \
		${PREFIX}/share/doc/prosody
	touch ${PREFIX}/share/examples/prosody/prosody.log

.include <bsd.port.mk>
