prefix = /usr
bindir = $(prefix)/bin
sharedir = $(prefix)/share
localedir = $(sharedir)/locale
launcherdir = $(sharedir)/applications
mandir = $(sharedir)/man
man1dir = $(mandir)/man1
CFLAGS = --std=c99

all:
	valac -X -D'GETTEXT_PACKAGE="timeshift"' --Xcc="-lm" --thread "Main.vala" "Utility.vala" "MainWindow.vala" "SettingsWindow.vala" "RestoreWindow.vala" "ExcludeMessageWindow.vala" -o timeshift --pkg glib-2.0 --pkg gio-unix-2.0 --pkg posix --pkg gtk+-3.0 --pkg gee-1.0 --pkg libsoup-2.4 --pkg json-glib-1.0 

clean:
	rm -rf *.o timeshift

install:
	mkdir -p "$(DESTDIR)"
	mkdir -p "$(DESTDIR)$(bindir)"
	mkdir -p "$(DESTDIR)$(sharedir)"
	mkdir -p "$(DESTDIR)$(mandir)"
	mkdir -p "$(DESTDIR)$(man1dir)"
	mkdir -p "$(DESTDIR)$(launcherdir)"
	mkdir -p "$(DESTDIR)$(sharedir)/timeshift"
	mkdir -p "$(DESTDIR)$(sharedir)/pixmaps"
	mkdir -p "$(DESTDIR)$(localedir)/it_IT/LC_MESSAGES"
	
	#binary
	install -m 0755 timeshift "$(DESTDIR)$(bindir)"
	
	#shared files
	cp -dpr --no-preserve=ownership -t "$(DESTDIR)$(sharedir)/timeshift" ./share/timeshift/*
	chmod --recursive 0755 $(DESTDIR)$(sharedir)/timeshift/*
	
	#launcher
	install -m 0755 TimeShift.desktop "$(DESTDIR)$(launcherdir)"
	
	#app icon
	install -m 0755 ./share/pixmaps/timeshift.png "$(DESTDIR)$(sharedir)/pixmaps/"
	
	#translations
	msgfmt --check --verbose -o "$(DESTDIR)$(localedir)/it_IT/LC_MESSAGES/timeshift.mo" ../po/timeshift-it.po

uninstall:

	#binary
	rm -f "$(DESTDIR)$(bindir)/timeshift"
	
	#shared files
	rm -rf "$(DESTDIR)$(sharedir)/timeshift"
	
	#launcher
	rm -f "$(DESTDIR)$(launcherdir)/TimeShift.desktop"
	
	#app icon
	rm -f "$(DESTDIR)$(sharedir)/pixmaps/timeshift.png"
	
	#translations
	rm -f "$(DESTDIR)$(localedir)/*/LC_MESSAGES/timeshift.mo"
