# fable-templates

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/fable-compiler/fable-templates/)

Templates for Fable projects maintained by fable-compiler org

## List of templates

| Name  | Short Name | Description  |
|---|---|---|
| Fable.Template | fable |  Small Fable app project, with the only dependency on Fable.Browser.Dom |


## How to test the template before publishing?

1. Package the template by running `dotnet pack -c Relase minimal/Fable.Template.proj`
2. Install the new version of the tempalte: `dotnet new -i bin/Release/Fable.Template.x.y.z.nupkg`
3. Create the template: `dotnet new -i fable -n <name-of-your-project>`. 
    
    If you are using gitpod to contribute, add `--gitpod` at the end
    
4. `cd <name-of-your-project>`
5. Follow the instructions from the README.md of the installed template

## Maintainer notes

### Requirements

- Your NuGet API key set in `NUGET_KEY` variable.

### Procedure to publish a new version

To publish a new version of the template you need to:

1. Update the changelog of the template you want to publish
2. Run `dotnet tool restore`
3. Run `dotnet fake build -t Release`

### Gitpod condition

In the webpack.config.js, we are adding things like:

```js
//#if( gitpod )
const execSync = require('child_process').execSync;
var isGitPod = process.env.GITPOD_INSTANCE_ID !== undefined;

function getDevServerUrl() {
    if (isGitPod) {
        const url = execSync('gp url 8080');
        return url.toString().trim();
    } else {
        return `http://localhost:${CONFIG.devServerPort}`;
    }
}
//#endif
```

The code between `//#if( gitpod )` and `//#endif` is not included in the generated template. It's here so people can use Gitpod to contribute to this repository.
