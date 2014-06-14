AUTOMAKE_OPTIONS = foreign
SUBDIRS = man scripts

.PHONY: release \
	release_build release_push release_clean \
	release_build_tarball \
	release_push_tarball \
	release_clean_tarball

release: release_build release_push release_clean

release_build: release_build_tarball

release_push: release_push_tarball

release_clean: release_clean_tarball

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
