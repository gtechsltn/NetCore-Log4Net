# Using Log4Net in .NET Core
* [SalesOrder](https://github.com/gtechsltn/SalesOrder)
* https://github.com/gtechsltn/workflow-lib
* https://github.com/gtechsltn/workflow-lib/tree/main/src/TaskManagementTool
* https://github.com/gtechsltn/workflow-lib/tree/main/src/MeetPlanning
* https://github.com/gtechsltn/workflow-lib/tree/main/src/BuildAutomationTool
* https://github.com/gtechsltn/workflow-lib/tree/main/src/Shared/AuthenticationService
* https://github.com/gtechsltn/sqlviewer
* https://github.com/gtechsltn/uptrader-eth-blazor
* https://github.com/gtechsltn/Microsoft-Intelligent-Apps-With-Azure-AI-Services

```
git clone https://github.com/alexeysp11/workflow-auth.git
git clone https://github.com/alexeysp11/workflow-lib.git
git clone https://github.com/alexeysp11/Convo.git
```

## web.config
```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<configSections>
		<section name="log4net" type="log4net.Config.Log4NetConfigurationSectionHandler, log4net" />
	</configSections>
	<log4net>
		<appender name="RollingFile" type="log4net.Appender.RollingFileAppender">
			<file value="Path\To\Logs\app.log" />
			<appendToFile value="true" />
			<maximumFileSize value="500KB" />
			<maxSizeRollBackups value="2" />
			<layout type="log4net.Layout.PatternLayout">
				<conversionPattern value="%date %level %logger - %message%newline" />
			</layout>
		</appender>
		<root>
			<level value="All" />
			<appender-ref ref="RollingFile" />
		</root>
	</log4net>
</configuration>
```

## Program.cs
```
public class Program
{
    public static void Main(string[] args)
    {
        var builder = WebApplication.CreateBuilder(args);
        ....
        builder.Services.AddLog4net();
        ....
        var app = builder.Build();
        ....
        app.Run();
    }
}
```

## Log4NetExtensions.cs
```
public static class Log4NetExtensions
{
    public static void AddLog4net(this IServiceCollection services)
    {        
        XmlConfigurator.Configure(new FileInfo("Path/To/web.config"));
        services.AddSingleton(LogManager.GetLogger(typeof(Program)));
    }
}
```
