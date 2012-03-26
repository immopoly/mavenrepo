# our very own maven repo

## about
This is a maven repo for all artifcats we use but where's no or no current version in the public maven repositories.

We created this repository following [this blog post](http://coffeecoders.de/2011/09/using-github-as-a-personal-maven-repository/) by our team member [stefanhoth](https://github.com/stefanhoth).

## What's in the box?

- [Analytics SDK for Android](http://code.google.com/apis/analytics/docs/mobile/download.html): The SDK enables you to track usage of your app just as if it were a website. First, identify the places in your app where you'd like to trigger a pageview or an event, then use the SDK to send these events to Google Analytics.
 - versions: **1.3.1**, **1.4.2**
- [android-support-v4-googlemaps](https://github.com/petedoyle/android-support-v4-googlemaps#readme): A port of the Android Compatibility package which makes FragmentActivity extend MapActivity. This is a hack to make it possible to use a MapView in a Fragment.
 - versions: **r3** ([original by Google](http://developer.android.com/sdk/compatibility-library.html)), **r6-petedoyle** (patched version)
- [JSON-Java](https://github.com/stefanhoth/JSON-java#readme): A reference implementation of a JSON package in Java.
 - versions: **20111006**

More to come if needed.

## How to use this?

There are two ways to make maven aware of new repositories besides the pre-configured one. Either in `~/.m2/repositories/settings.xml` which would be global for every repository but just for your user account. Or you can add the information into the `pom.xml` of your project. Since we want all developers for this project to easily use the new repository we will use the later.

Open your `pom.xml` and add the following lines for our example. Of course you have to edit the group-id, artifact and version according to your lib.

	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	    <modelversion>4.0.0</modelversion>
	    <!-- ... more project definition -->
	 
	    <dependencies>
	 
	        <dependency>
			<groupid>org.json</groupid>
			<artifactid>json</artifactid>
			<version>20111006</version>
	        </dependency>
	        <!-- more dependecies... -->
	    </dependencies>
	 
	    <!-- build config etc. ... -->
	 
	    <repositories>
			<repository>
				<id>immopoly-snapshots</id>
				<url>https://raw.github.com/immopoly/mavenrepo/master/snapshots</url>
				<releases>
					<enabled>false</enabled>
					<updatepolicy>always</updatepolicy>
					<checksumpolicy>warn</checksumpolicy>
				</releases>
				<snapshots>
					<enabled>true</enabled>
					<updatepolicy>never</updatepolicy>
					<checksumpolicy>fail</checksumpolicy>
				</snapshots>
			</repository>
			<repository>
				<id>immopoly-releases</id>
				<url>https://raw.github.com/immopoly/mavenrepo/master/releases</url>
				<releases>
					<enabled>true</enabled>
					<updatepolicy>always</updatepolicy>
					<checksumpolicy>fail</checksumpolicy>
				</releases>
				<snapshots>
					<enabled>false</enabled>
					<updatepolicy>always</updatepolicy>
					<checksumpolicy>warn</checksumpolicy>
				</snapshots>
			</repository>

			<!-- more repositories -->

		</repositories>
	</project>
