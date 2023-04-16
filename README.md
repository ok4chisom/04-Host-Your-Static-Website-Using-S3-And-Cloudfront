<h1>Hosting Your Static Website Using S3 and Cloudfront</h1>
<!--
 ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)
--!>
<h2>Description</h2>
A new startup business in North America has recruited you to help with the launch of a quick-access, low-cost static website. You've decided to complete this contract by hosting and deploying their website utilizing AWS S3
<br />

<b>Cloud Front is a content delivery network that allows to you distribute your content (in this case a website) to edge locations around the world. This reduces the latency when requests are made by users globally


<h2>Solution Overview</h2>

- <b>Create CloudFront Distribution
- Edit S3 bucket policy to allow CloudFront access
- Create SSL certificate
- Customize domain name
- Create A record for custom domain

<h2>Detailed Steps:</h2>

<p align="center">

Please complete this project before continuing "[Hosting A Static Website With AWS S3](https://github.com/ok4chisom/01-Hosting-A-Static-Website-on-S3)"


First test the latency of your website by pasting the domain into this url: https://tools.keycdn.com/performance: <br/>
<img src="https://i.imgur.com/L7ez2kG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Navigate to Cloudfront and select "Create Distribution"

Under "Origin" select the S3 bucket hosting your website

You will get a get prompted to "Use website endpoint" since your bucket is hosting a static website. Do not select  it. This will be useful when we want to enable origin access identity (OAI):  <br/>
<img src="https://i.imgur.com/s1rZh00.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Under "Origin access" select "Origin access control"
- Select "create control setting", keep defaults and select "create"
- Select "Yes, update the bucket policy"
<img src="https://i.imgur.com/S7nQ5RT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Under "Viewer" select "Redirect HTTP to HTTPS" and  "GET,HEAD"
- This ensures that viewers are viewing the content from a secure layer
- Users are only view the content
<img src="https://i.imgur.com/xBOabH0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Under "Cache Key and origin requests" select "Cach policy and origin request policy" and "CachingOptimized":  <br/>
<img src="https://i.imgur.com/SZqFka1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Under settings select "Use all edge locations" <br/>
<img src="https://i.imgur.com/FKNMaji.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Select "Create Distribution" <br/>


Copy the S3 policy statement provided by CloudFront for your S3 bucket <br/>
- This gives CloudFront read access to your S3 bucket
<img src="https://i.imgur.com/JPjyski.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Navigate to your S3 bucket and block all public access under "permissions" <br/>
- This is so that the website can only be access via cloudfront

Replace your bucket policy with the copied policy. Similar to below <br/>
<img src="https://i.imgur.com/QlwiFdJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Test that CloudFront is now distributing your website by copying the distribution ARN with/index.html and the website should populate. <br/>

Now Create SSL Certificate by going to AWS Certificate Manager and selecting "Request" <br/>
- This ensure that your website is encrypted

Select Next. Type your domain name, Email verification and RSA 2048. Then select "Request" <br/>

Once you have validated it from your email you will have access to the SSL certificate <br/>

Create custom domain name by navigating back to your CloudFront Distribution <br/>

On the "General" tab, choose "Edit". <br/>

Add your custom domain name <br/>

Select your SSL certificate

Specify "Default root object" as "index.html"
- So that you don't always have to specify the file to access

Navigate to Rout 53 to create a new A record that points to the CloudFront distribution

Name your record. Ensure it is the same name as your custom domain name

Select "A" as Record type and toggle "Alias" on

Select "Alias to CloudFront distribution", leave the "Simple routing" policy and select "Create Record"

Now test that your domain name is working and secure on your browser <br/>
<img src="https://i.imgur.com/yTyuNEs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Finally now test latency of your website again <br/>
- Test 1 - Notice the latency is similar to what we had in the beginning
    <img src="https://i.imgur.com/PUXb2y0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
- Test 2 - Now notice that the latency is much lower meaning that our CloudFront distribution is working
    <img src="https://i.imgur.com/SYXSo2c.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
    <br />
    <br />


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>