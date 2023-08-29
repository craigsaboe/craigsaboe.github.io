Title: Installing Sharp NPM Package On Windows
Date: 2023-08-28 12:00:00
Modified: 2023-08-28 12:00:00
Category: 
Tags: 
Slug: 
Summary:
Status: draft
---

![SharpLogo](images/sharp-node-image-processing/1.png)


Sharp is an npm module that is great for cases when you have a ton of photos that you need to get down to a download-friendly size.

It seems to use OS-specific extensions or libraries, so it is sensitive to the environment you install it using.

To use it successfully on Windows, use the following:

```
npm install --platform=win32 --arch=x64 sharp
```

Now, how this acts when you publish up to a Linux server of some type, I'm not sure, but at least I could run a site using it locally!
