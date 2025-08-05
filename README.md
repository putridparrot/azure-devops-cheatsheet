# Azure Devops cheat sheet

A list of usefules information for use in Azure Devops.

**Logging** 

| Command | Description | Example |
|---------|-------------|---------|
| ##vso[task.setvariable variable=varName]value | Set a pipelne variable across steps |  echo "##vso[task.setvariable variable=buildStatus]failed" |
| ##vso[task.setvariable variable=varName;isOutput=true]value | Sets an output variable from a job/task | echo "##vso[task.setvariable variable=result;isOutput=true]success" | 
| ##vso[task.setprogress value=XX;] | Updates progress bar in UI | echo "##vso[task.setprogress value=30;]Starting tests" | 
| ##vso[task.complete result=SucceededWithIssues;]message | Marks task as partially succeeded | echo "##vso[task.complete result=SucceededWithIssues;]Minor warnings occurred" | 
| ##vso[task.logissue type=error]message | Logs an error message | echo "##vso[task.logissue type=error]Deployment failed" | 
| ##vso[task.logissue type=warning]message | Logs a warning message | echo "##vso[task.logissue type=warning]Rollback occurred — manual intervention may be required" | 
| ##vso[build.updatebuildnumber]value | Dynamically updates build number | echo "##vso[build.updatebuildnumber]MyApp v1.2.3" | 
| ##vso[artifact.upload artifactname=name]path | Uploads an artifact for later use | echo "##vso[artifact.upload artifactname=logs]logs/error.log" | 
| ##vso[telemetry.publish area;feature]payload | Sends telemetry data | (used mainly by extensions) | 

**Common Condition Functions**

Used by the _condition:_ of jobs/tasks.

| Function | Description |
|----------|-------------|
| succeeded() | Runs only if the previous job/stage complete with success (default behavior) |
| failed() | Runs only if the previous job/stage failed |
| succeddedOrFailed() | Runs regardless of success or failure (but not if cancelled) |
| always() | Runs even if the pipeline was cancelled |
| canceled() | Runs only if the pipeline was cancelled |
| eq(a, b) | Runs if a equals b |
| ne(a, b) | Runs if a does NOT equal be |
| and(...) | AND logical operator |
| or(...) | OR logical operator |
| not(...) | NOT logical operator |

We can use functions such as succeeded() to reference the previous job as well as succeeded('Build') where _Build_ is a previous job name.

**Some Predefined System Variables**

| Variable | Description |
|----------|-------------|
| Build.BuildId | Unique ID for the build |
| Build.SourceBranch | Full ref of the branch (i.e. ref/heads/main) |
| Build.SourceBranchName | The branch name (i.e. main) |
| Build.ArtifactStagingDirectory | Path to the stage build artifacts |
| System.AccessToken | Token for access Azure Devops REST APIs |
| System.Debug | Enables verbose logging when set to _true_ |
| Agent.OS | OS of the build agent (i.e. Windows_NT, Linux) |
| Pipeline.Workspace | Root directory for pipeline execution |

See [User predefined variables](https://learn.microsoft.com/en-us/azure/devops/pipelines/build/variables?view=azure-devops&tabs=yaml) for a comprehensive list.
