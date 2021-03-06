RestKitMapper
=============

# Overview

RestKitMapper is a wrapper around [RestKit](http://restkit.org), popular Objective-C framework for REST API access. Its primary intention is to hide RestKit configuration complexity and wrap REST API calls in simple and intuitive methods.

# Features

RestKitMapper allows you to configure RestKit mappings declaratively. Supported RestKit features include:
  * Attribute mappings and primary keys
  * Dynamic path-based mappings
  * Full support for relationships
  * Request object mappings
  * Error response mappings

# Getting started

To get started with RestKitMapper you should fully understand RestKit concepts (and, in particular, RestKit mappings). Please read [RestKit docs](https://github.com/RestKit/RestKit/wiki) if you haven't done so yet. Installation is simple:

 * Include RestKitMapper in your Podfile (if you're not yet familar with [CocoaPods](http://cocoapods.org/), that's a good reason to start) and run **pod install**
 * Copy and edit RestKitMapper configuration file (sample file available in RestKitMapper project directory as **Config/RestKitMapper.plist**. Place it anywhere in your project file hierarchy.
 * Include and initialize RestKitMapper and your application

```objective-c
#include <RestKitMapper/RestKitMapper.h>

- (void)initializeRestKitMapperDefaults
{
  [RKMRestKitMapper configureWithFileName:@"RestKitMapperConfig"
                    serverBaseUrl:@"https://my.server:8080"
                    contextUrl:@"/api/v2"
                    modelName:@"MyModelName"];
}

- (void)callMyRestApiMethod
{
  RKMRestKitMapper *restKitMapper = [RKMRestKitMapper sharedInstance];
  [restKitMapper get: @"/relative_api_url" cached: NO withParams: nil success: ^(id result) {
    NSArray *items = result; // result normally contains NSArray of retrieved entities
    // handle results
    self.tableItems = items;
    [self.tableView reloadData];
  } failure:^(NSError *error) {
    // handle error
    NSLog("REST error: %@", error);
  }];
}

```

# More information

  * [RestKit API documentation](http://restkit.org/api/latest/)
  * [RestKit wiki](https://github.com/RestKit/RestKit/wiki)
  * [RestKitMapper configuration file syntax](https://github.com/xfyre/RestKitMapper/wiki/RestKitMapperConfig)
  * RestKitMapper API documentation (TODO)

# Author

Ilya Obshadko
