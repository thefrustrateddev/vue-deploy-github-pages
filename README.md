# Build vue app and then create branch gh-pages to deploy on github pages
This action first builds the vue application and then creates a new gh-pages branch in your repo which is further used for deployment to github pages.

## Getting Started
1. Create the `vue.config.js` file in root folder of your applications.
2. Add the following code to the `vue.config.js`

repoName = The name of the repository where you are adding the github action

```javascript
module.exports = {
    publicPath: '/${{ repoName }}/'
}
```
3. Create a .github folder in the root director of your application
4. Create a workflows folder with main.yml file under .github folder
5. Add the following code to the above created main.yml file

```yml
name: Build and Deploy Vue Application to Github Pages
on: 
    push:
        branch:
            -main/master/{{name of the branch you want to trigger you action on}}
jobs:
  build_deploy_vue:
    runs-on: ubuntu-latest
    name: Build and Deploy Vue
    steps:
    - uses: actions/checkout@v2
    - id: Build-Deploy-Vue
      uses: thefrustrateddev/vue-deploy-github-pages@v1.0.0
      with:
        username: '{{your_username}}'
        reponame: '{{your_repositoryname}}'
        token: ${{ secrets.GITHUB_TOKEN }} # no need to change this line this is used to create the branch in your application repository
```
4. Go to Repository Settings.
5. Open Pages under settings and select gh-pages and select folder as /(root)

## Options 
|   Name        |            Description                |     Default        |  Required |
|:-------------:|:-------------------------------------:|:------------------:|:---------:|
| username      | Your username                         |        -           |     Y     |
| reponame      | Your repository name                  |        -           |     Y     |
| token         | Add as mentioned in the readme above  |        -           |     Y     |
| buildscript   | Git commit email                      | build              |     N     |
| basebranchname| Base branch for cerating gh-pages     | master             |     N     |
| email         | email to be added to a commit         | action@example.com |     N     |
| name          | username to be added to a commit      | action             |     N     |
| commitmessage | Commit message to create gh-pages     | Create gh-pages    |     N     |
