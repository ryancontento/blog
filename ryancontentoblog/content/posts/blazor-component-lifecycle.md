---
title: "Blazor Component Lifecycle"
date: 2022-07-04T18:13:24-04:00
draft: false
categories: [Blazor, Development]
tags: [.NET, Blazor, C#, Component, Lifecycle]
---

Blazor is a component based framework, and like all of these modern frameworks, every component has a lifecycle. They are rendered, they exist in the UI, and eventually are disposed. There are 7 main methods that handle the lifecycle of a Blazor/razor component. These components are processed with a set of synchronous and asynchronous methods. All Blazor lifecycle methods are provided by the ComponentBase class, which all components inherit from. For the methods other than the first one we will cover, the synchronous version is always called before the asynchronous one.

## SetParametersAsync()

The first method that is called once the parent component of a component is rendered is the SetParametersAsync() method. This is where the process always starts. This method is the only one that requires us to call the base method. If you fail to do so, the component will not load. The base method does two things for us:

- Sets the values for any parameters the component defines.
- Calls the correct life cycle methods.

As the name suggests, this will set the parameters and cascading parameters for the components via the ParameterView object passed from the parent component.

Unlike the other lifecycle methods, SetParametersAsync() is **always** asynchronous. The following two methods are very closely related to both this initial method and each other.

## OnInitialized{Async}()

OnInitialized() and OnInitializedAsync() are the methods called following SetParametersAsync() **if** the component is being executed for the first time. This method will only run once in the lifecycle of a component. This is very similar to the constructor of a C# class.

## OnParametersSet{Async}()

The OnParametersSet() or OnParametersSetAsync() methods are called following SetParametersAsync(). This method, unlike OnInitialized(), will run each time the incoming parameters of a component change.

OnParametersSet() will run, **then** calls OnParametersSetAsync(). It will then make a call to StateHasChanged() (more on that later).

## OnAfterRender{Async}()

Again, as the name clearly suggests, these methods are called after a component has finished rendering. All elements and references for a component will be rendered at this point of the lifecycle.

## More on Async Calls

When making an asynchronous call in Blazor, multiple awaited calls will fire simultaneously. Lets look at a quick example.

```
List<string> _helloWorldList = new();

protected override async Task OnInitializedAsync()
{
		_helloWorldList.Add("hello");

		await Task.Delay(2000);
	  _helloWorldList.Add(" World");

		await Task.Delay(2000);
	  _helloWorldList.Add("!");
}
```

This example shows a list of strings with 3 items being added. If you were to watch this output, you will see that first “hello” will print, then 2 seconds later, both “ World” and “!” will print. It is understandable if you would have expected each await to complete before moving on to the next await, but that is not the case.

## StateHasChanged()

The final lifecycle method we need to mention is StateHasChanged(). This method will notify the render tree that the state of the component has changed. This method call is usually handled by the other lifecycle methods, but I have come across a handful of situations where an explicit call of StateHasChanged() was needed.

## Bonus Method: Dispose()

The Dispose() method is not needed very often, and is not one of the main lifecycle methods of a component. Dispose() does not inherit from ComponentBase like the other methods we have covered. This method is used to clean up resources, just like in any other C# application. This method is worth mentioning because if your component subscribes to an event you must use Dispose() before the component is destroyed. Failing to do so will cause a memory leak.

In order to access this method, the component will need to implement the IDisposable interface. Doing this will allow Blazor to handle the remaining work for us.

## Final Thoughts

This was far from a comprehensive breakdown of the component lifecycle, but I hope this helps clear up the basics. These lifecycle methods are vital to effectively creating components that work flawlessly together. If you have any questions, comments, or requests for covering specifics, please feel free to reach out [here](<[https://ryancontento.dev/#contact](https://ryancontento.dev/#contact)>).
