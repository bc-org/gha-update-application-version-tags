## Update Application Version Tags in Configuration Files

Get your new versions of your application (docker images) deployed. The aim of this action is aiding automated deployment processes
using tools like Helm and ArgoCD. It takes yaml configuration files and replaces all version tags with a new one using
a standard format e.g.:

```yaml
my-app: v0.0
```

### Single mode

The action will look in the `working directory` for a file called `values-[phase]` by default and change all application 
`tag`s using the above format. 

### Single cascade

The action expects three configuration files in `cascade` mode: values-dev.yaml, values-stage.yaml, and values-prod.yaml
whereby the prefix `values-` can be set using the `prefix` option.

Application version `tag`s are changed by `phase`using the following rules:

- `phase` dev changes values-dev.yaml only
- `phase` stage changes the config files for dev and stage
- `phase` prod changes the config files for all phases


## Options

| option             | required | default   | description                                  |
|--------------------|----------|-----------|----------------------------------------------|
| app                |  true    | None      | Name of the application                      | 
| phase              |  true    | dev       | Deployment phase (dev, stage, prod, ignore)  |
| tag                |  true    | None      | Version tag                                  |
| prefix             |  false   | values-   | Prefix of the configuration file             |
| working-directory  |  false   | ./        | Working directory                            |
| mode               |  false   | cascading | Whether to cascade                           |
| delimiter          |  false   | :         | Delimiter between app and version tag        |


## Example

```yaml
  - name: set-version-tag-cate
    uses: actions/update-application-version-tags@main
    with:
      app: my-app
      phase: dev
      tag: v0.0.0
```


