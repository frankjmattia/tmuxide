dist_bin_SCRIPTS = tmuxide log-pane
CLEANFILES = $(dist_bin_SCRIPTS)

EXTRA_DIST = tmuxide.in log-pane.in

do_subst = sed \
	-e 's,[@]PACKAGE[@],$(PACKAGE),g' \
	-e 's,[@]PACKAGE_VERSION[@],$(PACKAGE_VERSION),g'

tmuxide: tmuxide.in Makefile
	$(do_subst) < $(srcdir)/tmuxide.in > tmuxide
	chmod +x tmuxide

log-pane: log-pane.in Makefile
	$(do_subst) < $(srcdir)/log-pane.in > log-pane
	chmod +x log-pane
