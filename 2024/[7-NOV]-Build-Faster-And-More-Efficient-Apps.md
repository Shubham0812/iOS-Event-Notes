
# Build faster and more efficient apps
#### Apple Developer Event - In Person - 7th November 2024 - Apple Developer Center Bengaluru


## Talk - 1 - Improve performance from development to release 
#### by Ashok Prabhu @ Apple


-- We learned how to leverage Xcode's capabilities to detect problem areas, including the use of the View Hierarchy Debugger and Memory Graph Debugger. We also discussed test cases—every developer's bane—with a focus on performance tests for app launch and more.

The talk was divided into three key areas - Develop, Test, Monitor.


### Develop

-- While developing your app, you should try to leverage XCode's capabilities to figure out issues and performance problems within your app and optimise them. 

Some notable **capabilities** are - 

1. **Memory Graph Debugger**
-- This debugger helps you identify memory leaks, retain cycles, and excess memory usage that can lead to slowness in your app, and if it's badly managed then it can also lead to app termination. Something you should definitely avoid.

2. **View Hierarchy Debugger**
-- This debugger helps you debug your app's UI, allowing you to identify layout issues, constraint issues, excessive view hierarchies and unoptimised / problematic UI Components.

3. **Performance Thread Checker**
-- Detects when you're updating the UI on a background threads, unoptimised runtime issues that brings app slowness and also helps in identifying race-conditions and thread-related issues.

4. **Instruments**
-- Xcode Provides lots of instruments that you can use to profile various aspects of your app. 
-- To work with instruments you first have to profile your project.

 
 * Time Profiler
     * Measures how long different parts of your code take to execute and helps you identify performance bottlenecks.
     
 * Allocations 
     * Tracks memory allocation and finds memory leaks in your app
---
### Test

-- Aside from the usual Unit & UI tests, you can also write **Performance tests**. 

It's a key part of ensuring that your app runs efficiently, especially as you add new features and optimize existing ones. 

It helps identify bottlenecks and ensures that changes made to the codebase don’t negatively impact the app’s performance.

You can do various kinds of Performance Tests with XCTests

* Simple Performance Test to measure Time Elapsed
* Measure the execution time of Specific Code Blocks
* Measure the Memory & CPU usage of complex functions
* Create your own custom Performance Metrics
* Measure App Launch Time


Example on Measuring **App Launch Time performance**

-- App startup performance testing focuses on how quickly the app initializes and becomes interactive for the user. 

To measure this, you can use **XCTest’s** `measure` method to track the time taken from launching the app to when it’s fully loaded.

    import XCTest

    class AppLaunchPerformanceTests: XCTestCase {

        func testAppLaunchPerformance() {
            // Measure the startup time of the app
            measure(metrics: [XCTOSSignpostMetric.applicationLaunch]) {
                let app = XCUIApplication()
                app.launch()  // Launch the app
            }
        }
    }
    
-- In addition to measuring the launch time, you might want to set a benchmark or threshold for app startup performance. For example, you might want the app to launch within 1.5 seconds.

    import XCTest

    class AppLaunchPerformanceTests: XCTestCase {

        func testAppLaunchPerformance() {
            // Measure the startup time of the app
            let startTime = Date()
            measure(metrics: [XCTOSSignpostMetric.applicationLaunch]) {
                let app = XCUIApplication()
                app.launch()
            }
            let duration = Date().timeIntervalSince(startTime)
            
            XCTAssertTrue(duration < 1.5, "App launch time exceeds 1.5 seconds.")
        }
    }


---
### Monitor

-- Use **Organiser** to check out past releases and gain meaningful insights. Xcode Organiser provides various reports and Key metrics that you can use to figure out the pain points, and problems that your users are facing.

Few notable ***features*** of the Organiser

1. **Crash Logs**

-   **Identify Patterns in Crashes**: Crash logs show issues faced by users in the field. Analyzing them helps you locate problematic areas and prioritize fixes.

-   **Common Causes of Crashes**: Pay attention to memory issues, null pointer dereferencing, and thread-related crashes.
 ---
2. **Energy Metrics**
-   **Battery Usage**: High energy usage can lead to a poor user experience. Organizer provides insights into your app’s battery consumption patterns.
-   **Excessive CPU or Network Usage**: Look for spikes in CPU usage or frequent network requests, which can drain the battery.
-   **Optimize Background Work**: Identify background tasks that consume more energy and consider deferring or batching them to reduce power consumption.
---
3. **Memory Usage**
-   **Memory Leaks and High Usage**: Excessive memory usage can lead to slow performance and crashes. Organizer’s memory metrics can help you locate potential memory leaks and large allocations.
-   **Reduce Retain Cycles**: Focus on areas with memory spikes; it often indicates retain cycles or inefficient memory handling.

---
4. **App Launch Times**
-   **Track Cold and Warm Launch Times**: Organizer logs the average launch times, allowing you to see if your optimizations are effective in reducing loading times.
-   **Optimize for Faster Launches**: For longer launch times, examine the app startup process to identify which tasks can be deferred.

---

-- You can also use the **Metric Kit Framework** by Apple to define custom key-metrics, reports and create a dashboard.

---
---

## Talk - 2 - Improve performance from development to release 
#### by Karthick Sarve @ Apple

-- We learned about the best practices and principles that we should follow for writing great SwiftUI code, how to manage the data-flow dependency through the ViewModels to various views efficiently, and how to use the Profiler to figure out ways to optimize the SwiftUI Views, with an amazing walk-through demo.

**Goal**
>Reduce the frequency and cost of view updates to achieve great SwiftUI Performance


There are **3** things that you need to keep in mind to **maximise** performance of SwiftUI

* Keep View Initialisers and Bodies simple
* Break down Monolithic Views
* Structure Dependencies Efficiently


### Keep View Initialisers and Bodies simple

-- **View Initializers** and **Bodies** in SwiftUI are responsible for creating and describing the view hierarchy. However, if they are overly complex or do a lot of work on each update, it can significantly slow down the UI rendering process.


* **Avoid complex logic**: Keep any conditional checks or logic outside of the view body. For example, heavy calculations should not be in the view body.

* **Use `@State` or `@Binding` efficiently**: Instead of recalculating things repeatedly, store results in properties like `@State` or `@Binding` that don’t trigger unnecessary view updates. 

---

### Break down Monolithic Views
-- A **monolithic view** refers to a single large SwiftUI view that handles multiple responsibilities or contains too many subviews. This approach can make it difficult for SwiftUI’s diffing algorithm to efficiently update the view hierarchy when state changes.

* **Modularize your Views**: Break down large views into smaller, reusable components. This allows SwiftUI to efficiently handle re-renders, making it easier to identify which part of the view hierarchy needs updating.

    -- You can use the **@ViewBuilder** attribute with your functions to create functions that returns a view, this will help you modularise your View.
    
    -- You can also create child Views, and pass data to them using @Binding, through @EnvironmentObject or @Enviroment wrappers.

---
### Structure Dependencies Efficiently

-- Efficiently structuring dependencies means managing how data and state are passed down the view hierarchy. In SwiftUI, **dependencies** refer to the data and state that views rely on for rendering.

* Use `@State`, `@Binding`, and `@ObservedObject` correctly
    -- **`@State`** should be used for local view state, i.e., data that only the view needs.
    
    -- **`@Binding`** should be used for passing state down the view hierarchy, but it should be used only when necessary.
    
    --**`@ObservedObject`** and **`@EnvironmentObject`** are useful for managing data models and passing data to many views, but avoid overusing them on views that don’t need the entire model to change.

* Avoid creating new view instances in the body unnecessarily. This can lead to unnecessary state updates and slowdowns.

* If the minimum target deployment of your app is **>= iOS 17** then you should explore the **Observation Framework**.

#### Observation
-- Provides a modern, efficient, and declarative approach to managing data-driven changes in your app, especially when dealing with **state management** and **view updates**. It builds on concepts like **state binding** but with an emphasis on better performance and a more intuitive way of handling data flow between objects and views.

*  Only updates affected views that are using the @Observable adhered View-Model, this increases the performance drastically.

* You don't need to be confused whether to use @ObservedObject or @StateObject, with Observation framework everything is **@State** 

---
---

## Talk - 3 - Speed up Core ML loading and execution
#### by Sandhya Kundapur @ Apple

-- We learned about the things we should keep in mind while we analyze our  
models. How to optimize the training of the models using the various CPU, GPU & Neural engines, how to debug it efficiently through a demo, and then how to use those models in the app.


### Optimisation Strategies for Model Training

* Use the Neural Engine when Possible 
    * The Apple Neural Engine (ANE) is highly optimized for Core ML tasks, delivering faster inference times and lower power consumption. It’s especially suited for models that rely on deep learning.

* With iOS 15 and later, Core ML models can be updated or fine-tuned directly on the device. This training utilizes available hardware efficiently, and for resource-intensive tasks, offloading to the GPU or Neural Engine can help accelerate performance. 

*  Core ML allows you to specify the preferred processing unit (`MLComputeUnits`). Choose `.all` to leverage all available compute units (CPU, GPU, and ANE), or specifically select `.cpuOnly`, `.gpuOnly`, or `.neuralEngineOnly` based on the model and device capabilities.


---
### Debugging Core ML Models

* Use the **Core ML template in Instruments** to monitor the time taken for loading and executing models. This tool helps identify bottlenecks and visualizes performance across CPU, GPU, and Neural Engine.

* Use the Core ML console logs to check for warnings, such as falling back to the CPU if a model isn’t supported on the GPU or Neural Engine. This can reveal potential misconfigurations. 

---

### Use Models Efficiently in the App

* Use asynchronous APIs (`async/await`) to load models in the background, preventing blocking of the main thread. This keeps the app responsive during loading.

* Only load Core ML models when necessary instead of pre-loading them. This reduces memory usage and loading times when users don’t access all models immediately.

* For image or video processing models, batch predictions to minimize the number of calls to the model, improving speed. Preprocess inputs outside the model for efficiency.

---
### Best Practices

* When feasible, select or train models that are smaller, even if slightly less accurate. Lightweight models load faster and are more responsive.

* Pass in optimized input sizes and request minimal output to reduce model complexity.   

---
That's it guys, all the sessions were amazing and kudos to the Apple Developer Team @ Bengaluru to organise such a fantastic event!

Events like these are great to connect with the fellow iOS developers, learn something new, and get inspired to work on your own amazing ideas.


See ya next time. :D

 
      

