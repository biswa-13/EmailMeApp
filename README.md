# EmailMeApp
Developing Hybriod Mobile Application Part -3 (Adding Compose Email plugIn)

<p><strong>How To Develop Hybrid Mobile App For Sending Emails</strong></p>
<p>Hi friends in my <a href="https://software.intel.com/en-us/forums/android-applications-on-intel-architecture/topic/609918">previous tutorial</a> I have explained how to configure the environment for developing Hybrid Mobile Apps. Now proceeding further I am going to show you how to use available Cordova plugins for achieving your various requirements. Here in my demo I will use a cordova plug-in which is developed for sending the emails and to create the required UI for email composition.</p>
<p>I will demonstrate in step by step and the source codes will be available in my Git Repository for your reference which you can freely download , access and share .</p>
<div><center><strong>Let&rsquo;s Start The Cooking</strong></center></div></p>
<p><strong>While proceeding&nbsp; I hope you must have ready with necessary software&rsquo;s and environment setups.</strong></p>
<div><center><strong>Step 1 : Create a New Cordova App</strong></center></div>
<p><strong>1.1 &ndash; </strong><strong>Create&nbsp; a Fresh Cordova Project</strong></p>
<ul>
<li>Create a new Directory/Folder for your application (Ex : G:/ Hybrid Mobile App).</li>
<li>Open Command prompt and Navigate to the directory (i: e-&nbsp;<em>G:/</em>&nbsp;Hybrid Mobile App) that you have created recently for your &nbsp;Mobile Application.</li>
<li>And enter the following syntax</li>
<li><em>Syntax : &nbsp;</em>cordova create EmailMeApp com.brs.emailmeapp EmailMeApp</li>
<li>And a new cordova project named &ldquo;EmailMeApp&rdquo; will be created under that location (G:/ Hybrid Mobile App).</li>
</ul>
<p><strong>&nbsp;</strong></p>
<p><strong>1.2 &ndash; </strong><strong>Test Your Cordova Project</strong></p>
<ul>
<li>Go inside the project (G:/ Hybrid Mobile App/EmailMeApp)find &ldquo;www&rdquo; folder and then inside this folder select &ldquo;index.html&rdquo; (G:/ Hybrid Mobile App/EmailMeApp/www/index.html) and open it in any browser.</li>
<li>If it successfully opens and you can find the cordova&rsquo;s default page and default message then, Congrats you completed your first step .</li>
</ul>
<p>&nbsp;</p>
<p><center><strong>Step 2 : Installing Cordova Plugins</strong></center></p>
<p>There are so many plug-in available for various purposes in Cordova , which you can find at <a href="https://cordova.apache.org/plugins/">https://cordova.apache.org/plugins/</a> , also one can develop it&rsquo;s own plug-in and use it or distribute it .</p>
<p><strong>2.1 &ndash; Installing PlugIn Required to Send Email</strong></p>
<ul>
<li>In our application we will use &ldquo;CordovaEmail Plugin&rdquo; whose details can be found at <a href="https://www.npmjs.com/package/cordova-plugin-email-composer">https://www.npmjs.com/package/cordova-plugin-email-composer</a> .</li>
<li>Now in Command Prompt navigate to your newly created cordova project (i:e EmailMeApp) </li>
</ul>
<p>&gt;&gt; And enter the following syntax :</p>
<p><strong>Syntax :</strong> <em>cordova plugin add <a href="mailto:cordova-plugin-email-composer@0.8.3">cordova-plugin-email-composer@0.8.3</a></em></p>
<ul>
<li>You can check this plugin under &ldquo;plugins&rdquo; folder of your project (I&rdquo;e EmailMeApp/plugins).</li>
<li>Note : According to the authors <em>&ldquo;</em><em>The Email service is only available on devices which are capable &nbsp;to send emails. E.g. which have configured an email account and have installed an email app. &ldquo;</em></li>
</ul>
<p><strong>2.2 &ndash; Adding the Plugin reference in config.xml :</strong></p>
<ul>
<li>Open &ldquo;config.xml&rdquo; (i:e EmailMeApp/config.xml) and add following line :-</li>
</ul>
<p><em>&lt;plugin name="cordova-plugin-email-composer" spec="1" /&gt;</em></p>
<p><center><strong>Step -3 : Implementing Email Me Application</strong></center></p>
<p><strong>3.1 &ndash; Editing index.html :</strong></p>
<ul>
<li>Open &ldquo;index.html&rdquo; (i:e EmailMeApp/www/index.html), and remove all the <em>html contents </em>from the <em>&lt;body&gt; </em>tag, And place the following codes inside the <em>&lt;body&gt; </em></li>
</ul>
<p>Codes : <em>&lt;div&gt;</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;center&gt;&lt;h1&gt;Send Us Your FeedBack&lt;/h1&gt; </em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;br&gt;&lt;br&gt;&lt;button id="mailBtn" class="button"&gt; Click Here&lt;/button&gt;&lt;/center&gt;</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/div&gt;</em></p>
<p><strong>3.2 &ndash; Editing index.js file :</strong></p>
<ul>
<li>In above UI when the user will click on the &ldquo;Click Here&rdquo; button the compose mail screen of installed mail client will be opened.</li>
<li>Now lets implement the functionalities, for this open the &ldquo;index.js &ldquo; file present inside &ldquo;EmailMeApp/www/js/index.js&rdquo; , and write the following codes</li>
</ul>
<p><strong>Codes :</strong></p>
<p><em>bindEvents: function() {</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; document.addEventListener('deviceready', this.onDeviceReady, false);</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; document.getElementById("mailBtn").addEventListener("click", this.composeMail)</em></p>
<p><em>&nbsp;&nbsp;&nbsp; },</em></p>
<p><em>&nbsp;&nbsp;&nbsp; // deviceready Event Handler</em></p>
<p><em>&nbsp;&nbsp;&nbsp; //</em></p>
<p><em>&nbsp;&nbsp;&nbsp; // The scope of 'this' is the event. In order to call the 'receivedEvent'</em></p>
<p><em>&nbsp;&nbsp;&nbsp; // function, we must explicitly call 'app.receivedEvent(...);'</em></p>
<p><em>&nbsp;&nbsp;&nbsp; onDeviceReady: function() {</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; app.receivedEvent('deviceready');</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cordova.plugins.email.isAvailable(</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; function (isAvailable) {</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; alert('Before proceeding check your mail settings ...') ; </em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // Add app alias </em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; );</em></p>
<p><em>&nbsp;&nbsp;&nbsp; },</em></p>
<p><em>&nbsp;&nbsp;&nbsp; composeMail : function(){</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cordova.plugins.email.addAlias('gmail', 'com.google.android.gm');</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cordova.plugins.email.open({</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; app: 'gmail',</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; to:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 'bichhubiswa@gmail.com',</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; subject: 'Greetings',</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; body:&nbsp;&nbsp;&nbsp; 'How are you? Dummy mail from Bichhu &hellip;'</em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; });</em></p>
<p><em>&nbsp;</em></p>
<p><em>&nbsp;&nbsp;&nbsp; },</em></p>
<p><center><strong>4 &ndash; Building and Running the Application</strong></center></p>
<p><strong>4.1 &ndash; Building Your App</strong></p>
<ul>
<li>Here we will only build the app for Android platform, if you want to build app for other platforms then you can do it similarly by slightly modifying the syntax (Ex : <a href="http://www.tutorialspoint.com/cordova/cordova_first_application.htm">Tutorials Point</a>).</li>
</ul>
<p>Syntax : <em>&nbsp;cordova build android</em></p>
<ul>
<li>Now you can find the apk files at <em>&ldquo;EmailMeApp/platforms/android/build/outputs/apk&rdquo; .</em></li>
</ul>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </em><strong>4.2 &ndash; Running Your App </strong></p>
<ul>
<li>You can now simply take the apk file from the said location and install it in your android device and run it .</li>
<li>For more alternatives to run an apk file please refer to <a href="http://www.tutorialspoint.com/cordova/cordova_first_application.htm">Tutorials Point</a> .</li>
</ul>
<p>&nbsp;</p>
