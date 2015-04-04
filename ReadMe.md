##2013.10.16 update
* Compatible with new API(new attributes, landmarks etc.) 

##2.0 update
* Compatible with 2.0 API
* Modify the initialize function to change region between CN and US 
	- Example: `[FaceppAPI initWithApiKey: @"YOUR_KEY" andApiSecret: @"YOUR_SECRET" andRegion: API_SERVER_REGION]`

------------------------------------------------------
##To integrate FacePlusPlus SDK into your iOS project

1. In the finder, drag FaceppSDK into project's file folder.

2. Add it to your project: 
	- File -> Add Files to "your project"
	- Choose 'Recursively create groups for any added folders'

3. In xcodeproj -> Build Settings, set **"Objective-C Automatic Reference Counting"** to **NO**
	- If you want to use automatic reference counting, you can use "FaceppSDK_ARC" instead of "FaceppSDK" which in step 1&2.

4. In your Application Delegate:
	- Import FaceppAPI
	- Add: `[FaceppAPI initWithApiKey: @"YOUR_KEY" andApiSecret: @"YOUR_SECRET"]`
	- Sample code:
	<pre><code>\#import "FaceppAPI.h"
	\- (BOOL)application:(UIApplication \*)application didFinishLaunchingWithOptions:(NSDictionary \*)launchOptions {
		[FaceppAPI initWithApiKey:API_KEY andApiSecret:API_SECRET];
		...
	}</code></pre>

5. Call FaceppAPI to do anything you want, it will return a struct called `FaceppResult`
	- Examples: 
	<pre><code>FaceppResult\* result = [[FaceppAPI detection] detectWithURL:nil 
							imageData:[NSData dataWithContentsOfFile:@"LOCAL_FILE_PATH"]];
FaceppResult\* result = [[FaceppAPI group] deleteWithGroupName: @"GROUP_NAME" orGroupId: nil];</code></pre>
6. Get value from FaceppResult
	- Examples:
		- Get image's width in pixel from a detection result - `detectLocalFileResult`:
	<pre><code>double img_width = [[detectLocalFileResult content][@"img_width"] doubleValue];</code></pre>
		- Get the first face_id from result:
			<pre><code>NSString \*face_id = [detectLocalFileResult content][@"face"][0][@"face_id"];</code></pre>

7. Optional: enable debug mode	
	- Set debug mode on to display all http request packages and response raw JSON result on console output.
		<pre><code>[FaceppAPI setDebugMode: TRUE];</code></pre>

-- More sample codes would be found in "FaceppDemo" --
