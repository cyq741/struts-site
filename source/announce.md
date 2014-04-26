---
layout: default
title: Announcements
---
# Announcements

<p class="pull-right">
  Skip to: <a href="announce-2013.html">Announcements - 2013</a>
</p>

#### <span id="a20140424"> 24 April 2014 - Struts 2.3.16.2 General Availability Release - Security Fix Release

The Apache Struts group is pleased to announce that Struts 2.3.16.2 is available as a "General Availability"
release. The GA designation is our highest quality grade.

Apache Struts 2 is an elegant, extensible framework for creating enterprise-ready Java web applications.
The framework is designed to streamline the full development cycle, from building, to deploying,
to maintaining applications over time.

Two security issues were solved with this release:

  - [S2-021](http://struts.apache.org/release/2.3.x/docs/s2-021.html)
    Improves excluded params to avoid ClassLoader manipulation via ParametersInterceptor
  - [S2-021](http://struts.apache.org/release/2.3.x/docs/s2-021.html)
    Adds excluded params to CookieInterceptor to avoid ClassLoader manipulation when the interceptors is configured
    to accept all cookie names (wildcard matching via "*")

All developers are strongly advised to perform this action.

#### <span id="a20140424"> 24 April 2014 - Struts up to 2.3.16.1: Zero-Day Exploit Mitigation

In Struts 2.3.16.1, an issue with ClassLoader manipulation via request parameters was supposed to be resolved. Unfortunately, 
the correction wasn't sufficient.

A security fix release fully addressing this issue is in preparation and will be released as soon as possible.

Once the release is available, all Struts 2 users are strongly recommended to update their installations.

**Until the release is available, all Struts 2 users are strongly recommended to apply the following mitigation:**

In your struts.xml, replace all custom references to params-interceptor with the following code, especially regarding the class-pattern
found at the beginning of the excludeParams list:

    <interceptor-ref name="params">
       <param name="excludeParams">(.*\.|^|.*|\[('|"))(c|C)lass(\.|('|")]|\[).*,^dojo\..*,^struts\..*,^session\..*,^request\..*,^application\..*,^servlet(Request|Response)\..*,^parameters\..*,^action:.*,^method:.*</param>
    </interceptor-ref>

If you are using default interceptor stacks packaged in struts-default.xml, change your parent packages to a customized secured configuration
as in the following example. Given you are using defaultStack so far, change your packages from

    <package name="default" namespace="/" extends="struts-default">
        <default-interceptor-ref name="defaultStack" />
        ...
        ...
    </package>

to

    <package name="default" namespace="/" extends="struts-default">
        <interceptors>
            <interceptor-stack name="secureDefaultStack">
                <interceptor-ref name="defaultStack">
                    <param name="params.excludeParams">(.*\.|^|.*|\[('|"))(c|C)lass(\.|('|")]|\[).*,^dojo\..*,^struts\..*,^session\..*,^request\..*,^application\..*,^servlet(Request|Response)\..*,^parameters\..*,^action:.*,^method:.*</param>
                </interceptor-ref>
            </interceptor-stack>
        </interceptors>

        <default-interceptor-ref name="secureDefaultStack" />
        ...
    </package> 

Please follow the Apache Struts Announcements to stay updated regarding the upcoming security release. Most likely the release will be available within the next 72 hours.
Please prepare for upgrading all Struts 2 based production systems to the new release version once available.

#### <span id="a20140302"> 2 March 2014 - Struts 2.3.16.1 General Availability Release - Security Fix Release

The Apache Struts group is pleased to announce that Struts 2.3.16.1 is available as a "General Availability"
release. The GA designation is our highest quality grade.

Apache Struts 2 is an elegant, extensible framework for creating enterprise-ready Java web applications.
The framework is designed to streamline the full development cycle, from building, to deploying,
to maintaining applications over time.

Two security issues were solved with this release:

  - [S2-020](http://struts.apache.org/release/2.3.x/docs/s2-020.html) ClassLoader manipulation
    via request parameters
  - [S2-020](http://struts.apache.org/release/2.3.x/docs/s2-020.html) Commons FileUpload library was upgraded
    to version 1.3.1 to prevent DoS attacks

All developers are strongly advised to perform this action.

#### <span id="a20140221"> 21 February 2014 - Immediately upgrade commons-fileupload to version 1.3.1

The Apache Struts Team recommends to immediately upgrade your Struts 2
based projects to use the latest released version of Commons
FileUpload library, which is currently 1.3.1. This is necessary to
prevent your publicly accessible web site from being exposed to
possible DoS attacks (see \[1] \[2]).

Your project is affected if it uses the built-in file upload mechanism
of Struts 2, which defaults to the use of commons-fileupload. The
updated commons-fileupload library is a drop-in replacement for the
vulnerable version. Deployed applications can be hardened by replacing
the commons-fileupload jar file in WEB-INF/lib with the fixed jar. For
Maven based Struts 2 projects, the following dependency needs to be
added:

    <dependency>
      <groupId>commons-fileupload</groupId>
      <artifactId>commons-fileupload</artifactId>
      <version>1.3.1</version>
    </dependency>

More details can be found here:

  1. <a href="http://commons.apache.org/proper/commons-fileupload/changes-report.html#a1.3.1">
      http://commons.apache.org/proper/commons-fileupload/changes-report.html#a1.3.1</a>
  2. <a href="http://mail-archives.apache.org/mod_mbox/www-announce/201402.mbox/%3C52F373FC.9030907@apache.org%3E">
      http://mail-archives.apache.org/mod_mbox/www-announce/201402.mbox/%3C52F373FC.9030907@apache.org%3E</a>

All developers are strongly advised to perform this action.

<p class="pull-right">
  Skip to: <a href="announce-2013.html">Announcements - 2013</a>
</p>

<p class="pull-left">
  <strong>Next:</strong>
  <a href="kickstart.html">Kickstart FAQ</a>
</p>