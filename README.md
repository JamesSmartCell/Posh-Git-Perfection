# Posh-Git-Perfection
Simple script to get minimal posh-git branch display

Want to see just this when you're in a source directory?

```
~\StudioProjects\my-awesome-source [Ultimate-Optimisation]>
```

Then use this script in your PowerShell profile:

```
Import-Module -Name posh-git

cd StudioProjects
cd alpha-wallet-android

function prompt 
{
    $origLastExitCode = $LASTEXITCODE

    if ($status = Get-GitStatus -Force) 
    {
        $prompt =  Write-Prompt '~' -ForegroundColor White
        $prompt += Write-Prompt "$($ExecutionContext.SessionState.Path.CurrentLocation)".Substring($Home.Length) -ForegroundColor White
        $prompt += Write-Prompt ' [' -ForegroundColor Yellow
        $prompt += Write-Prompt $status.Branch -ForegroundColor Cyan
        $prompt += Write-Prompt ']' -ForegroundColor Yellow
        $prompt += "$('>' * ($nestedPromptLevel + 1)) "
    }
    else
    {
        $prompt = "$($ExecutionContext.SessionState.Path.CurrentLocation)> "
    }

    $LASTEXITCODE = $origLastExitCode
    $prompt
}
```
