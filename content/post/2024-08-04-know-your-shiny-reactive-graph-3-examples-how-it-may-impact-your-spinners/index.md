---
title: 'Know Your Shiny Reactive Graph: 3 Examples How It May Impact Your Spinners'
author: ''
date: '2024-08-04'
slug: []
categories: []
tags: []
---

# Introduction

We use spinners to inform users about a computation happening in the application. In Shiny you can use libraries like [shinycssloaders](https://github.com/daattali/shinycssloaders) or [waiter](https://github.com/JohnCoene/waiter) to show such a loading indicator.

Both of those libraries use [JavaScript events emitted by Shiny](https://shiny.posit.co/r/articles/build/js-events/) like `shiny:outputinvalidated` ([shinycssloaders](https://github.com/daattali/shinycssloaders/blob/2f2623fa8762c7351e5e6d044d3dae08a677b06f/inst/assets/spinner.js#L56), [waiter](https://github.com/JohnCoene/waiter/blob/776f9f3ccd27aa3322d6c6d37c47b3d7b1f393e6/R/waiter.R#L831)) or `shiny:recalculating` ([waiter](https://github.com/JohnCoene/waiter/blob/776f9f3ccd27aa3322d6c6d37c47b3d7b1f393e6/R/waiter.R#L774)).

Those events are emitted based on what is happening in the reactive graph in our Shiny application.

Depending on how we structure our reactive graph, we might end up in a situation where our spinners don't work smoothly.

In this blog post I'd like to show 3 examples of how the structure of the reactive graph might impact how our spinners behave. 


# Example 1: `renderPlot` based on a `reactive`
In our examples we will be using an app with a single `Run` button. Clicking it results in an artificially slow computation leading to showing a histogram plot.

```r
library(shiny)
library(shinycssloaders)

create_histogram <- function() {
  rnorm(100) |> 
    hist()
}

run_slowly <- function(expr = NULL, time = 1) {
  Sys.sleep(time = time)
  expr
}

ui <- fluidPage(
  actionButton(inputId = "run", label = "Run"),
  plotOutput(outputId = "histogram") |> withSpinner()
)

server <- function(input, output, session) {
  output$histogram <- renderPlot({
    req(input$run)
    
    histogram <- create_histogram() |> 
      run_slowly()
    
    plot(histogram)
  })
}

shinyApp(ui, server)
```

Let's see how it works!

![01_app_gif](/2024-08-04-know-your-shiny-reactive-graph/01_app.gif)


It seems to be working as expected (the spinner is shown right after we click the button).

Let's have a look at the reactive graph of this app.


![01_app-reactive_graph-step_1](/2024-08-04-know-your-shiny-reactive-graph/01-reactive-graph-step_1.png)

It's quite straightforward: our `output$histogram` is based on `input$run` value. 

> The `plotObj` block might seem confusing. It is [created internally by the renderPlot function](https://github.com/rstudio/shiny/blob/d84aa94762b4ffaf7533a007b6cb92c40f4f29af/R/render-plot.R#L124) to make the plot react to dimension changes (we don't need to worry about it in our examples).

After we click the *Run* button, the input gets invalidated.

![01_app-reactive_graph-step_2](/2024-08-04-know-your-shiny-reactive-graph/01-reactive-graph-step_2.png)

As a result `output$histogram` gets invalidated. This triggers the `shiny:outputinvalidated` event which results in a spinner being shown.

![01_app-reactive_graph-step_3](/2024-08-04-know-your-shiny-reactive-graph/01-reactive-graph-step_3.png)

This means that a click of the button directly invalidates the output and that triggers the spinner.

But what if we implement our app in a slightly different way?

# Example 2: `renderPlot` based on a `reactiveVal`

Instead of using a `reactive` let's use `reactiveVal` along with an `observeEvent`:

```r
library(shiny)
library(shinycssloaders)

create_histogram <- function() {
  rnorm(100) |> 
    hist()
}

run_slowly <- function(expr = NULL, time = 1) {
  Sys.sleep(time = time)
  expr
}

ui <- fluidPage(
  actionButton(inputId = "run", label = "Run"),
  plotOutput(outputId = "histogram") |> withSpinner()
)

server <- function(input, output, session) {
  histogram_value <- reactiveVal(NULL, label = "___histogram_value")
  
  observeEvent(input$run, {
    histogram <- create_histogram() |> 
      run_slowly()
    
    histogram_value(histogram)
  }, label = "___observeEvent")
  
  
  output$histogram <- renderPlot({
    req(histogram_value())
    
    plot(histogram_value())
  })
}

shinyApp(ui, server)
```

Let's see how the app behaves now:

![02_app_gif](/2024-08-04-know-your-shiny-reactive-graph/02_app.gif)

That's weird, the app seems much more clunky. The spinner appears for a very short time right before showing the plot which results in this weird flickering effect.

To understand why this is happening let's look at the reactive graph of the app:

![02_app-reactive_graph-step_1](/2024-08-04-know-your-shiny-reactive-graph/02-reactive-graph-step_1.png)

It looks very similar to the previous one, we have an additional part that captures the relationship between `input$run` and `observeEvent`.

Let's see   what happens after we click the *Run* button:

![02_app-reactive_graph-step_2](/2024-08-04-know-your-shiny-reactive-graph/02-reactive-graph-step_2.png)

The `observeEvent` block gets invalidated. In the next step our `observeEvent` starts to run:

![02_app-reactive_graph-step_3](/2024-08-04-know-your-shiny-reactive-graph/02-reactive-graph-step_3.png)

Notice that the slow calculation is part of the `observeEvent`, but `output$histogram` is not invalidated yet. This means that our slow computation is happening, but we are not showing the spinner!

After the slow computation in the `observeEvent`, we update the `histogram_value` reactive value: 

![02_app-reactive_graph-step_4](/2024-08-04-know-your-shiny-reactive-graph/02-reactive-graph-step_4.png)

Which is the moment when `output$histogram` gets invalidated (and our spinner is shown)

![02_app-reactive_graph-step_5](/2024-08-04-know-your-shiny-reactive-graph/02-reactive-graph-step_5.png)

What is happening here is that our spinner is shown **after** the slow computation which leads to:
1. The spinner being shown with a delay
2. The flickering effect as the spinner is shown when we already computed the histogram

To make the spinner behave like expected we can trigger the spinner from our server (e.g. using the `shinycssloaders::showSpinner` function):

```r
  observeEvent(input$run, {
    showSpinner(id = "histogram")
    histogram <- create_histogram() |> 
      run_slowly()
    
    histogram_value(histogram)
  })
```

Now, before running the slow computation, we are sending a message to the browser to show a spinner for our histogram. Which fixes the issue:

![03_app_gif](/2024-08-04-know-your-shiny-reactive-graph/03_app.gif)

The fix is not perfect though as there are other things that may go wrong here. Let's check it out in our next example.

# Example 3: Another reactive element blocking the `observeEvent` with `showSpinner`
What if our app is bigger and there are other reactive elements that might take a long time?

Let's add a second `observeEvent` to our app:

```r
  observeEvent(input$run, {
    run_slowly(time = 2)
  }, priority = 1)
```

We use the `priority` argument here to force it to run before our `observeEvent` with `showSpinner`. Let's see how that impacts the app:


![04_app_gif](/2024-08-04-know-your-shiny-reactive-graph/04_app.gif)

The spinner appears with a delay and there is no flickering.

Let's check the reactive graph, we now have two `observeEvent` expressions that depend on `input$run`:

![04_app-reactive_graph-step_1](/2024-08-04-know-your-shiny-reactive-graph/04-reactive-graph-step_1.png)

After clicking the *Run* button our input gets invalidated:

![04_app-reactive_graph-step_2](/2024-08-04-know-your-shiny-reactive-graph/04-reactive-graph-step_2.png)

Which results in both observeEvents to be invalidated:

![04_app-reactive_graph-step_3](/2024-08-04-know-your-shiny-reactive-graph/04-reactive-graph-step_3.png)

Now the observeEvent with the higher priority (`__observeEvent_1`) is performing computations:

![04_app-reactive_graph-step_4](/2024-08-04-know-your-shiny-reactive-graph/04-reactive-graph-step_4.png)

Which effectively blocks `___observeEvent_2` from running `showSpinner` which causes the spinner to appear with a delay (As we can see in the reactive graph `__observeEvent_1` took 2030ms to run):

![04_app-reactive_graph-step_5](/2024-08-04-know-your-shiny-reactive-graph/04-reactive-graph-step_5.png)

`__obseveEvent_2` starts to be computed - it shows the spinner and updates the `__histogram_value` reactive value:

![04_app-reactive_graph-step_6](/2024-08-04-know-your-shiny-reactive-graph/04-reactive-graph-step_6.png)

The `___histogram_value` reactive value invalidates `output$histogram`:

![04_app-reactive_graph-step_7](/2024-08-04-know-your-shiny-reactive-graph/04-reactive-graph-step_7.png)

`output$histogram` starts to be computed:

![04_app-reactive_graph-step_8](/2024-08-04-know-your-shiny-reactive-graph/04-reactive-graph-step_8.png)

When working on a big app, even if you are not using priorities, you might be surprised by one reactive element blocking another reactive element that is supposed to show a spinner.

Fortunately, there is another solution provided by the `waiter` package. It involves adding the `waiter::triggerWaiter` function in our UI definition:

```r
library(waiter)


ui <- fluidPage(
  useWaiter(),
  actionButton(inputId = "run", label = "Run") |>
    triggerWaiter(id = "histogram"),
  
  plotOutput(outputId = "histogram")
)
```

Let's see how it influences the app:

![05_app_gif](/2024-08-04-know-your-shiny-reactive-graph/05_app.gif)

Now the spinner appears immediately after clicking the *Run* button! The `triggerWaiter` function sets up a JavaScript snippet which watches for *click* events. When this event occurs, it runs additional JavaScript code to show the spinner.

This means that this happens purely on the browser side and there is no need to wait for the server to send the message to the browser to show the spinner.

That said, this comes at the cost of setting up this dependency yourself instead of relying on the reactive graph to do it for you.

# Conclusion

Existing libraries like `shinyjs` or `waiter` make it easy to add spinners to your shiny application. However, if you do not structure your reactive graph properly this might result in:

1. The spinner being shown with a delay
2. Unpleasant flickering of components that are being computed

To avoid those issues you can:
1. Structure your reactive graph in a way where a user action will result in an immediate invalidation of outputs for which spinners have to be shown
2. Use server side functions like `showSpinner`
3. Do things browser side with `triggerWaiter`

> You can find the full examples on GitHub: https://github.com/szymanskir/know.your.reactive.graph.spinners