---
title: 'Omniture API: Pulling Campaign Tracking Code Click-Throughs programatically'
author: jbeckham
layout: post
date: 2012-04-10
url: /2012/04/omniture-api-pulling-campaign-tracking-code-click-throughs-programatically/
categories:
  - Dev
---
This is the process I used to pull campaign tracking code click throughs programatically through the Omniture Reporting API. While you can start with code, I found it to be much more productive to use Omniture&#8217;s <a href="https://developer.omniture.com/en_US/get-started/api-explorer" target="_blank">API Explorer</a> to figure out exactly what I wanted first. The API Explorer is nice because it shows you the available methods  with their parameters and gives you immediate feedback as to whether it worked or not. The first section below goes through the API Explorer. The second half contains the code I wrote and is specific to C# and Visual Studio 2010.

&nbsp;

## Access to the API

First, you need <a href="https://developer.omniture.com/en_US/content_page/enterprise-api/c-get-web-service-access-to-the-enterprise-api" target="_blank">web service access</a> to Omniture. This creates a Share Secret key which is used _instead_ of your password when making API calls. The username passed to the API is a combination of your company and your Omniture username: <username>:<company>.  Your username and shared key should look something like this:

  * **Username:** jdoe:Company
  * **Shared Secret:** 728275238473afe875ae398fea323ad3

&nbsp;

## API Explorer

You&#8217;ll want to verify that your username and shared secret actually work. The best way to do that is with the <a href="https://developer.omniture.com/en_US/get-started/api-explorer" target="_blank">API Explorer</a>. Enter your username and shared secret in the first section.

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="2012-04-10_142911" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_142911_thumb1.png?resize=293%2C129" alt="2012-04-10_142911" border="0" data-recalc-dims="1" />][1]

In the next section, choose &#8220;Company&#8221; for the API and &#8220;GetTokenCount&#8221; for the Method. This is a great Method to start with because it doesn&#8217;t require any parameters. Click &#8220;Get Response&#8221;.

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="2012-04-10_143825" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_143825_thumb.png?resize=581%2C473" alt="2012-04-10_143825" border="0" data-recalc-dims="1" />][2]

The response shows up in a box below. If there are any problems, the error will appear here. If all is well, you&#8217;ll see the data you requested. In this case, we asked for the Token Count and got back 9978. Omniture gives you an allotment of API tokens. Each call you make (regardless of the response size) consumes 1 token.

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="2012-04-10_143320" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_143320_thumb.png?resize=575%2C97" alt="2012-04-10_143320" border="0" data-recalc-dims="1" />][3]

Now that we know that we can successfully access the API, the next step is figuring out the API calls you want to use and the parameters that they take. In my case, I wanted to get a Ranked Report containing the number of Click-throughs for each Campaign Tracking Code. The <a href="https://developer.omniture.com/en_US/documentation/sitecatalyst-reporting/c-overview-6" target="_blank">Report API documentation</a> explains most of the parameter fields and options. I selected &#8220;Report&#8221; for the API, and &#8220;GetRankedReport&#8221; for the Method. This populates the parameter section with a template for all possible options (it can be a bit overwhelming, but fortunately, you don&#8217;t need most of it most of the time).

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="2012-04-10_144729" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_144729_thumb.png?resize=572%2C435" alt="2012-04-10_144729" border="0" data-recalc-dims="1" />][4]

After quite a bit of trial and error, I ended up with this:

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="2012-04-10_145725" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_145725_thumb1.png?resize=578%2C470" alt="2012-04-10_145725" border="0" data-recalc-dims="1" />][5]

Which results in this response:
  
[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="2012-04-10_150038" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_150038_thumb.png?resize=582%2C375" alt="2012-04-10_150038" border="0" data-recalc-dims="1" />][6]

Once you figure out how to pull the data you need through the API explorer, it&#8217;s time to move on to the code.

&nbsp;

## The Code (Visual Studio 2010 specific)

Omniture has created guides for a number of different platforms. You can search for them on the <a href="https://developer.omniture.com/" target="_blank">Omniture Developer Connection</a>. In my case, I&#8217;m building the project in Visual Studio 2010, which has a <a href="https://developer.omniture.com/en_US/blog/getting-started-with-the-omniture-apis-using-visual-studio-2010-wcf" target="_blank">guide</a> and some <a href="https://developer.omniture.com/en_US/gallery/using-the-apis-with-wcf-dlls" target="_blank">libraries</a> that Omniture created. I followed steps 1-4 of the guide to get started as they are. Their API client class follows the request structure you used in the API Explorer pretty closely. You need to create a _reportDescription_ object within which you will put the parameters you need.

I decided to create an Extension method to populate the _reportDescription_ object for me. Here it is:

<pre class="lang:c# decode:true">public static class reportDescriptionExtensions
{
    public static reportDescription PopulateWith(this reportDescription reportDescription, string reportSuite, string startDate, string endDate, string filter, int top, int startingWith)
    {
        reportDescription.reportSuiteID = reportSuite;
        reportDescription.dateFrom = startDate;
        reportDescription.dateTo = endDate;
        reportDescription.metrics = new reportDefinitionMetric[]
            {
                new reportDefinitionMetric() { id = "instances" }
            };
        reportDescription.elements = new reportDefinitionElement[]
            {
                new reportDefinitionElement()
                {
                    id = "trackingCode",
                    search = new reportDefinitionSearch()
                    {
                        type = reportDefinitionSearchType.and,
                        keywords = new string[] { filter }
                    },
                    top = top,
                    startingWith = startingWith,
                }
            };

        return reportDescription;
    }
}</pre>

&nbsp;

Note that the _reportDescription_ object is created outside of this method and is passed in. I&#8217;ve both hardcoded some of the values and passed in others as arguments. I ended up adding in a few extra parameters that I didn&#8217;t have in the API Explorer example above: I added a search and split the results into pages (_top_ & _startWith_). Note how the values and structure here are pretty close to what we had in the API Explorer.

Here is the client I created to pull down the report and convert it to my own reporting format. I&#8217;ll break each section down below.

<pre class="lang:c# decode:true">public class SiteCatalystClient
{
    private string url;
    private string username;
    private string password;
    private int top;

    public SiteCatalystClient(string url, string username, string password)
    {
        this.url = url;
        this.username = username;
        this.password = password;
        top = 10000;
    }

    public ClickthroughReport GetClickThroughsReport(string reportSuite, string filter, string startDate, string endDate)
    {
        using (var client = OmnitureWebServicePortTypeClient.getClient(username, password, url))
        {
            ((CustomBinding)client.Endpoint.Binding).Elements.Find&lt;TransportBindingElement&gt;().MaxReceivedMessageSize = int.MaxValue;
            var startingWith = 0;
            var report = new ClickthroughReport();
            var executionCount = 0;

            do
            {
                var trackingCodeReportDescription = new reportDescription().PopulateWith(reportSuite, startDate, endDate, filter, top, startingWith);
                var reportResponse = client.ReportGetRankedReport(trackingCodeReportDescription);

                foreach (var dataPoint in reportResponse.report.data)
                {
                    report.AddRecord(new ClickthroughReportRecord()
                    {
                        Name = dataPoint.name,
                        ClickThroughs = (int)dataPoint.counts[0]
                    });
                }

                startingWith += top;

                if (reportResponse.report.data.Count() &lt; top) break;
            } while (++executionCount &lt; 10);

            return report;
        }
    }
}</pre>

&nbsp;
  
Let&#8217;s break this down. The constructor takes the API _url_ ([https://api.omniture.com/admin/1.3/][7]), _username_ (the combined username from above), and _password_ (shared secret). I also set _top_ to the number of records I want to fetch each time.

<div id="codeSnippetWrapper">
  <pre class="lang:default decode:true">public SiteCatalystClient(string url, string username, string password)
{
    this.url = url;
    this.username = username;
    this.password = password;
    top = 10000;
}</pre>
  
  <p>
    &nbsp;
  </p>
</div>

The only method that this class has at this time is to pull the Compaign Tracking code click-throughs. It takes the _reportSuite_, filter (filters on the actual tracking code to narrow the results down), and _startDate_ and _endDate_. It returns a _ClickthroughReport_ object which is my own object I use elsewhere in my project.

<div id="codeSnippetWrapper">
  <pre class="lang:default decode:true">public ClickthroughReport GetClickThroughsReport(string reportSuite, string filter, string startDate, string endDate)</pre>
  
  <p>
    &nbsp;
  </p>
</div>

Next I instantiate the client that Omniture provided in the library we downloaded earlier, then I overrode the _MaxReceivedMessageSize_ to the largest possible value. This sets how large the messages can be coming back from Omniture. The messages for my reports were quite large, so I just set this limit as high as it could go.

<div>
  <pre class="lang:c# decode:true">using (var client = OmnitureWebServicePortTypeClient.getClient(username, password, url))
{
    ((CustomBinding)client.Endpoint.Binding).Elements.Find&lt;TransportBindingElement&gt;().MaxReceivedMessageSize = int.MaxValue;</pre>
  
  <p>
    &nbsp;
  </p>
</div>

<div>
</div>

<div>
  Then I set starting values for <em>startingWith</em> and <em>executionCount</em> and create my <em>ClickthroughReport</em> object which I will return from this method.
</div>

<div>
</div>

<div id="codeSnippetWrapper">
  <pre class="lang:c# decode:true">var startingWith = 0;
var report = new ClickthroughReport();
var executionCount = 0;</pre>
  
  <p>
    &nbsp;
  </p>
</div>

&nbsp;

We go into a do while loop. Our result set is paged, so each time through the loop pulls the next range of data. I have it limited to 10 loops though because I don&#8217;t want this report to run for too long.

<pre class="lang:default decode:true">do
{
    ///.....
} while (++executionCount &lt; 10);</pre>

&nbsp;

I create the _reportDescription_ object (this was provided in the Omniture library) and populate it with my extension method, _PopulateWith_, that I showed above.

<div id="codeSnippetWrapper">
  <pre class="lang:c# decode:true">var trackingCodeReportDescription = new reportDescription().PopulateWith(reportSuite, startDate, endDate, filter, top, startingWith);</pre>
</div>

<div>
</div>

<div>
  Now we finally get to the actual API call. We give it the <em>reportDescription</em> object we just created.
</div>

<div>
</div>

<div id="codeSnippetWrapper">
  <pre class="lang:default decode:true">var reportResponse = client.ReportGetRankedReport(trackingCodeReportDescription);</pre>
</div>

The _reportResponse_ object contains a property called _report_ which contains a property called _data_. _Data_ is an array with the values we want. I loop through each item and place it in to my own report record object:

<div>
  <pre class="lang:default decode:true">foreach (var dataPoint in reportResponse.report.data)
{
    report.AddRecord(new ClickthroughReportRecord()
    {
        Name = dataPoint.name,
        ClickThroughs = (int)dataPoint.counts[0]
    });
}</pre>
</div>

<div>
</div>

<div>
</div>

<div>
  The last little bit is to increment the record we&#8217;ll start with next time and break out of the loop if we&#8217;re at the end of the result set.
</div>

<div>
</div>

<div id="codeSnippetWrapper">
  <pre style="text-align: left; line-height: 12pt; background-color: #f4f4f4; margin: 0em; width: 100%; font-family: 'Courier New', courier, monospace; direction: ltr; color: black; font-size: 8pt; overflow: visible; border-style: none; padding: 0px;" id="codeSnippet">startingWith += top;

<span style="color: #0000ff;">if</span> (reportResponse.report.data.Count() &lt; top) <span style="color: #0000ff;">break</span>;</pre>
</div>

<div>
  I return my report object which is essentially just a list of campaign codes with their corresponding click-through values.
</div>

 [1]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_1429111.png
 [2]: http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_143825.png
 [3]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_143320.png
 [4]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_144729.png
 [5]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_1457251.png
 [6]: http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/04/2012-04-10_150038.png
 [7]: https://api.omniture.com/admin/1.3/ "https://api.omniture.com/admin/1.3/"