# Tech Interview Q&A

<details>
	<summary>Question?</summary>

	Answer
</details>

## Swift

<details>
	<summary>What is opaque type in Swift?</summary>

	Swift 5.1 introduced a new language feature called opaque types. Opaque types give us the capability to return a concrete type without having to expose it.

    A function or method with an opaque return type hides its return value’s type information. Instead of providing a concrete type as the function’s return type, the return value is described in terms of the protocols it supports. Hiding type information is useful at boundaries between a module and code that calls into the module, because the underlying type of the return value can remain private. Unlike returning a value whose type is a protocol type, opaque types preserve type identity — the compiler has access to the type information, but clients of the module don’t.   
</details>

<details>
	<summary>Explain Access Control?</summary>

	[The Swift Programming Language: Redirect](https://docs.swift.org/swift-book/LanguageGuide/AccessControl.html)
</details>

<details>
	<summary>What is `closure`?</summary>

	Closure are self contained blocks of functionality that can be passed around and used in code.
</details>

<details>
	<summary>What is `@escaping` and `@nonescaping`?</summary>

	Basically, a non-escape closure can only run the contents inside of it’s body, anything outside of it’s closure cannot be used. A non-escape closure tells the complier that the closure you pass in will be executed within the body of that function and nowhere else. When the function ends, the closure will no longer exist in memory. For example, if we needed to extract any values within our closure to be used outside of it, we may not do so. During the earlier days of Swift, closure parameters were escaping by default. Due to better memory management and optimizations, Swift has changed all closures to be non-escaping by default.

	Essentially escaping closure is the opposite of non-escaping closure. An escaping closure grants the ability of the closure to outlive the function and can be stored elsewhere. By using escape closure, the closure will have existence in memory until all of it’s content have been executed. To implement escaping closure, all we have to do is put @escaping in front of our closure. If you are unsure whether your closure needs escaping, no worries, as I’ve said before the complier is smart enough to let you know.
	There are several ways when we need to implement an escaping closure. One instance is when we use asynchronous execution. When we are dealing with dispatch queue, the queue will hold onto the closure for you, and when the queue is done completing its work, then it will return back to the closure and complete it. Since dispatch queue is outside of the scope, we need to use escaping closure. Another instance is when we need to store our closure to a global variable, property, or any bit of storage that lives on past the function.
</details>

<details>
    <summary>What is a Protocol in Swift?</summary>

    Answer: The protocol is a very common feature of the Swift programming language and the protocol is a concept that is similar to an interface from java. A protocol defines a blueprint of properties, methods, and other requirements that are suitable for a particular task.

    In its simplest form, the protocol is an interface that describes some methods and properties. The protocol is just described as the properties or methods skeleton instead of implementation. Properties and methods implementation can be done by defining enumerations, functions, and classes.

    Protocols are declared after the structure, enumeration or class type names. A single and multiple protocol declaration can be possible. Multiple protocols are separated by commas.
</details>

<details>
    <summary>What is a delegate in Swift?</summary>

    Answer: Delegate is a design pattern, which is used to pass the data or communication between structs or classes. Delegate allows sending a message from one object to another object when a specific event happens and is used for handling table view and collection view events.

    Delegates have one to one relationship and one to one communication.
</details>

### Types

<details>
	<summary>Enums and Structs</summary>

	Sum and product types.
</details>

<details>
	<summary>Optional, Optional Binding, Unwrapping and Optional Chaining</summary>

	Optional is Swift's powerful feature which come to solve problem of non-existing value. It is just a type.

	Optional Binding: You use optional binding to check if the optional contains a value or not. If it does contain a value, unwrap it and put it into a temporary constant or variable.

	Forced Unwrapping: That means we tell compiler that optionalInt has a value and extract and use it.

	Implicitly Unwrapped Optional : When we are very very sure about it has value after first time it is set, then we need not unwrap every time. So for this type of scenario, we have to use it with `!` mark in their type.

	Optional chaining is the way by which we try to retrieve a values from a chain of optional values. Optional chaining is a process of querying and calling properties. Multiple queries can be chained together, and if any link in the chain is nil then, the entire chain fails.

</details>

## Concurrency

<details>
	<summary>Write different ways to achieve concurrency in iOS?</summary>

	Concurrency means "running multiple tasks simultaneously". Concurrency allows iOS devices to handle background tasks (such as downloading or processing data) while maintaining a responsive user interface. In iOS, you can manage concurrent tasks using Grand Central Dispatch (or GCD), and Operations (formally known as NSOperation). In order to achieve concurrency, iOS provides three ways as follows:

	- Threads: An independent sequence of instructions can be executed separately from other code within a program. Through threads, one can execute multiple code paths simultaneously in a single application. Having a thread is especially useful when you need to perform a lengthy task without affecting the execution of the rest of the program.
	- Dispatch queues: They are used to manage tasks in first-in-first-out (FIFO) order and execute tasks sequentially or concurrently. This is an easy way to handle asynchronous (not occurring at the same time) and concurrent tasks in your application.
	- Operation Queues: Operation queue objects are invoked in accordance with their priority and readiness. Essentially, operation queues are high-level abstractions of queueing models, built on top of GCD (Grand Central Dispatch). It is possible, therefore, to execute tasks concurrently, just like GCD, but in an object-oriented manner.
	- Structured Concurrency
</details>

<details>
	<summary>What is GCD?</summary>

	Grand Central Dispatch (GCD) is a low-level API that enables users to run concurrent tasks (occurring simultaneously) by managing threads in the background. Grand Central Dispatch is Apple's solution to build concurrency and parallelism into iOS applications, so multiple background tasks can be run concurrently in the background without affecting the main thread. It was introduced in iOS 4 to avoid the tedious process of serial execution of tasks.
</details>

<details>
    <summary>How can we bridge a completion handler into an async function in Swift?</summary>

    To write our own async/await functions, Swift provides so called continuations which give us control over suspending and resuming a function. To bridge a completion handler function, we can use Swift's `withCheckedContinuation` function.
</details>

## Combine

<details>
    <summary>What is the difference between a subject and a publisher in Combine??</summary>

    A publisher exposes values of a certain type over time and can be completed or optionally fail with an error. A subject is basically a mutable publisher i.e. it has the ability to send new values after its initialization.
</details>

## SwiftUI

See [Tech Interview Q&A - SwiftUI](Tech Interview Q&A - SwiftUI.md) file.

## Other

<details>
	<summary>What is Deep Link?</summary>

	Deep links are links that send users directly to an app directly instead of a website or store using URI (Uniform resource locator) or universal links. The URL scheme is a well-known method of having deep links, but Universal Links are Apple's new approach to connecting your web page and your app under the same link. Deep linking involves not only creating a clickable link that opens up your app, but also a smart one that navigates to the resource you desire. Users are directed straight to in-app locations using these links, which saves them the time and effort of finding those pages themselves thus improving their user experience tremendously.

	Explanation: If you use the URL fb://, you may open the Facebook app. However, if you use fb://profile/33138223345, you will open Wikipedia's profile in the Facebook app.
</details>

<details>
	<summary>What is ARC?</summary>

	In the Swift programming language, automatic reference counting (ARC) is used to manage apps' memory usage. It initializes and deinitializes system resources, thereby releasing memory reserved by a class instance when it no longer needs it. ARC keeps track of how many properties, constants, and variables currently refer to each class instance. When there is at least one active reference to an instance, ARC will not deallocate that instance. The use of ARC concepts is an essential part of iOS development.

	Functions of ARC -

	- ARC creates a new class instance using init() and allocates a chunk of memory to store the information.
	- Memory stores information about the instance type and its values.
	- As soon as the class instance is no longer required, ARC automatically frees memory by calling deinit().
	- By tracking current referring classes' properties, constants, and variables, ARC ensures that deinit() is only applied to those instances that are unused.
</details>

<details>
	<summary>What is Dynamic Dispatch?</summary>

	In simple terms, dynamic dispatch means that the program decides at runtime which implementation of a particular method or function it needs to invoke. In the case where a subclass overrides a method of its superclass, dynamic dispatch determines whether to invoke the subclass implementation of the method or the parents.
</details>

## UIKit

<details>
    <summary>What is the concept behind intrinsic content size of a UIView??</summary>

    Intrinsic content size represents the amount of space a view needs to display its content. A view can have an intrinsic content height, width or both.

    For example, the intrinsic content size of a UILabel will be the size of the text it contains.

    Not all views have an intrinsic content size. When defining a custom view, we are able to decide if it has an intrinsic content size depending on how we setup the view's constraints.
</details>
