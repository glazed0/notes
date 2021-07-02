<h1 id="dos-and-donts-of-html-email-development-in-2021">Dos (and Don’ts) of HTML email development in 2021</h1>
<p>(In no particular order)<br>
When coding emails in 2021, here are some tips and tricks that you can keep in your toolbox so your clients don’t have sketchy looking emails in Microsoft Outlook.</p>
<h2 id="dont-code-everything-from-scratch-every-time">Don’t code everything from scratch, every time</h2>
<p>There are tools (link to last tip) that can help speed up your workflow.</p>
<ul>
<li>Buttons, background images (and patterns)</li>
<li>Use design templates in your UI tool (Sketch, Figma, XD)
<ul>
<li>consistent artboard widths and content widths (and margins) make development much easier</li>
</ul>
</li>
</ul>
<h2 id="do-use-google-fonts">Do use Google Fonts</h2>
<p>Let me explain… Outlook doesn’t render Google fonts (since you’ll need to call them in the <code>head</code> and Outlook strips that tag), but that doesn’t mean you should only use Arial and Times in every email. You can use Google fonts in your email designs, as long as their line height, letter spacing, and font size rendering will be friendly when Outlook defaults to Arial and Times. Always use <a href="https://www.cssfontstack.com/">font stacks</a> and make sure your Google Font calls don’t have quotes, as Outlook becomes finicky and can ignore the whole <code>font-family</code> rule if one of them has quotes.</p>
<h2 id="dont-be-afraid-to-nest-your-tables.-seriously.">Don’t be afraid to nest your tables. Seriously.</h2>
<p>Nested tables makes spacing your elements vertically trivial, and will cause fewer bugs in Outlook’s appalling rendering system. Add your <code>background-color</code> to your <code>&lt;table&gt;</code>, and your <code>padding-top</code> and <code>padding-bottom</code> to your <code>td</code>:</p>
<pre><code>&lt;body bgcolor="#fff" style="display: block; Margin: 0; padding: 0;"&gt;
    &lt;!-- Your parent table --&gt;
    &lt;table align="center" cellpadding="0" cellspacing="0" style="Margin: 0 auto;" width="640"&gt;
        &lt;tr&gt;
            &lt;!-- Where you can add your internal vertical spacing --&gt;
            &lt;td style="padding: 40px 0px;"&gt;
                &lt;!-- Here's where your modules can start --&gt;
                &lt;table align="center" cellpadding="0" cellspacing="0" style="Margin: 0 auto; background-color: #eaeaea;" width="640"&gt;
                    &lt;tr&gt;
                        &lt;td&gt;&lt;/td&gt;
                    &lt;/tr&gt;
                &lt;/table&gt;
            &lt;/td&gt;
        &lt;/tr&gt;
    &lt;/table&gt;
&lt;/body&gt;
</code></pre>
<blockquote>
<p>Note: Make sure that the <code>td</code> that has your vertical padding is the only <code>td</code> in it’s parent <code>tr</code>, otherwise you may run into spacing inconsistencies in Outlook</p>
</blockquote>
<p>Now, when working with horizontal spacing, the most fool-proof method doesn’t involve <code>margin</code> or <code>padding</code> like it does in normal 21st century CSS. You should be using empty <code>td</code> with a <code>width</code> attribute to control horizontal spacing. Below, I’ll start the snippet with our child <code>table</code> from above and continue with some left and right “margins”:</p>
<pre><code>&lt;table cellspacing="0" cellpadding="0" width="640" align="center" style="Margin: 0 auto; background-color: #eaeaea;"&gt;
    &lt;tr&gt;
        &lt;td width="40"&gt;&lt;/td&gt;
        &lt;td width="560"&gt;
            &lt;!-- Here's where your content can go --&gt;
            &lt;img src="#0" width="560" style="width: 560px; display: block; Margin: 0; padding: 0;"&gt;
        &lt;/td&gt;
        &lt;td width="40"&gt;&lt;/td&gt;
    &lt;/tr&gt;
&lt;/table&gt;
</code></pre>
<p>At this point in your code, your vertical spacing should already have been taken care of. In the <code>td</code> that holds your content, make sure that it’s <code>width</code> is taking up the exact space that the <code>td</code> elements aren’t. Now you’re free to now add your <code>img</code> and text elements as you wish!</p>
<h2 id="do-pay-attention-to-your-width-on-img">Do pay attention to your width on <code>img</code></h2>
<p>Notice how I added a <code>width</code> attribute to the <code>img</code>? Outlook will otherwise expand the image to it’s 100% width, even if your <code>td</code> has a fixed width. Also, add <code>display: block; Margin: 0; padding: 0;</code> to each <code>img</code> to make sure it doesn’t have access spacing that the browser or rendering system adds by default.</p>
<h3 id="what-about-retina-images">What about retina images?</h3>
<p>You can export your images as 2x from your UI software, and still use them in your email code. As long as your <code>width</code> attribute is accurate, everything will still stay in it’s place.</p>
<h2 id="dont-ignore-the-email-service">Don’t ignore the email service</h2>
<p>Coding emails can give you tunnel vision, but some email service providers have different methods to help your workflow. Also, I can’t forget to mention the astronomical list of <a href="https://www.campaignmonitor.com/css/">unsupported CSS rules</a> that makes coding emails feel like we should be worried about Y2K again.</p>
<h3 id="what-do-the-jackrabbit-developers-recommend">What do the Jackrabbit Developers recommend?</h3>
<p>There are multiple email services we love to use when working with our clients. Salesforce’s Pardot has a robust content management system for single emails and templates. Hubspot (a Boston area company!) has some developer-friendly features that make the coding process a breeze. But the Rabbit’s most favorite email service is Mailchimp with their robust template capabilities. All of these platforms have campaign flows, actions, and triggers for email marketing initiatives.</p>
<h4 id="salesforce-pardot">Salesforce Pardot</h4>
<p>While currently undergoing some transitions into Salesforce’s main interface, Pardot still is one of the flagship email marketing platforms that we love using when working with clients. Pardot has the ability to use advanced dynamic content</p>
<h4 id="hubspot">Hubspot</h4>
<p>I won’t get deep into the CRM capabilities that are shared/differentiated between Salesforce and Hubspot, but I will say that Hubspot is a much easier and user-friendly tool to work with that won’t require immense amounts of training and practice to learn the ins-and-outs. Hubspot has custom <a href="https://developers.hubspot.com/docs/cms/building-blocks/templates/email-template-markup">syntax and attributes</a> which gives breadth to template development.</p>
<h4 id="mailchimp">Mailchimp</h4>
<p>Mailchimp has <a href="https://mailchimp.com/help/create-editable-content-areas-with-mailchimps-template-language/">custom attributes</a> that makes coding emails a bit more time consuming, but ultimately creates an amazing template experience for the client. Many comparison articles online fail to mention this feature, unfortunately. While not as much of a customer relationship management (CRM) tool as Salesforce’s Pardot, Mailchimp can cater to both B2B and B2C organizations and still scales well with a growing customer base, and has a <em><strong>much</strong></em> smaller monthly cost!</p>
<h3 id="what-about-constant-contact">What about Constant Contact?</h3>
<p>While Constant Contact has been a mainstay in the email marketing space for many years, it hasn’t grown in complexity in the ways of other platforms. It’s a great visual email builder for the marketers who aren’t HTML savvy, but without the ability to even change plain text in a visual editor, many clients need additional help with their campaigns more often then when they use a platform like Mailchimp or Pardot.</p>
<h2 id="do-use-tools-and-resources-to-help-development-workflow-probably-the-last-tip">Do use tools and resources to help development workflow (probably the last tip)</h2>
<p>Here are some helpful links to help save time and energy while you’re coding and listening to <a href="https://www.youtube.com/watch?v=5qap5aO4i9A">lofi hip hop beats</a> to study and relax to:<br>
Code Tools</p>
<ul>
<li><a href="https://www.image-map.net/">Image-Map Generator</a></li>
<li><a href="https://buttons.cm/">Bulletproof email buttons</a></li>
<li><a href="https://backgrounds.cm/">Bulletproof background images</a></li>
</ul>
<p>CSS Inlining</p>
<ul>
<li><a href="https://templates.mailchimp.com/resources/inline-css/">Mailchimp CSS Inliner</a></li>
<li><a href="https://htmlemail.io/inline/">HTML Email CSS Inliner</a></li>
</ul>
<p>Fonts</p>
<ul>
<li><a href="https://www.cssfontstack.com/">font stacks</a></li>
<li><a href="https://fonts.google.com/">Google Fonts</a></li>
</ul>
<p>Pre-Deployment Checklist</p>
<ul>
<li><a href="https://www.emailonacid.com/">Email on Acid</a></li>
<li><a href="https://www.litmus.com/">Litmus</a></li>
</ul>
<p>Further Readings</p>
<ul>
<li><a href="https://thebetter.email/">The Better Email</a></li>
<li><a href="https://webdesign.tutsplus.com/tutorials/creating-a-future-proof-responsive-email-without-media-queries--cms-23919">Creating Future-Proof Responsive Email without Media Queries</a></li>
</ul>
<p>Codepens &amp; Git Repositories</p>
<ul>
<li><a href="https://codepen.io/reallygoodemails">Really Good Emails</a></li>
<li><a href="https://github.com/dandenney/eMMail">The eMMail system</a></li>
</ul>

