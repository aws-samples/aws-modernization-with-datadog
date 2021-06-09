+++
title = "4.2.3 Implementing Synthetics"
chapter = false
weight = 40
+++


Now try looking at Synthetic Tests. RUM waits for real users to experience the product, but Synthetic Tests visit the site from different locations  around the world at regular intervals to simulate what a real user might experience.  You can define a flow around the app and even test the APIs that you use in the app. 
![frontend synthetics](/images/dd-frontend-synthetics.png)


To try this section, you must be using Google Chrome. Other browsers are not supported when recording a test.

1.  Navigate to the Synthetic Tests page on Datadog: https://app.datadoghq.com/synthetics/tests
2.  Click the **Get Started** button.
3.  Choose **New Browser Test**.
4.  Paste in the URL of our website. Ensure you set the protocol at the beginning of the URL to http since our site isn't configured to use https.
5.  Name the test **Frontend Synthetics**.
6.  Choose a few locations to test from and set the test frequency. 6 or 12 hours is a good choice. 
7.  Click **Save Details and Record Test** at the bottom.
8.  Our website doesn't allow for being loaded in an iframe, so click the **Open in Popup** button.
9.  Click the **Start Recording** button.
10. Add something to the cart, then go to the cart and click the **Empty Cart** button to ensure we always start the test with an empty cart. Now look around the site. Do a search. Then find something and add it to the cart. 
11. With the shopping cart shown, click the **Assertion** button in Datadog to add an assertion. 
12. Click the **Test an element's content** button and choose the cart's total. The total will populate the assertion's value. Click **Apply**.
13. Scroll down and click **Save & Launch Test**.
14. Within a few seconds you should see some results showing up in the browser. 

You can add other tests you would like to run on a regular basis. Our API for discounts and advertisements is not exposed on this cluster, but if it were, you could test the output of them too. 