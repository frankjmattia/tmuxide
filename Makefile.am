AUTOMAKE_OPTIONS = foreign
SUBDIRS = man scripts

.PHONY: release \
	release_build release_push release_clean \
	release_build_tarball release_build_homebrew\
	release_push_tarball release_push_homebrew \
	release_clean_tarball release_clean_homebrew

edit_package = sed \
	-e 's|@PACKAGE[@]|$(PACKAGE)|g' \
	-e 's|@PACKAGE_VERSION[@]|$(PACKAGE_VERSION)|g' \
	-e 's|@DIST_ARCHIVES[@]|$(DIST_ARCHIVES)|g' \
	-e 's|@DIST_SHA[@]|$(DIST_SHA)|g'

release: release_build release_push release_clean

release_build: release_build_tarball release_build_homebrew

release_push: release_push_tarball release_push_homebrew

release_clean: release_clean_tarball release_clean_homebrew

release_build_tarball: Makefile distcheck
	git clone --branch gh-pages git@github.com:frankjmattia/tmuxide.git gh-pages
	cp $(DIST_ARCHIVES) gh-pages
	cd gh-pages && \
		git add $(DIST_ARCHIVES) && \
		git commit -m "Release v$(PACKAGE_VERSION)"

release_push_tarball:
	cd gh-pages && \
		git push

release_clean_tarball:
	rm -rf gh-pages

release_build_homebrew: DIST_SHA
	git clone git@github.com:frankjmattia/homebrew-formulae.git homebrew-formulae
	$(edit_package) homebrew/tmuxide.rb.in > homebrew-formulae/Formula/tmuxide.rb
	cd homebrew-formulae && \
	  git add Formula/tmuxide.rb && \
	  git commit -m "tmuxide: Release v$(PACKAGE_VERSION)"

release_push_homebrew:
	cd homebrew-formulae && \
		git push

release_clean_homebrew:
	rm -rf homebrew-formulae

DIST_SHA: Makefile distcheck
	$(eval DIST_SHA := $(shell shasum $(srcdir)/$(DIST_ARCHIVES) | cut -d' ' -f1))

# vim: set ts=4:
