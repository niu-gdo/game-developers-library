# Unity Installation
*By Jake Rogers*

(Warning) This guide is primarily tested on a Windows machine (10+). Mac or Linux users may have different

In this section, we will download Unity and some other necessary tools.

## Unity Hub
### Download
Unity Hub is a sort of 'launcher' for Unity. The application will allow you to download and manage multiple versions of Unity.  
It also allows you to create new projects and track existing ones, so you will use this app often to reopen your work!  

[Download Unity Hub](https://unity.com/download)

### Unity ID
In order to use Unity, you will need to make a Unity ID Account and log into it through Unity Hub.

[Create An Account](https://id.unity.com)

### Unity's Licensing

Once your account is made, you may notice that Unity Hub is telling you that you need a license.

In Unity Hub, open the drop down on the top left (next to the profile picture) and select 'manage licenses'. Select 'Add License' and get a personal one.

#### (ℹ) Unity Licenses

To paraphrase, Unity's Personal License permits you to create applications with Unity as long as **your software(s) developed with Unity** gross less than $100,000 in any fiscal year (The time between now and the last twelve months).

The above only qualifies if you are an *individual* using Unity.If you are part of a legal entity or an established, budgeted organization / institution, the rules are different. 

Shold you have the 'problem' of accidentally making over $100k in a fiscal year with your software, you (and your team) will need to upgrade to a Unity Plus or Pro license depending on your financial threshold.

[Unity's Terms of Service](https://unity.com/legal/editor-terms-of-service/software) **should be well-understood before creating a commercial product with the software**. If in doubt, don't trust what I say, trust their terms of service!

### (Optional) Create an Organization
At this point, you can also create a Unity 'Organization'. Organizations allow you to make use of some special Unity project *services*, such as advertising features or integrated source control like **Plastic SCM**.

It is perfectly fine to make an organization with just you in it. In fact, one was created under the same name as your username when your first made a Unity ID. However, you can make a new org if you would like its name to be different from your Unity username, such as *Jamie Doe Studios* or *Elder Oak Games*.

To do so, click on the drop down in the top left of Unity Hub, and select 'Manage Organizations'. Add a new one from the webpage it brings you to.

## Install A Unity Editor
Once you are signed in on Unity Hub and have acquired the appropriate license, you must install a version of Unity that you would like to use.

Before continuing, **consider changing your *installs location* in Unity Hub's preferences section**. Preferably, change it somewhere on the fastest drive your system has, as this will substantially help your editor load faster.

In Unity Hub, go to 'Installs', then select 'Install Editor'.

Pick the version Unity Recommends, likely one tagged 'LTS', or 'Long Term Support'.

### Installation Modules
When installing a version of Unity, you will get the option of adding some additional modules.  

Most importantly, **you should select the provided version of *Microsoft's Visual Studio Community***. It is a very popular, free IDE for Unity which comes with some nicely integrated bells and whistles. This series and most other guides written by me will use it.

Furthermore, you can also download build support packages which will give you the ability to build your final product on various platforms.

These modules can be added to your installation later, so for now, just pick the support module for the platform you are developing on (Windows, Mac, Linux)

#### (Optional) Visual Studio Workloads
If you decided to install Visual Studio Community, you will eventually be prompted to install some workloads. There is a specific workload for Unity, so pick that! You may also be interested in the *Game Development with C++* workload, which has some features for Unreal Engine.

## Conclusion
Once Unity Hub (and optionally Visual Studio Community) has finished installing, you are ready to move on to the next section! \o/

Next: [Creating a New Project](./unity-first-step-new-proj.md)