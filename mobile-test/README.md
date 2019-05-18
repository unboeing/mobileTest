# Instructions:

- Fork this git repo to your computer
- Create a branch
- When you are done, push your work and create a pull request to the original repo.

# Requirements

*Create a 3 page app.*

- When you launch the app, you should see a list of resource categories (`/data/categories.json`)
- When you click on a category, it should open a list of resources (`/data/restaurant.json` or `/data/vacation-spot.json`)
- When you click on a resource, it should open a details page (see attached mockup)

# Tips:

- You can showcase usage of Dependency Injection and Architecture Component.
- You can show how to handle threads.
- Remember you can always create a side project first and prepare yourself before jumping into the test.
- For JSON, you can use the RAW file version in git hub so you can simulate a call to remote API.

# User Stories

| 1  | As a user, I want to see a list of categories
- need uitableview -> data source -> .json with categories
- need Category :Decodable struct to represent each category - properties - id: String, updatedAt: Date, slug: String, customModuleEid: String, eid: String, title: String, description: String, _v: Int, active: Bool, createdAt: Date
- uitableviewcells to view each category - need model and custom controller

| The list items must link to the resources page                                  |
- “Resources” UIButton in each Category UITableViewCell, with its respective view model 


| 2  | As a user, I want to see the resources inside a category
- new UIViewController containing UITableView of either restaurants or vacationSpots, both resources in same .json file
- need Resource :Decodable struct to represent each .json entry - properties - id: String, slug: String, eid: String, title: String, description: String, bizHours: [BusinessHours]?,  categoryEid: String, _v: Int, photoURL: NSURL, active: Bool, updatedAt: Date, createdAt: Date, addresses: [Address]?, contactInfo: ContactInfo?, socialMedia: SocialMedia? - read tutorial for :Decodable protocol
- need BusinessHours enum inside Resource struct - read about Enums
- need Address :Decodable struct - properties: addressNumber: String, label: String, zipCode: String, city: String, state: String, country: String, gps: (String: String, String: String)  
- need ContactInfo :Decodable struct - properties: website: NSURL, email: String, phoneNumber: String, faxNumber: String?, tollFree: String?, freeText: String?
- need SocialMedia :Decodable struct - properties: youtubeChannel: NSURL?, twitter: NSURL?, facebook: NSURL? 
- each Resource object will be displayed in a UITableViewCell containing various sections for object properties; in the case of bizHours, contactInfo and addresses, the sections will be UITableViews themselves, with scrolling disabled and custom UITableViewCells

| The list items must link to the details page                                    |
- “Details” UIButton in each UITableViewCell


| 3  | As a user, I want to see the details of a category  
- 3rd new UIViewController containing a UITextView for the description
- segues from the initial view upon the user tapping on the "Details" UIButton of one of the custom UITableViewCells for each category
- at segue the relevant details are passed in String format onto this DetailsView's view model(?) or viewController class for easy display (maybe possibilities/requirements for HTML parsing)
- also must contain “Dismiss” button, probably default with overarching UINavigationController

| The description is HTML, but the what you see on the screen must be text        |
- contains a UITextView Properly formatted with the description of the category, accessible from the initial view's category UITableViewCells 

| 4  | As a user, I want to sort the list of resources alphabetically
- “Sort” UIButton. Assuming it’s the “Search” button from mockup

| When I tap on the sort button, the list should sort from A-Z                    |
- implies the table view displays the data in the original order initially
- ResourcesUIViewController should contain sorted: Bool = false


| 5  | When I tap on it a second time, it should sort the list from Z-A  
- ResourceUIViewController should contain sortedUp: Bool? = nil, also change above to sorted: bool = false { didSet {sortedUp = true} } 

| As a user, I want to send an email by tapping on a resource email               |
- create sendEmail UIButton inside email UITableViewCell in the contactInfo section of Resource UITableViewCell


| 6  | It should open the email without leaving the app  
- need new UIView for email composition, with its own viewmodel/class which animates from the right in the same view by the user tapping sendEmail Button described above
- this EmailUIView viewmodel/class will have a UITextField for the adresee, a UITextField for the Subject, a UITextField for any CC:, a UITextView for the message, a "Send" UIButton, a "Save as Draft" UIButton, a "Cancel" UIButton 

| As a user, I want to call one of the phone numbers on the resource details page |
- create callNumber UIButton inside each UITableViewCell of the contactInfo section of Resource UITableViewCell that is displaying a phone number
- create associate callNumberTapped(sender: UIButton) @IBAction inside the corersponding viewmodel of a Resource UITableViewCell that is displaying a phone number


| 7  | As a user, I want to open the maps app on my phone when I tap on a resource address  
- need to make Address UITableViewCell of the addresses section of Resource UITableViewCell open the Maps App at the displayed address 
- each Address UITableViewCell's viewmodel will be an Address struct obtained and modeled as described at User Story #2


| 8  | As a user, I want to open a web link without leaving the app 
- need new UIView to display a WKWebView and the necessary controls for web browsing: an address bar?, a Back UIButton?, a Forward UIButton?, a Dismiss UIButton

| It should open a web browser without leaving the app                            |
- since the app requres only 3 pages, we have to bring another UIView from offscreen to display the web browser described above, achievable with constraint @IBOutlets and AutoLayout in the ResourcesUIViewController, overlaid on top of the ResourcesUITableView and disabling the normal functinos of ResourcesUIViewController, regainable at dismissWebBrowserTapped(sender: UIButton) @IBAction 


| 9  | As a user, I want to see a resource image     
- have photoURL displayed in a UIImageView inside its Resource UITableViewCell, above Title UITextField
- updatable from an URL, it provides a good spot for threading


| 10 | As a user, I want to see a resource description         
- have description displayed in a UITextView with scrolling disabled below addresses section in each Resource UITableViewCell


# Mockup:

Use the following mockup as a UI guide for your app (the image is at the root of the project). This mockup contains more details that you actually will need in this test. Please use with intepretation. We do not provide you with any specs, so please use your imagination while trying to respect the mockup as much as you can.

![Mockup](https://github.com/quickseries/mobile-test/blob/master/resources_android.png "Mockup")
