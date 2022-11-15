app_slug := "${REPLICATED_APP}"
CHANNEL=Unstable

createapp:
	@replicated app create ${app_slug}

list-releases:
	@replicated release ls --app ${app_slug}

lint:
	@replicated release lint --app $(app_slug) --yaml-dir manifests

release-auto:
	@replicated release create \
		--auto -y \
		--yaml-dir manifests \
		--promote $(CHANNEL)

release:
	@replicated release create \
		--yaml-dir manifests \
		--promote $(CHANNEL)
