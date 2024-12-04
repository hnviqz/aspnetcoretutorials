### ASP.NET Core Attribute Routing using Tokens

In this article, I will discuss the ASP.NET Core Attribute Routing using Tokens with Examples. Please read our previous article before proceeding to this one, as we will work with the same example that we worked on in our previous article. Our previous article discussed Attribute Routing in ASP.NET Core MVC Applications. As part of this article, we will discuss the following pointers.

1. Understanding Tokens in Attribute Routing.
2. Token Example in Attribute Routing.
3. Advantages of using Tokens in Attribute Routing.
4. Do we need to write the action  token on each action method?

### Tokens in Attribute Routing:

Tokens in Attribute Routing allow you to dynamically replace parts of the route template. These tokens are placeholders within route templates that are substituted with actual values during URL generation and routing. In ASP.NET Core MVC, Tokens in Attribute Routing are enclosed in square brackets [] and can represent values such as controller name, action name, etc. The following are the Commonly Used Tokens in ASP.NET Core MVC:

- **[controller]**: This represents the controller’s name without the “Controller” suffix. For example, a controller named HomeController would have the [controller] token substituted with Home.
- **[action]**: Represents the name of the action method. For example, an action method named Index would mean the [action] token gets substituted with Index.

### Token Replacement Example in Attribute Routing:

Let us understand Token Replacement in ASP.NET Core Attribute Routing with an example. Please modify the Home Controller class as shown below. Here, we are applying the token [controller] to the Home Controller and the token [action] to all the action methods.

```csharp
using Microsoft.AspNetCore.Mvc;
namespace FirstCoreMVCApplication.Controllers
{
    //Using token controller at the Controller level using the Route Attribute
    public class HomeController : Controller
    {
        //Using token action at the Action Method level using the Route Attribute
        [Route("[action]")]
        public string Index()
        {
            return "Index() Action Method of HomeController";
        }

        //Using token action at the Action Method level using the Route Attribute
        [Route("[action]")]
        public string Details()
        {
            return "Details() Action Method of HomeController";
        }
    }
}
```

With the above controller and action tokens in place with the Route Attribute, you can now access the Index action method of the Home Controller with the URL **/Home/Index**. Similarly, you can access the Details action method of the Home Controller using the URL **/Home/Details**.


- The route of the Index action method would be /Home/Index because of the [controller] and [action] tokens used in the controller's route attribute.
- The route for the Details action method would be /Home/Details because of the [controller] and [action] tokens used in the controller's route attribute.

Now, run the application and see if everything is working as expected. The token controller will be replaced with the actual controller name, and similarly, the token action will be replaced with the actual action method name.

### How Do We Make the Index Action Method the Default Action?

With the controller and action tokens in place with Route Attribute, if you want to make the Index action method of Home Controller the default action, then you need to include the [Route(“/”)] attribute with an “/” on the Index action method. So, modify the Home Controller as shown below and rerun the application. It should display the Index Action method.

```csharp
using Microsoft.AspNetCore.Mvc;

namespace FirstCoreMVCApplication.Controllers
{
    //Using token controller at the Controller level using the Route Attribute
    [Route("[controller]")]
    public class HomeController : Controller
    {
        //Using token actin at the action method level using the route attribute
        [Route("/")] ///This will make the Index action method as the Default action
        [Route("[action]")]
        public string Index()
        {
            return "Index() Action method of HomeController";
        }

        //Using token action at the action method level using the route attribute
        [Route("[action]")]
        public string Details()
        {
            return "Details() action method of HomeController";
        }
    }
}
```

### Do We Need to Write the Action Token for Each Action Method?

Not Really. If you want all your action methods to apply the action token, then instead of applying the [action] token on each and every action method, you can apply it only once on the controller. So, in this case, the Route attribute at the controller level should include both controller and action tokens like [Route(“[controller]/[action]”)]. So, modify the Home Controller class as shown below to apply the controller and action tokens at the controller level.

```csharp
using Microsoft.AspNetCore.Mvc;

namespace FirstCoreMVCApplication.Controllers
{
    //Using controller and action tokens at the Controller level using the Route attribute
    [Route("[controller]/[action]")]
    public class HomeController : Controller
    {
        //This will make the Index action method as the default action
        [Route("/")]
        public string Index()
        {
            return "Index() action method of HomeController";
        }


        public string Details()
        {
            return "Details() action method of HomeController";
        }
    }
}
```

Now, run the application, and it should work as expected. 

### Advantages of Using Tokens in ASP.NET Core Attribute Routing:

Attribute routing with tokens provides a flexible and expressive way to define dynamic routes in your ASP.NET Core MVC application. The following are the advantages of using Token with Attribute Routing in ASP.NET Core Web Applications:


- **Reduction of Redundancy**: Tokens help reduce redundancy by eliminating the need to repeat the controller or action names in each route definition.
- **Maintainability**: Changing the name of a controller or action only requires updating the class or method name, not the routes.
- **Clarity**: Route templates with tokens are generally easier to read and understand, as they directly relate to the controller and action names.
- 
In the next article, I will discuss Attribute Routing vs Conventional Routing in ASP.NET Core. In this article, I explain the need and use of ASP.NET Core Attribute Routing using Tokens with Examples. I hope you enjoy this Token Replacement in ASP.NET Core Attribute Routing article. 