#
# Copyright (C) 2003 Christophe Varoqui, <christophe.varoqui@opensvc.com>
#
TOPDIR = ../..
include ../../Makefile.inc

CPPFLAGS +=  -I$(multipathdir) -I$(mpathutildir)
CFLAGS += $(LIB_CFLAGS)
LDFLAGS += -L$(multipathdir) -L$(mpathutildir)
LIBDEPS = -lmultipath -lmpathutil -laio -lpthread -lrt

# If you add or remove a checker also update multipath/multipath.conf.5
LIBS= \
	libcheckcciss_tur.so \
	libcheckreadsector0.so \
	libchecktur.so \
	libcheckdirectio.so \
	libcheckemc_clariion.so \
	libcheckhp_sw.so \
	libcheckrdac.so

all: $(LIBS)

libcheck%.so: %.o
	$(Q)$(CC) $(LDFLAGS) $(SHARED_FLAGS) -o $@ $^ $(LIBDEPS)

install:
	$(Q)$(INSTALL_PROGRAM) -m 755 $(LIBS) $(DESTDIR)$(plugindir)

uninstall:
	$(Q)for file in $(LIBS); do $(RM) $(DESTDIR)$(plugindir)/$$file; done

clean: dep_clean
	$(Q)$(RM) core *.a *.o *.gz *.so

OBJS := $(LIBS:libcheck%.so=%.o)
.SECONDARY: $(OBJS)

include $(wildcard $(OBJS:.o=.d))

dep_clean:
	$(Q)$(RM) $(OBJS:.o=.d)
