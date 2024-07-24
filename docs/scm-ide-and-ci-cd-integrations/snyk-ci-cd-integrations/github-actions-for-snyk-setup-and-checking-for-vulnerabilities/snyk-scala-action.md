# Snyk Scala Action

{% hint style="warning" %}
**Warning:** This image is scheduled for removal on 12 Aug 2024. It is highly recommended that users consider migrating to a newer action to ensure continued support and up-to-date functionality. If you are currently using this image, plan an upgrade as soon as possible to avoid any disruptions in your workflow post this date.
{% endhint %}

This page provides examples of using the Snyk GitHub Action for [Scala](https://github.com/snyk/actions/tree/master/scala). For instructions on using the action and further information see [GitHub Actions integration](https://docs.snyk.io/integrations/ci-cd-integrations/github-actions-integration).

## Using the Snyk Scala Action to check for vulnerabilities

You can use the Snyk Scala Action to check for vulnerabilities as follows:

```yaml
name: Example workflow for Scala using Snyk
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - name: Run Snyk to check for vulnerabilities
        uses: snyk/actions/scala@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

You can use the Snyk Scala Action to check for **only high severity vulnerabilities** as follows:

```yaml
name: Example workflow for Scala using Snyk
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - name: Run Snyk to check for vulnerabilities
        uses: snyk/actions/scala@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          args: --severity-threshold=high
```

## Using the Snyk Scala Action to run snyk monitor

For an example of running `snyk monitor`, see [Snyk monitor example](https://docs.snyk.io/integrations/ci-cd-integrations/github-actions-integration#snyk-monitor-example) on the GitHub Actions integration page.

## Uploading Snyk scan results to GitHub Code Scanning using the Snyk Scala Action

Using `--sarif-file-output` [Snyk CLI option](https://docs.snyk.io/snyk-cli/cli-reference) and the [GitHub SARIF upload action](https://docs.github.com/en/code-security/secure-coding/uploading-a-sarif-file-to-github), you can upload Snyk scan results to GitHub Code Scanning as shown in the example that follows.

The Snyk Action fails when vulnerabilities are found. This would prevent the SARIF upload action from running. Thus you must use a [continue-on-error](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#jobsjob\_idstepscontinue-on-error) option as shown in this example:

```yaml
name: Example workflow for Scala using Snyk
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - name: Run Snyk to check for vulnerabilities
        uses: snyk/actions/scala@master
        continue-on-error: true # To make sure that SARIF upload gets called
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          args: --sarif-file-output=snyk.sarif
      - name: Upload result to GitHub Code Scanning
        uses: github/codeql-action/upload-sarif@v2
        with:
          sarif_file: snyk.sarif
```

{% hint style="info" %}
To use the upload-sarif option for private repos you must have GitHub Advanced Security. &#x20;

If you see the error `Advanced Security must be enabled for this repository to use code scanning`, check that GitHub Advanced Security is enabled. For more information, see "[Managing security and analysis settings for your repository](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-security-and-analysis-settings-for-your-repository)."
{% endhint %}