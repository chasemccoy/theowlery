---
title: Form Validation with Swift Protocol Extensions
---

If you develop iOS apps I am pretty sure you have needed to validate an input form at some point. It’s a pretty common use case that can lead to a lot of repeated code in the wrong places.

I am currently working on an app that has several input forms and I needed to find a better way to validate the inputs without repeating validation code anywhere. Of course, like they usually do, Swift’s protocols came to the rescue.

In addition, you will probably want a way to let the user know why their input is invalid, so I start by declaring an enum that has two cases: `Valid` and `Invalid`. The `Invalid` case has an associated string value that will store the error message.

```swift
enum ValidationResult {
  case Valid
  case Invalid(String)
}
```

Next, create a protocol for each type of input that you need to validate (email, password, user name, etc.). The key here is that since we don’t want to rewrite code, we will declare the functions that actually validate the input inside of a protocol extension.

Methods declared inside of protocol extensions have implementations that are available to all types that conform to that protocol. Here I created a protocol called `ValidatesPassword` and inside of an extension I wrote an `isPasswordValid` method. This method accepts the password as a string and returns one of our `ValidationResult` cases.

```swift
protocol ValidatesPassword {}
extension ValidatesPassword {
  func isPasswordValid(password: String?) -> ValidationResult {
    guard let password = password
      else { return .Invalid("Password field is empty.") }
    
    guard password.characters.count > 7
      else { return .Invalid("Password must be at least 8 characters long.") }
    
    return .Valid
  }
}
```

You can see that whenever we find an invalid password, we return `.Invalid` with our error string associated. Guards make it really easy to cascade validation requirements and exit the function without evaluating unnecessary conditions. If all of the conditions are met, we return `.Valid`.

One we have created all of our validating protocols, we can simply create a struct that conforms to the ones we need and validates any input field in our app.

One neat trick here is that if you have an input form with a lot of fields, it can become messy to conform to all of those protocols. Instead, create a typealias for the ones you need and then just conform to that one:

```swift
typealias ValidatesRegistrationForm = protocol<ValidatesName, ValidatesEmail, ValidatesAge, ValidatesZipCode, ValidatesPassword>
```

In the app I am currently writing, I created a struct that gets initialized with all of my `UITextField`s and then validates each field one by one. It simply switches on the result and handles the cases appropriately. 

When the user hits the “Submit” button, the view controller creates an instance of the validator and calls the validate function. I also pass in a completion handler that accepts and displays an alert controller. That way, if a validation step fails, the validator can create a `UIAlertController` with the error message and pass this into the callback to display it to the user. 

What is great about this message is that if our validation conditions ever change, we simply have to update our validation function in one place and then every form in our app will validate correctly.

Hope this helps! If you have any questions or comments (or suggestions for making this better) please send me a tweet [@chase_mccoy](http://twitter.com/chase_mccoy). 
