## Web API 2 with Ninject
I’ve been using [Ninject](https://http://www.ninject.org/) for a few years, but every time I use it with Web Api 2 I have to search for the setup instructions. For my future self and your reference, here is how it is done.

1. Get Nuget packages
```
Ninject.Web.WebApi
Ninject.Web.Common.WebHost
```

This will pull down the WebActivatorEx package and add a new class called NinjectWebCommon to your App_Start directory.

2. Edit NinjectWebCommon.cs
NinjectWebCommon.cs is missing a key feature if you want to use ninject to construct the controllers, and I presume that is why you are using ninject inside a Web Api project.

In the CreateKernel() method add the code below just before the return statement. Now ninject will be used to resolve controller dependencies.
```
GlobalConfiguration.Configuration.DependencyResolver = new NinjectDependencyResolver(kernel);
return kernel;
```

3. Add bindings
```
private static void RegisterServices(IKernel kernel)
{
    kernel.Bind<ISomeRepository>()
        .To<SomeRepository>()
        .WithConstructorArgument("connectionString", ConfigurationManager.AppSettings["DomainDatabase"]);
}
```
4. Use bindings in controllers
```
public class SomeController : ApiController
{
    private readonly ISomeRepository _repo;
    public SomeController(ISomeRepository repo)
    {
        _repo = repo;
    }
 
    public SomeModel Get(int id)
    {
        SomeEntity ent = _repo.GetById(id);
        
        return ToModel(ent);
    }
}
```
