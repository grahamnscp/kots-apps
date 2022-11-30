# Replicated vendor portal app manifest files to show muliple helm chart components
Manifest files for the replicated vendor portal to deploy a sample application made up of multiple helm charts.  Some components are enabled using custom license fields used as feature flags.

Ensure that you have a valid Replicated Vendor Portal API token defined in your environment and set the desired application slug value.

```
export REPLICATED_APP=my-kafka-app
export REPLICATED_API_TOKEN=<user token value>
```

Load the app into the vendor portal using
```
 make createapp
```

Which calls the replicated cli under the covers
```
replicated app create ${REPLICATED_APP}
```

Create your first release using `make release`
```
replicated release create \
	--auto -y \
	--yaml-dir manifests \
	--promote Unstable
```
Note: for the --auto flag to work there needs to be a git config present with a 'commit' made

Define the two custom license fields referenced in the manifests
```
- Field:feature-flag-embedded-pg Type:Integer Default:1
- Field:feature-flag-kafka-ui    Type:Integer Default:1
```

Create an end customer in the vendor portal and you will see these new license fields there, try setting one to '0' initially to test on your first deployment, you can change them later and perform a 'license sync' in the kots admin portal UI.

Happy testing

