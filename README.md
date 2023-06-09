# TabHub Card Action

TabHub Card Action helps you to generate your own album cards used in [TabHub Chrome Extension](https://tabhub.io).

## Usage

For example, you can put your family's photos in a repo:

1. all these images must be put under a folder named `images` that we can call it an album or resource
2. you can have several `images` folders in different directories, and a manifest json file will be generated according to one `images` folder
3. if current directory already exists an `images` folder, those `images` folders in current sub directories wouldn't be included in result

then use this action to generate some `manifest.json`s that you can use to play these photos in a new tab of your Chrome(or Edge) browser, you can find the action will also generate a [README file](https://github.com/tabhub/tabhub-card-action/blob/master/ACTION_README_SAMPLE.md) for you that contains a list of manifest file's link.

### Add a resource manifest link in your TabHub

Copy a resource manifest link address from README file generated by the action and set it in the TabHub as below:

<p align="center">
<img src="https://raw.githubusercontent.com/image-store/github/master/add-tabhub-resource-url.png" width="350">
</p>

### Workflow Configuration

You can follow the config below to create your GitHub workflow, or just [use a template](https://github.com/tabhub/tabhub-card-action-template/generate) we provide.

```yaml
# your GitHub Action workflow config file

name: Test TabHub Card Action

on: [push]

jobs:
  test_tabhub_action:
    runs-on: ubuntu-latest
    name: A job to test TabHub action
    steps:
    - name: Checkout
      uses: actions/checkout@v2
    - name: TabHub Card Action
      uses: tabhub/tabhub-card-action@master
    - name: Git commit
      run: |
        # git commit if there's any change
        if test -n "$(git status --porcelain 2>/dev/null)"; then
            git config --local user.email "41898282+github-actions[bot]@users.noreply.github.com"
            git config --local user.name "github-actions[bot]"
            git add .
            git commit -m "Update manifest"
            git push
        fi
```
