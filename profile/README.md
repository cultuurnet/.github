# Setting up a new repository

## 1. Initial settings

Go to the form to [create a new repository in our organization](https://github.com/organizations/cultuurnet/repositories/new) and fill out the basic information of your repository. 

### Template

Select the `cultuurnet/.template` template. Do not check "include all branches".

### Repository name

* Always use `kebab-case` for new repository names
* Try to use a common prefix for repositories related to the same project. For example `uitpas-mobile-app`, `uitpas-frontend`, and so on
* Use one of these common names when applicable:
  * `{project}-frontend`
  * `{project}-backend`
  * `{project}-mobile-app`

### Visibility

Most of our repositories are public and open-source.

You are free to decide whether your repository should be public or private, but note that we only have [a limited number of GitHub Actions Minutes per month for all of our private repositories combined](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions).
Since most repositories use GitHub Actions to run their CI checks and sometimes even to build the applications, these usually run out quite fast when we have too many private repositories.

So it is advised to only make your repository private if it is strictly necessary. Common reasons to make a repository private are:

* The repository contains code and/or data that we do not own but have licensed from another party, and we are not free to share it publically.
* The repository contains secrets like credentials. Note that you can store secrets as [GitHub Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) though, so this is only valid in some very specific use cases.

On the other hand, there are some common mistakes why a repository should be private:

* Making the source code publicly available does not make the application less secure. See for example <https://rubygarage.org/blog/open-source-software-security>
* There might be doubt if we want to share the code with the world, to avoid it being re-used. However we ourselves use a lot of open-source code in our projects, and we get discounts and sponsorships from SAAS tools because we also share a lot of our code as open-source. So making a repository private just to not share the code goes against that philosophy. Also because our applications are very specific, the more common use case for someone "re-using" our code would be for learning purposes. Last but not least we can control the terms that our code is shared under by [adding a license to the repository](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/adding-a-license-to-a-repository). (More guidelines about licenses will be added in the future.)

## 2. General settings

After creating your new repository, go to its settings via this URL (replace `<your-project>` with your repository name):

```
https://github.com/cultuurnet/<your-project>/settings
```

(Alternatively, browse to the "Settings" tab of your repository.)

Next, enable the following general settings for your repository:

- [x] **Allow auto-merge**
- [x] **Automatically delete head branches**

## 3. Access

Go to the access settings of your repository via the following URL:

```
https://github.com/cultuurnet/<your-project>/settings/access
```

(Alternatively, browse to the "Settings" tab of your repository and then go to "Collaborators and teams" in the sidebar of the settings page.)

Next, click the "Add teams" button and add the `cultuurnet/contributors` team with the `Maintain` role. 
This will give contributors from external firms that we work with access to your repository to push changes, open PRs, merge PRs, etc.

## 4. Code owners

Edit the following `.github/CODEOWNERS` file in your repository to enable the rule for global code owners (by uncommenting it) and replace the `@example1` and `@example2` users with actual usernames of GitHub users that will work on this repository.

You can find this file via the following URL:
```
https://github.com/cultuurnet/<your-project>/blob/main/.github/CODEOWNERS
```

You can read more about the CODEOWNERS file in the GitHub documentation: <https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners>

## 5. Protecting branches

It is highly recommended to disable pushes to the `main` branch of your repository and require pull requests, so that changes go through a code review process.

To configure this, go to the branches settings of your repository via the following URL:

```
https://github.com/cultuurnet/<your-project>/settings/branches
```

(Alternatively, browse to the "Settings" tab of your repository and then go to "Branches" in the sidebar of the settings page.)

Next, click "Add branch protection rule" and enter `main` as the "Branch name pattern".

Then, select the following options:

- [x] **Require a pull request before merging**
  - [x] Require approvals (usually enabled by default)
  - [x] Require review from Code Owners
- [x] **Require status checks to pass before merging**
  - [x] Require branches to be up to date before merging
- [x] **Restrict who can push to matching branches** (leave the list of allowed people/teams/apps empty)
