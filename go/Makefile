BRANCH	 = main
PACKAGE  = whois
VERSION	 = `date "+%Y.%m%d%"`
NEXT     = `autotag -b $(BRANCH) -n`
RELEASE_DIR  = ..
RELEASE_FILE = $(PACKAGE)-$(VERSION)

.SILENT: all
.SILENT: release-next
.SILENT: _patch
.SILENT: _packages


# Default target.
all:
	echo "Hello $(LOGNAME), nothing to do by default"

release:
	autotag -b $(BRANCH)
	goreleaser release

release-next:
	echo "Next release: v$(NEXT)"

release-build:
	goreleaser release --snapshot --rm-dist

release-notag:
	goreleaser release


_patch:
	# fetch all tags and history:
	git fetch --tags --prune

	if [ `git rev-parse --abbrev-ref HEAD` != "$(BRANCH)" ]; then
		# ensure a local branch exists at 'refs/heads/master'
		git branch --track master origin/$(BRANCH)
	fi

_packages:
