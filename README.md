# Background Service
A simple example of running a Background service in asp.net core application


```
public class MyBackgroundService : BackgroundService
{
    private readonly ILogger<MyBackgroundService> _logger;

    public MyBackgroundService(ILogger<MyBackgroundService> logger)
    {
        _logger = logger;
    }

    protected override async Task ExecuteAsync(CancellationToken cancellationToken)
    {
        while(!cancellationToken.IsCancellationRequested)
        {
            _logger.LogInformation("Running from my background service");
            await Task.Delay(10000);
        }
    }

    public override Task StopAsync(CancellationToken cancellationToken)
    {
        _logger.LogInformation("Stopping my background service");
        return base.StopAsync(cancellationToken);
    }
}
```

Inject the class in the startup

```
builder.Services.AddHostedService<MyBackgroundService>();
```


