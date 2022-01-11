# nuget-release-action

Action to release Nuget packages

```yml
name: Release

on:
  release:
    types:
      - released
  workflow_dispatch:

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Prepare
        id: prep
        shell: bash
        run: |
          VERSION=${GITHUB_REF#refs/tags/}
          echo ::set-output name=version::${VERSION}
      - name: Pubish
        uses: sitkoru/nuget-release-action@v1
        with:
          version: ${{ steps.prep.outputs.version }}
          project_path: src/PROJECT/PROJECT.csproj
          nuget_host: ${{ secrets.NUGET_HOST }}
          nuget_token: ${{ secrets.BOT_TOKEN }}
```
