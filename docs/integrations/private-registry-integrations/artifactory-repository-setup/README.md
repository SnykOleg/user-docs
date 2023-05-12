# Artifactory Package Repository setup

{% hint style="info" %}
**Feature availability**\
This feature is available with Enterprise plans. See [pricing plans](https://snyk.io/plans/) for more details.
{% endhint %}

{% hint style="info" %}
**Supported Projects**\
The Artifactory Package Repository integration currently supports [Node.js](../../../scan-application-code/snyk-open-source/snyk-open-source-supported-languages-and-package-managers/snyk-for-javascript/) (npm and Yarn) and [Maven](../../../scan-application-code/snyk-open-source/snyk-open-source-supported-languages-and-package-managers/snyk-for-java-gradle-maven.md) Projects. Gradle Projects are not currently supported.
{% endhint %}

Connecting a custom Artifactory Package Repository enables Snyk to resolve all direct and transitive dependencies of packages hosted on the custom registry and calculate a more complete, accurate dependency graph and related vulnerabilities.

You can configure these types of Artifactory Package Repository:

* Publicly accessible instances protected by basic authentication
* Instances on a private network accessed through Snyk Broker (with or without basic authentication).

These instructions apply to configuring publicly accessible instances. For instructions on configuring a brokered instance, see [Set up Snyk Broker with Artifactory Repository](../../../snyk-admin/snyk-broker/snyk-broker-set-up-examples/set-up-snyk-broker-with-artifactory-repository.md).

The steps to set up Artifactory Repository Manager follow.

1. Go to settings <img src="../../../.gitbook/assets/cog_icon.png" alt="" data-size="line"> > **Integrations > Package Repositories > Artifactory**.
2. Enter the URL of your Artifactory instance, this **must** end with **/artifactory**.
3. Enter your username and password.
4. Select **Save**.

<figure><img src="../../../.gitbook/assets/screenshot_2020-04-17_at_14.38.12.png" alt="Artifactory integration setup"><figcaption><p>Artifactoryrepository setup</p></figcaption></figure>