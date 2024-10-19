
# Building Blocks of Great Design
#### Apple Event - 18th October 2024 - Anikey Roy (Design Evangelist @ Apple)
----

## Introduction
* As long as you have basic building blocks figured out, you can build anything.
* We are exposed to various UI & interactions in our day-to-day app consumption, and we should take notes of what these apps do well and what we can take away from them.

-- One thing that you should remember while building apps is that the users expect your app to be consistent with Apple's Design language and system.


## What are the aspects of a great design?

- Being able to understand the design standards and aspects for the specific platforms that you're developing the app for.

- An understanding of the Human Interface Guildelines (https://developer.apple.com/design/human-interface-guidelines) for specific platforms.

-   A clear organisation of content with a logical structure and easy-to-access User-Interface.


### #1 Standard UI Elements

-   Standard controls behave as users expect, providing a consistent experience across different apps, which leads to higher user satisfaction.

- These elements provide a polished appearance that aligns with user expectations and gives your app a sense of credibility and trustworthiness.

- These standard UI Elements that Apple provides go through lots of development/design iterations and usually handle all the edge cases and requirements thus it's recommended to use these elements for efficient and consistent development.


### #2 Terminology

- The users should know what a particular UI element in your application does without even interacting with it.

- One reminder that you should always keep in mind is that the tech can be intimidating. You should always keep the target audience in mind while developing the User-Interface.

-- Consistent terminology helps ensure a cohesive look and feel across all parts of the app. 


### #3 Icons

- Icons should be simple and easy to recognize at a glance. Overly detailed or abstract icons can confuse users. Stick to icons that users are familiar with i.e. **SFSymbols** (https://developer.apple.com/sf-symbols/)

- **SFSymbols** have over **6000+** icons that you can and should use in your apps. These icons are consistent, balanced, and harmonious, and are used throughout all the apps published by Apple.

- These symbols come with various weights and styles, and you can easily animate layers or the whole symbol using the .symbolEffect modifier in SwiftUI.


### #4 Text Styles

- Text Styles drive the readability of your app's interface. It can make or break the experience of the users.

- With the correct usage of text styles, you can invoke a strong sense of trust/reliability when the users open your app for the first time.

-    Clear distinctions between various texts used between the app reduce confusion.


#### Text Hierarchy

- Clubbing related UI together and differentiating between the UI elements by modifying the Font-Weight, Font-Style, and colors.

-  Helps the users to quickly identify the most important information. Larger, bold headers grab attention first, while smaller body text provides details.

-- You should try to use the native fonts San Francisco (https://developer.apple.com/fonts/) to ensure consistent, scalable, and legible font throughout the platforms.


## Design Paradigms

### #1 Page Layout

-   A well-structured Page layout helps the users to navigate content easily, guiding them to the most important information or actions without any issues.

- You should have a good understanding of the purpose of the app & then understand the intent of the users.

- The User-Interface that you develop should never cause Analysis Paralysis to the users. 


### #2 Search
- A dedicated Search in the tab bar is usually better for placements. It lets the user explore their Heart's content without losing the context of whatever they were doing on the other pages.

- Let's take an ideal Search Functionality for a Travel app
     
     - A Last View Section (Helps the user to quickly jump back into a particular destination/location they were looking for)
     
     - Recent Search ( Helps the user to search for something without typing) 
     
     - Popular Destinations / Packages etc.
    
     -- You should also provide autocomplete, suggestions as the user is typing to help them find the thing that they're looking for with ease.


### #3 Modals

* Modals are used to present information on top of the existing User-Interface so that they can perform any critical/vital actions and then close it without losing context.
 
* They simplify complex workflows by guiding users through necessary steps without overwhelming them with too much information at once. 

* Apple Platforms provides various easy-to-use Modals that you can integrate within your apps.

---

-- Whenever you're designing iOS Apps you should keep the **Pareto Principle** in mind.

> Also known as the 80/20 rule, is the observation that 80% of outcomes are a result of 20% of causes.

* Identify the 20% of features that will deliver 80% of the value to users.

* Design the User-Interface to highlight the commonly used features, reduce clutter, and simplify the navigation.


--- 
One last thing you should remember is to design the user interfaces of your apps in ways the users are most familiar with, that's the key to success.

---


That's it guys, it was a great session and I couldn't show you some of the amazing User-Interface iterations Aniket showed us but it was great.

I'll see if I can incorporate that and these learnings in a Tutorial. See ya next time. :D

 
      
