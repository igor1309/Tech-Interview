# Tech Interview Q&A

## SwiftUI

<details>
    <summary>What is the entry point of a SwiftUI application??</summary>

    Starting with iOS 14, Apple introduced the `App` protocol for pure SwiftUI applications which mostly replaced the AppDelegate and SceneDelegate. A most basic SwiftUI App implements the body property as entry point of the application.
</details>

<details>
    <summary>What is `AnyView`? Should we avoid using `AnyView` in SwiftUI? How?</summary>

    SwiftUI provides the type-erased view `AnyView` that can be used as a wrapper for any other SwiftUI view, for example to be able to return multiple view types from a function.

    While using AnyView might be a good choice in some cases, Apple recommends using alternatives when possible.

    That’s because SwiftUI uses a so called structural identity mechanism, where SwiftUI uses the view's type to identify it and to determine when they should be updated. Since AnyView erases the type of the view, it reduces SwiftUI’s ability to efficiently update the views.

    Using `ViewBuilder` instead of AnyView.
    Using Group instead of AnyView.
    Using Generics instead of AnyView.
</details>

<details>
    <summary>What's the difference between a view's initializer and onAppear()?</summary>

    Paul Hudson's suggested approach: Using `init()` and `onAppear()` both let us run some code early in a view's lifecycle, however it's important to understand the difference between them.

    SwiftUI creates all its view structs immediately, even creating destination views for navigation links, which means that initializers are run immediately and that's probably not something you want. In comparison, code placed in an onAppear() modifier is called only when the view is shown for the first time, so it's the right place to do complex work.
</details>

<details>
	<summary>What is opaque type in Swift? Is it used in SwiftUI?</summary>

	Swift 5.1 introduced a new language feature called opaque types. Opaque types give us the capability to return a concrete type without having to expose it.

	A common place where we use opaque types today is inside the body of a SwiftUI view: `var body: some View { ... }`.
</details>

<details>
    <summary>How would you create programmatic navigation in SwiftUI?</summary>

    Paul Hudson's suggested approach: SwiftUI makes simple navigation as easy as it should be, but programmatic navigation is trickier because you need to declare all your states up front.

    If you want to talk about tags for `NavigationLink` views you can, but I would say the important thing here is to think about why it's important – handling deep links from Spotlight or widgets are both good places where you need to navigate programmatically.
</details>

<details>
    <summary>What is the purpose of the `ButtonStyle` protocol?</summary>

    Paul Hudson's suggested approach: SwiftUI provides several built-in button styles depending on which platform you're targetting, and the ButtonStyle protocol allows us to create new button styles that can be reused across our apps to get consistent designs.

    For bonus points, compare and contrast ButtonStyle with PrimitiveButtonStyle.
</details>

<details>
    <summary>When would you use `GeometryReader`?</summary>

    Paul Hudson's suggested approach: Start with the simplest answer and work your way up: `GeometryReader` allows us to read the size and location of a view, which means we can create proportional layouts or create adaptive modifiers that change their values as a view moves around the screen.

    For bonus points you might want to add that `GeometryReader` is frequently over-used.
</details>

<details>
    <summary>Why does SwiftUI use structs for views?</summary>

    Paul Hudson's suggested approach: Start with the easiest answer, then work your way up: structs are used because they are much simpler and much more efficient than classes. Once you've nailed the basics, go on to discuss why this matters – SwiftUI is free to recreate your view structs whenever and as often as it wants, so performance needs to be good.
</details>

<details>
    <summary>How to use `async/await` in SwiftUI?</summary>

    Depending on the scenario, there are different ways to use Swift's `async/await` syntax in SwiftUI. We might want to call an asynchronious function for example when:

    - a SwiftUI view appears
    - as a response to a user action like a button tap or a pull to refresh

    Using the `task` view modifier
    Calling the async static function (Task)
    Using the `refreshable` view modifier
</details>

<details>
    <summary>How to identify objects when using SwiftUI's `List` and `ForEach`?</summary>

    When we use `List` or `ForEach` to create dynamic views, SwiftUI needs to know how to identify them. If an object conforms to the `Identifiable` protocol, SwiftUI will automatically use its `id` property for identifying.

    By using `\.self` (or other `keyPath`), we tell SwiftUI to use the whole object as the identifier. In our case, it tells SwiftUI that each value in the array is unique and can be used for identifying.

    In the last approach, it is important to make sure that the values in the array are unique, since otherwise `ForEach` might incorrectly reuse the resulting views.
</details>

<details>
    <summary>What is Dynamic Color? How would you create Dynamic Colors in SwiftUI?</summary>

     SwiftUI offers a range of predefined semantic colors we can use in our views. But in most cases, we want to define our own custom colors that automatically adapt to certain user preferences like dark mode changes.   

    Using the asset catalog to define dynamic colors for SwiftUI views: Configure dark mode colors by opening the `Attributes Inspector` and select `Any, Dark` in the `Appearances` dialog.

    The programmatic approach to define dynamic colors for SwiftUI views: make use of the `UITraitCollection` class.

    [Dynamic colors in SwiftUI](https://tanaschita.com/20211108-dynamic-colors-in-swiftui/)
</details>

<details>
    <summary>How to preview SwiftUI views in dark mode?</summary>

    Use `preferredColorScheme(\_:)` view modifier.
</details>

<details>
    <summary>How to bridge SwiftUI and UIKit?</summary>

    To use a UIKit view in a SwiftUI view, we wrap the UIKit view in a SwiftUI view that conforms to the `UIViewRepresentable` protocol.
    For using SwiftUI views inside UIKit, we initialize a `UIHostingController` with the SwiftUI view and then use it like a standard view controller.   
</details>

<details>
    <summary>What is the difference between `AppDelegate`, `SceneDelegate` and SwiftUI's `App` protocol?</summary>

    Starting with iOS 14, Apple introduced the App protocol for pure SwiftUI applications which mostly replaced the AppDelegate and SceneDelegate. A most basic SwiftUI App implements the body property as the entry point of a SwiftUI application.

    Before that, we would have used a UIHostingViewController initialized with a SwiftUI view in the AppDelegate or SceneDelegate.

    The body property is of type some Scene we recognize from the scene based approach introduced in iOS 13. The returned WindowGroup is a Scene which wraps SwiftUI views.

    To observe scene life cycle changes we know from SceneDelegate's methods, we can add an environment property scenePhase and subscribe to any changes.

    For now, we still may need the AppDelegate or SceneDelegate in some cases, for example to register for remote push notifications or to add quick home screen actions. In those cases, we can use the UIApplicationDelegateAdaptor property wrapper.

    In doing so, SwiftUI instantiates the AppDelegate and calls the delegate’s methods in response to life cycle events or communications with the iOS system as we know it from UIKit.

    [Understanding the difference between AppDelegate, SceneDelegate and SwiftUI's App protocol](https://tanaschita.com/20220404-understanding-the-difference-between-appdelegate-scenedelegate-and-swiftui-app-protocol/)
</details>

<details>
    <summary>What king of toolbars do we have in SwiftUI?</summary>

    With iOS 14, Apple introduced the `toolbar()` modifier allowing us to add toolbar items to different places in SwiftUI views.

    Depending on the configuration of the `ToolbarItem` (`placement`) we add inside a toolbar and the platform, the system places it accordingly:

    - in the bottom bar: `.bottomBar`
    - in the navigation bar: `.principal`, `.navigationBarTrailing` and `.navigationBarLeading`
    - above the keyboard: `.keyboard`
    - in modal views: `.confirmationAction`, `.destructiveAction`, `.cancellationAction`
</details>

<details>
    <summary>How to manage lifecycle events in SwiftUI iOS applications?</summary>

    When working with views in an iOS application, we often need to trigger side effects when certain lifecycle events occur - for example loading or refreshing some data when a view appears.

    In UIKit, we did that by overriding methods like `viewDidAppear(_:)` or `viewDidDisappear(_:)`.

    SwiftUI also provides methods like `onAppear(perform:)`, `onDisappear(perform:)` and `task(priority:_:)` to react to lifecycle events.

    Not a SwiftUI view lifecycle method per se, the `onReceive(_:perform:)` method can be useful to react to application lifecycle events - for example to update a view when the app enters foreground.
</details>

<details>
    <summary>How to make basic animations in SwiftUI?</summary>

    To add an animation to a SwiftUI view, the framework provides the following two options:

    - `animation(_:value:)` view modifier for animations when a certain state value changes
    - `withAnimation(_:_:)` global function which we can use to apply state changes and create animations for all affected views
</details>

### Property Wrappers

<details>
    <summary>What is a property wrapper?</summary>

    Like the name implies, a property wrapper is essentially a type that wraps a given value in order to attach additional logic to it — and can be implemented using either a struct or a class by annotating it with the @propertyWrapper attribute. Besides that, the only real requirement is that each property wrapper type should contain a stored property called wrappedValue, which tells Swift which underlying value that’s being wrapped.

    Although property wrappers are a general Swift feature since they were introduced in Swift 5.1, they are particularly common in SwiftUI – you’ll see `@Published`, `@ObservedObject`, `@EnvironmentObject` and many more, all with the purpose of helping reduce the amount of boilerplate in our code.

    - Some property wrappers allow us to achieve effects that would otherwise not be possible, such as the way @State lets us modify properties inside a struct.
    - Some property wrappers specifically require you to have done extra work elsewhere, and may crash your app if that work isn’t done. For example, @FetchRequest expects you to have placed a Core Data managed object context into the environment ahead of time.
    - You may apply only one property wrapper at a time, which means `@ObservedObject @Binding var value = SomeClass()` is not allowed.
    - Even though some property wrappers look similar (looking at you, `@Environment` and `@EnvironmentObject`!) they are all different and it’s important you use them appropriately.
    - You can create your own property wrappers if you want, but this isn’t required to use SwiftUI.
</details>

<details>
    <summary>How would you explain SwiftUI’s environment to a new developer?</summary>

    Paul Hudson's sSuggested approach: I would suggest you start off nice and broad, and say that the environment acts a bit like a singleton manager – you place objects in there and share them in many places. But then you want to dive into the details a little more, perhaps saying that actually you can subdivide the environment if you want, allowing some views to have different environment objects.

    I would recommend you try to mention how the environment differs from just injecting an ObservableObject instance in an initializer.
</details>

<details>
	<summary>What is `@Environment`?</summary>

	With the `@Environment` property wrapper, SwiftUI provides a possibility to share data between views without explicitly passing the data from view to view. By setting an environment property on a view, it will be available not only in the view itself but also in all of its subviews.

	SwiftUI provides predefined values that we can use just out of the box like `colorScheme`, `managedObjectContext`, `timeZone`, `openURL` and more.
</details>

<details>
	<summary>How to create custom `@Environment` values in SwiftUI?</summary>

	With the `@Environment` property wrapper, we have the possibility to share data between SwiftUI views without explicitly passing the data from view to view.

	Besides using the predefined values provided by SwiftUI, we can also create our own custom `@Environment` values using the following 3 steps:

	1. Declare a new environment key type conforming `EnvironmentKey` protocol.
	2. Define custom environment value property by extending `EnvironmentValues`
	3. Done. Use it.

	[How to create custom `@Environment` values in SwiftUI](https://tanaschita.com/20210206-how-to-create-custom-environment-values-in-swiftui/)
</details>

<details>
	<summary>What is a `@FetchRequest`?</summary>

	A @FetchRequest property wrapper provided by SwiftUI allows us to fetch data from a `Core Data` store in a SwiftUI view.

	To filter or sort the results, `FetchRequest` offers sortDescriptors and predicate as parameters.

	The fetch request and its results use the managed object context stored in the environment. For that reason, we need to inject a Core Data managed object context into the environment before using it.
</details>

<details>
	<summary>What does the `@Published` property wrapper do?</summary>

	Paul Hudson's suggested approach: As with many questions, the best answer here starts with a simple definition (when used inside an ObservableObject an @Published property will automatically send out change notifications when its value changes), then diving into a practical example. So, you might say that a class you’re using in SwiftUI has an array of todo list items, and when that array changes the UI should update – a simple, real-world use for `@Published`.
</details>

<details>
	<summary>What does the `@State` property wrapper do?</summary>

	Paul Hudson's suggested approach: Remember to start with a basic definition first, then provide a practical example. Here, that means saying the `@State` allows us to mutate a value that belongs to a struct without using mutating methods. When it comes to a practical example, almost any kind of value-type SwiftUI binding is good, such as storing text in a TextField.
</details>

<details>
    <summary>When would you use `@StateObject` versus `@ObservedObject`?</summary>

    Paul Hudson's suggested approach: I would recommend you start by making the similarities and differences clear, then sum up by answering the question directly. So, you would say that both of these property wrappers monitor an observable object for changes, and refresh SwiftUI views when changes happen. However, `@StateObject` is used when you create an object for the first time and want to retain ownership of it, whereas `@ObservedObject` is used in other places where you pass the object and does not retain ownership.
</details>

<details>
    <summary>How can an observable object announce changes to SwiftUI?</summary>

    Paul Hudson's suggested approach: There are two primary ways this is done: using the `@Published` property wrapper, or by calling `objectWillChange.send()` directly.

    Try to provide examples of when one is preferable over the other, such as saying that you might use `@Published` by default, switching over to `objectWillChange.send()` for times when you need more fine-grained control.
</details>

