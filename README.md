# Azure Pipelines

Our common Azure Pipeline workflows used in our projects at [Nimble](https://nimblehq.co/).
- `publish_wiki.yml`: inspired by [GitHub Actions's publish_wiki.yml](https://github.com/nimblehq/github-actions-workflows/blob/develop/.github/workflows/publish_wiki.yml) workflow to publish the wiki content to the [same GitHub's Wiki repository](https://github.com/nimblehq/azure-pipelines/blob/main/Pipelines/publish_wiki.yml#L34) of the current attached GitHub's repository in the Azure DevOps.

## Usage

### Publish Wiki (GitHub)

Prepare the wiki content in folder `.github/wiki/`.

Create a new Azure Pipelines yml file with these configurations as below:
- `group: 'Android Pipelines'`: the variables group to provide variables access in following steps.
- `ref: main` (optional, default is `main`): the branch which contains the version of the publish wiki workflow in this repository.
- `USER_NAME`: the GitHub's user name used to publish the wiki content and has access to the destination's Wiki repository.
- `USER_EMAIL`: the GitHub's user email used to publish the wiki content and has access to the destination's Wiki repository.
- `USER_TOKEN`: the GitHub's [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) of the above username used to publish the wiki content with [basic `repo` scopes](https://docs.github.com/en/developers/apps/building-oauth-apps/scopes-for-oauth-apps#available-scopes).

```
trigger:
  - develop
pr: none

variables:
  - group: 'Android Pipelines'

resources:
  repositories:
    - repository: publish_wiki_template
      type: github
      name: nimblehq/azure-pipelines
      endpoint: nimblehq
      ref: main

jobs:
  - template: Pipelines/publish_wiki.yml@publish_wiki_template
    parameters:
      USER_NAME: $(WIKI_USER_NAME)
      USER_EMAIL: $(WIKI_USER_EMAIL)
      USER_TOKEN: $(WIKI_GITHUB_API_TOKEN)
```

## License

This project is Copyright (c) 2014 and onwards Nimble. It is free software and may be redistributed under the terms specified in the [LICENSE] file.

[LICENSE]: /LICENSE

## About
<a href="https://nimblehq.co/">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://assets.nimblehq.co/logo/dark/logo-dark-text-160.png">
    <img alt="Nimble logo" src="https://assets.nimblehq.co/logo/light/logo-light-text-160.png">
  </picture>
</a>

This project is maintained and funded by Nimble.

We ❤️ open source and do our part in sharing our work with the community!
See [our other projects][community] or [hire our team][hire] to help build your product.

Want to join? [Check out our Jobs][jobs]!

[community]: https://github.com/nimblehq
[hire]: https://nimblehq.co/
[jobs]: https://jobs.nimblehq.co/
