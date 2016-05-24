# MongoLabKit by ustwo
---

### Welcome to MongoLabKit 
[![GitHub license](https://img.shields.io/badge/license-MIT-lightgrey.svg)](https://github.com/ustwo/mongolabkit-swift/blob/master/LICENSE) 
[![Carthage Compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![CocoaPods Compatible](https://img.shields.io/badge/Pods-compatible-4BC51D.svg?style=flat)](https://cocoapods.org)
[![Platforms iOS | watchOS | tvOS](https://img.shields.io/badge/Platforms-iOS%20%7C%20watchOS%20%7C%20tvOS-lightgray.svg?style=flat)](https://developer.apple.com/swift/)

MongoLabKit is a REST client API for iOS, tvOS and watchOS written to make REST calls to a MongoLab database.

---

## Requirements 

- iOS 9.0+ / Mac OS X 10.9+
- Xcode 7.3 / Swift 2.2

## Platform Support

- iOS
- tvOS
- watchOS

## Integration

Platform-specific framework projects are included in the workspace.

``` swift 
import MongoLabKit
```

### Installation with Carthage

[Carthage](https://github.com/Carthage/Carthage) is a decentralized dependency manager that builds your dependencies and provides you with binary frameworks.

You can install Carthage with [Homebrew](http://brew.sh/) using the following command:

``` bash
$ brew update
$ brew install carthage
```

To integrate MongoLabKit into your Xcode project using Carthage, specify it in your `Cartfile`:

``` ogdl
github "ustwo/mongolabkit-swift"
```

Then use platform-specific commands to create the build products that you need to add to your project:

````
carthage update --platform iOS
carthage update --platform tvOS
carthage update --platform watchOS
````

### Installation with CocoaPods

[CocoaPods](http://cocoapods.org) is a dependency manager for swift and Objective-C, which automates and simplifies the process of using 3rd-party libraries like MongoLabKit in your projects. You can install it with the following command:

```bash
$ gem install cocoapods
```

#### Podfile

To integrate MongoLabKit into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
use_frameworks!

target '{TARGET_NAME}' do
    pod 'MongoLabKitSwift'
end
```

Then, run the following command:

```bash
$ pod install
```

---

## Usage

*An example is available [here](https://github.com/ustwo/mongolabkit-swift/blob/master/MongoLabKit/MongoLabKitExamples/ViewController.swift)*

## Usage with service

### Listing collections

``` swift
let configuration = MongoLabConfiguration(baseURL: "{BASE_URL}", apiKey: "{API_KEY}")

let service = CollectionService(configuration: configuration, delegate: self)

service.loadCollections()
```

---

### Listing documents in a collection

``` swift
let configuration = MongoLabConfiguration(baseURL: "{BASE_URL}", apiKey: "{API_KEY}")

let service = DocumentService(configuration: configuration, delegate: self)

service.loadDocumentsForCollection(Collection("{COLLECTION_NAME}"))
```

---

### Adding a document in a collection

``` swift
let configuration = MongoLabConfiguration(baseURL: "{BASE_URL}", apiKey: "{API_KEY}")

let document = Document(payload: {JSON_OBJECT})

let service = DocumentService(configuration: configuration, delegate: self)

service.addDocument(document, inCollection: Collection("{COLLECTION_NAME}"))
```

---

## Usage with custom requests

### Creating a GET request with query string parameters

``` Swift
let configuration = MongoLabConfiguration(baseURL: "{BASE_URL}", apiKey: "{API_KEY}")

let parameter1 = MongoLabURLRequest.RequestParameter(parameter: "{PARAMETER_NAME}", value: "{PARAMETER_VALUE}")
let parameter2 = MongoLabURLRequest.RequestParameter(parameter: "{PARAMETER_NAME}", value: "{PARAMETER_VALUE}")

let request = try MongoLabURLRequest.URLRequestWithConfiguration(configuration, relativeURL: "collections/[COLLECTION_NAME]", method: .GET, parameters: [parameter1, parameter2], bodyData: nil)
```

### Creating a POST request with body data

``` Swift
let configuration = MongoLabConfiguration(baseURL: "{BASE_URL}", apiKey: "{API_KEY}")

let body: [String: AnyObject] = [{PARAMETER_KEY}: [{PARAMETER_KEY}: {PARAMETER_VALUE}]]

let request = try MongoLabURLRequest.URLRequestWithConfiguration(configuration, relativeURL: "collections/[COLLECTION_NAME]", method: .POST, parameters: [], bodyData: body)
```

### Making REST call

``` Swift
let client = MongoLabClient()

client.performRequest(request) {
result in

switch result {
    case let .Success(response):
        print("Success \(response)")
    
    case let .Failure(error):
        print("Error \(error)")
    
    }
}
```

---

## Roadmap

* *DocumentService*: Modify document with id in collection
* *DocumentService*: Delete document with id in collection

---

## Contributing

Do you love the app and want to get involved? Or maybe you've found a bug or 
have a new feature suggestion? Thanks! There are plenty of ways you can help.

Please see the [Contributing to MongoLabKit guide](https://github.com/ustwo/mongolabkit-swift/blob/develop/CONTRIBUTING.md).

---

## Maintainers

* Developer iOS: [Luca Strazzullo](mailto:luca@ustwo.com)

---

## Contact

[open.source@ustwo.com](mailto:open.source@ustwo.com)

---

## License

This is a proof of concept with no guarantee of active maintenance.

See [License](./LICENSE)

