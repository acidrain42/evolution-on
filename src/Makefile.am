AM_CPPFLAGS =                                                   \
	-I$(EVOLUTION_SOURCE)                           	\
	-I$(top_srcdir)                                 	\
	-DGETTEXT_PACKAGE="\"$(GETTEXT_PACKAGE)\""      	\
	-DLOCALEDIR="\"$(LOCALEDIR)\""                  	\
	-DEVOLUTION_VERSION_STRING=\"$(EVOLUTION_EXEC_VERSION)\"\
	-DEVOLUTION_VERSION=$(evolution_version_int)            \
	-DEVOLUTION_GLADEDIR=\""$(gladedir)"\"                  \
	-DEVOLUTION_ICONDIR=\""$(ICON_DIR)"\"                   \
	-DLIBNOTIFY_VERSION=$(LIBNOTIFY_VERSION)		\
	$(TRAY_EPLUGIN_CFLAGS)					\
	$(GTKHTML_EDITOR_CFLAGS)


%.eplug.in: %.eplug.xml
	LC_ALL=C $(INTLTOOL_MERGE) -x -u /tmp $< $@

%.eplug: %.eplug.in
	sed -e "s%+PLUGIN_INSTALL_DIR+%$(PLUGIN_INSTALL_DIR)%" \
	-e "s%+GETTEXT_PACKAGE+%$(GETTEXT_PACKAGE)%" \
	-e "s%+LOCALEDIR+%$(LOCALEDIR)%" \
	-e "s%+ICON_DIR+%$(ICON_DIR)%" \
	-e "s%+VERSION+%$(VERSION)%" \
	$< > $@

plugindir = $(PLUGIN_INSTALL_DIR)
plugin_DATA = 					\
		org-gnome-evolution-on.eplug

plugin_LTLIBRARIES = liborg-gnome-evolution-on.la

liborg_gnome_evolution_on_la_SOURCES = tray.c
liborg_gnome_evolution_on_la_CFLAGS=$(libappindicator_CFLAGS)
liborg_gnome_evolution_on_la_LIBADD = $(LIBGCONFBRIDGE_LIBS) $(LIBNOTIFY_LIBS)	\
	$(libappindicator_LIBS)
liborg_gnome_evolution_on_la_LDFLAGS = -module -avoid-version -rpath $(PLUGIN_INSTALL_DIR)

gsettings_SCHEMAS =                            \
	org.gnome.evolution.plugin.evolution-on.gschema.xml

@INTLTOOL_XML_NOMERGE_RULE@

@GSETTINGS_RULES@

convertdir = $(datadir)/GConf/gsettings
convert_DATA = evolution-on.convert

EXTRA_DIST = 	org-gnome-evolution-on.eplug.xml	\
		$(convert_DATA)                         \
		$(gsettings_SCHEMAS:.xml=.xml.in)


BUILT_SOURCES = org-gnome-evolution-on.eplug

CLEANFILES = $(BUILT_SOURCES)

DISTCLEANFILES = $(gsettings_SCHEMAS)
