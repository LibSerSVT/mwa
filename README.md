# microwebapp - build
Micro Web Application
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<HTML>
<HEAD>
<META http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<META name="GENERATOR" content="IBM WebSphere Studio">
<TITLE>Micro Benchmarks - mod title</TITLE>
</HEAD>
<BODY>

<P>This Web Application contains some micro-benchmark
applications, plus a few interesting utilities.  They are listed
below.</P>

<H2>ping.html, ping.jsp</H2>

<P><A name="ping"></A>A simple <A href="ping.html">page</A> and <A href="ping.jsp">servlet</A>
that do nothing but respond "Ping!".</P>

<H2>large.html</H2>

<P><A name="large.html"></A>A <A href="large.html">large HTML page</A>.
The HTML source size is 63151 bytes.</P>

<H2>PostEcho</H2>

<FORM action="PostEcho" method="post" enctype="multipart/form-data">
<P>This servlet handles only POST, and
simply copies the request body into the
response body.  For an example,
click <INPUT type="submit" value="send">.
<LABEL>Example input:
</LABEL><INPUT type="text" value="fubar">
</P>
</FORM>

<H2>PingSession</H2>

<P>This servlet tests fundamental HTTP session functionality
by creating a unique session ID for each individual user.
The ID is stored in the users session and is accessed
and displayed on each user request.
For an example, click <A href="PingSession">here</A>.</P>

<H2>ServerInfo</H2>

<P>This servlet prints some basic info
from the servlet's perspective.
For an example, click <A href="ServerInfo">here</A>.</P>

<H2>ResponseFromQuery</H2>

<P>This servlet replies with a response code given in
the query string.  For an example, click
<A href="ResponseFromQuery?responseCode=414">here</A>.</P>

<H2>CpuLoad</H2>

<P><A name="CpuLoad"></A>A single invocation of this servlet applies a controlled amount
of CPU load for a controlled amount of time.
The CPU load consists of doing a given amount of arithmetic per second.
When not doing arithmetic, time is passed in <code>Thread.sleep()</code>.
One parameter is a rate, the rate at which arithmetic units are done.
One unit of arithmetic consists of doing a given number (also a parameter)
of iterations of a certain loop.
This servlet returns a plain text body showing the output of running
for a given amount of time; the invocation does not return until
the given amount of time has passed.
The output has a summary every minute, showing statistics on both
the sleeps and the units of computation; there are both
cumulative statistics and per-minute statistics.
Click <A href="CpuLoad?maxMins=1.01">here</A> for an example
that runs for one minute.
Following are the parameters.</P>

<DL>
	<DT>concurrency</DT>
	<DD>The number of parallel threads to use.</DD>
	
	<DT>kCount</DT>
	<DD>The number of thousands of iterations to use
	as the unit of arithmetic.  An integer.</DD>
	
	<DT>rate</DT>
	<DD>The number of units of arithmetic to do per second.
	This is a float-point number in decimal format</DD>
	
	<DT>sleepMillis</DT>
	<DD>The number of milliseconds to sleep at a time.
	This is an integer.</DD>
	
	<DT>maxMins</DT>
	<DD>The number of minutes for which to apply the load.
	This is a floating-point number in decimal format.</DD>

</DL>

<H2>CpuAndSleepBound</H2>

<P><A name="CpuAndSleepBound"></A>Click <A
href="CpuAndSleepBound?deterministic=true&sleepLength=100">here</A>
for an example.  This servlet does a programmable combination of
arithmetic, <code>Thread.yield()</code>, and
<code>Thread.sleep(ms)</code>.  The basic code structure is to
iterate through a loop a certain number of times, invoking
<code>Thread.yield()</code> and <code>Thread.sleep(ms)</code>
every so often.
</P>
<P>This servlet takes several parameters, in the usual HTTP ways
(e.g., an HTTP query string).  All are optional.  Here is an example invocation:
<BLOCKQUOTE>
<code>http://host/root/CpuAndSleepBound?deterministic=true&amp;sleepLength=100</code>
</BLOCKQUOTE>The actual values used are echoed in the output.
Following is a list of the available parameters.</P>

<DL>
	<DT><A
	name="CpuAndSleepBound_deterministic">deterministic</A></DT>
	<DD>The number of iterations can be either deterministic or
	chosen randomly from a truncated negative exponential
	distribution; this parameter indicates which it will be.  The
	value should be either <code>true</code> or
	<code>false</code>; default is <code>false</code>.</DD>

	<DT><A name="CpuAndSleepBound_countMax">countMax</A></DT>
	<DD>This parameter is used only if the number of iterations is
	random; in that case, this parameter is the maximum value that
	will be used.  The value should be a decimal integer, without
	commas; default is 100,000.</DD>

	<DT><A name="CpuAndSleepBound_countMean">countMean</A></DT>
	<DD>If the number of iterations is deterministic, this
	paramter is it; otherwise, this parameter gives the mean of
	the distribution (without considering the truncation).  The
	value should be a decimal integer, without commas; default is
	30,000.</DD>

	<DT><A
	name="CpuAndSleepBound_yieldInterval">yieldInterval</A></DT>
	<DD>This parameter gives the number of iterations between
	calls on <code>Thread.yield()</code>.  The value should be a
	decimal integer without commas; default is 1,000.</DD>

	<DT><A
	name="CpuAndSleepBound_sleepInterval">sleepInterval</A></DT>
	<DD>This parameter gives the number of iterations between
	calls on <code>Thread.sleep(ms)</code>.  The value should be a
	decimal integer without commas; default is 3,000.</DD>

	<DT><A name="CpuAndSleepBound_zk">zk</A> ("zero key")</DT>
	<DD>There are two choices available for the phase of the calls
	on <code>Thread.yield()</code> and
	<code>Thread.sleep(ms)</code>.  One choice is to invoke
	whenever the iteration count is equal to 0 modulo the relevant
	<var>interval</var> above; the other choice is when the
	iteration count is equal to half of the interval, modulo the
	interval.  For example, using the first choice, with an
	interval that is at least as large as the actual number of
	iterations, will result in exactly one invocation (the
	counting starts at 0).  For another example, using the second
	choice, with an interval that is at least twice as large as
	the number of iterations, will cause no invocations.  The
	value should be either <code>true</code> or
	<code>false</code>, which code for the first and second
	choices above, respectively; default is
	<code>true</code>.</DD>

	<DT><A
	name="CpuAndSleepBound_sleepLength">sleepLength</A></DT>
	<DD>This parameter gives the number of milliseconds
	<code>ms</code> used in <code>Thread.sleep(ms)</code>.  The
	value should be a decimal integer without commas; default is
	1.  Remember that <code>Thread.sleep</code> may actually pause
	longer than the requested amount of time --- and on Linux has
	been observed to always sleep for 11 to 20 ms longer than
	requested when invoked under light CPU load.</DD>

	<DT><A name="CpuAndSleepBound_debConc">debConc</A> ("debug
	concurrency")</DT> <DD>This servlet has some concurrency
	instrumentation built in; this parameter can disable it.  The
	value should be either <code>true</code> or
	<code>false</code>; default is <code>true</code>.</DD>

</DL>


<H2>CpuAndGetBound</H2>

<P><A name="CpuAndGetBound"></A>Click <A
href="CpuAndGetBound?deterministic=true">here</A>
for an example.  This servlet does a programmable combination of
arithmetic, <code>Thread.yield()</code>, and
HTTP GET.  The basic code structure is to
iterate through a loop a certain number of times, invoking
<code>Thread.yield()</code> and HTTP GET
every so often.
</P>
<P>This servlet takes several parameters, in the usual HTTP ways
(e.g., an HTTP query string).  All are optional.  Here is an example invocation:
<BLOCKQUOTE>
<code>http://host/root/CpuAndGetBound?deterministic=true&amp;countMean=10000</code>
</BLOCKQUOTE>The actual values used are echoed in the output.
Following is a list of the available parameters.</P>

<DL>
	<DT><A
	name="CpuAndGetBound_deterministic">deterministic</A></DT>
	<DD>The number of iterations can be either deterministic or
	chosen randomly from a truncated negative exponential
	distribution; this parameter indicates which it will be.  The
	value should be either <code>true</code> or
	<code>false</code>; default is <code>false</code>.</DD>

	<DT><A name="CpuAndGetBound_countMax">countMax</A></DT>
	<DD>This parameter is used only if the number of iterations is
	random; in that case, this parameter is the maximum value that
	will be used.  The value should be a decimal integer, without
	commas; default is 100,000.</DD>

	<DT><A name="CpuAndGetBound_countMean">countMean</A></DT>
	<DD>If the number of iterations is deterministic, this
	paramter is it; otherwise, this parameter gives the mean of
	the distribution (without considering the truncation).  The
	value should be a decimal integer, without commas; default is
	30,000.</DD>

	<DT><A
	name="CpuAndGetBound_yieldInterval">yieldInterval</A></DT>
	<DD>This parameter gives the number of iterations between
	calls on <code>Thread.yield()</code>.  The value should be a
	decimal integer without commas; default is 1,000.</DD>

	<DT><A
	name="CpuAndGetBound_getInterval">getInterval</A></DT>
	<DD>This parameter gives the number of iterations between
	HTTP GET operations.  The value should be a
	decimal integer without commas; default is 3,000.</DD>

	<DT><A name="CpuAndGetBound_zk">zk</A> ("zero key")</DT>
	<DD>There are two choices available for the phase of the calls
	on <code>Thread.yield()</code> and
	HTTP GET.  One choice is to invoke
	whenever the iteration count is equal to 0 modulo the relevant
	<var>interval</var> above; the other choice is when the
	iteration count is equal to half of the interval, modulo the
	interval.  For example, using the first choice, with an
	interval that is at least as large as the actual number of
	iterations, will result in exactly one invocation (the
	counting starts at 0).  For another example, using the second
	choice, with an interval that is at least twice as large as
	the number of iterations, will cause no invocations.  The
	value should be either <code>true</code> or
	<code>false</code>, which code for the first and second
	choices above, respectively; default is
	<code>true</code>.</DD>

	<DT><A
	name="CpuAndGetBound_target">target</A></DT>
	<DD>This parameter gives the URL on which the HTTP GET
	operations are invoked.  The default value is
	"CpuAndSleepBound".</DD>

	<DT><A
	name="CpuAndGetBound_readBufSize">readBufSize</A></DT>
	<DD>This parameter gives the size of the byte buffer
	used to read an HTTP reply.</DD>

	<DT><A name="CpuAndGetBound_debConc">debConc</A> ("debug
	concurrency")</DT> <DD>This servlet has some concurrency
	instrumentation built in; this parameter can disable it.  The
	value should be either <code>true</code> or
	<code>false</code>; default is <code>true</code>.</DD>

</DL>


<H2>CpuAndEchoBound</H2>

<P><A name="CpuAndEchoBound"></A>Click <A
href="CpuAndEchoBound?deterministic=true">here</A>
for an example.  This servlet does a programmable combination of
arithmetic, <code>Thread.yield()</code>, and
waiting using an echo or wait server.  The basic code structure is to
iterate through a loop a certain number of times, invoking
<code>Thread.yield()</code> and wait using echo server
every so often. The echo server on TCP port 7, available on many OSes may be used.
If this is used, the sleepLength argument is ignored. If you want something that will sleep,
you can use the simple wait server. The wait server has been packaged into the J2EE ear,
and must be extracted from the ear. Inside an ear file is either a microwebapp.war file or directory.
Within that is the WEB-INF/classes directory. Create a jar file with the contents of the classes directory.
Then run the class <code>com.ibm.wsmm.services.waiter.WaitServer</code>.
This will run an echo server that waits on TCP port 5867.</P>

<P>
To use this servlet, you must tell it the echo or wait server endpoints to use.
These endpoints are put in a pool that is shared by all invocations of this servlet in a given appserver.
Each endpoint is a connection to the echo/wait server.
If you don't have enough endpoints in the pool to handle max concurrency, you will have contention for the endpoints.
There are two ways to specify the endpoints: (1) prepare each appserver with a list of endpoints to use,
or (2) in each invocation pass the list of endpoints to use.  Do only one of these two.
<A name="CpuAndEchoBound_target">The first alternative</A> is done by issuing
the request:
<BLOCKQUOTE>
<code>http://host/root/CpuAndEchoBound?target=n,endpoint,endpoint2,...,endpointk</code>
</BLOCKQUOTE>
This will create n connections to each of the endpoints specified.
The syntax of an endpoint is <var>host</var>[<code>":"</code><var>port</var>] ---
that is host optionally followed by a colon and port number.  A host can be specified
either by IP address (as parsed by Java) or name.
This must be done with every app server
in the cluster.
This request may be issued multiple times to a server.
Each time the additional endpoints are added to the list of endpoints available.
</P>

<P>The second alternative way to specify the endpoints is to
pass the complete list in every invocation.
No two concurrent invocations should be given different lists.
The list should be changed rarely:
any change in the list involves breaking all the old connections
and making all new connections.
The list of endpoints is passed as a regular parameter, which is among those detailed below.
</P>

<P>This servlet takes several parameters, in the usual HTTP ways
(e.g., an HTTP query string).  All are optional.  Here is an example invocation:
<BLOCKQUOTE>
<code>http://host/root/CpuAndEchoBound?deterministic=true&amp;countMean=10000</code>
</BLOCKQUOTE>The actual values used are echoed in the output.
Following is a list of the available parameters.<DL>

	<DT><A name="CpuAndEchoBound_allTargets">allTargets</A></DT>
	<DD>The complete list of echo/wait server endoints to use,
	if you are using the second of the two possible ways to
	specify this list.  The syntax for the value is the
	same as for the <code>target</code> parameter.</DD>
	
	<DT><A
	name="CpuAndEchoBound_deterministic">deterministic</A></DT>
	<DD>The number of iterations can be either deterministic or
	chosen randomly from a truncated negative exponential
	distribution; this parameter indicates which it will be.  The
	value should be either <code>true</code> or
	<code>false</code>; default is <code>false</code>.</DD>

	<DT><A name="CpuAndEchoBound_countMax">countMax</A></DT>
	<DD>This parameter is used only if the number of iterations is
	random; in that case, this parameter is the maximum value that
	will be used.  The value should be a decimal integer, without
	commas; default is 100,000.</DD>

	<DT><A name="CpuAndEchoBound_countMean">countMean</A></DT>
	<DD>If the number of iterations is deterministic, this
	paramter is it; otherwise, this parameter gives the mean of
	the distribution (without considering the truncation).  The
	value should be a decimal integer, without commas; default is
	30,000.</DD>

	<DT><A
	name="CpuAndEchoBound_yieldInterval">yieldInterval</A></DT>
	<DD>This parameter gives the number of iterations between
	calls on <code>Thread.yield()</code>.  The value should be a
	decimal integer without commas; default is 1,000.</DD>

	<DT><A
	name="CpuAndEchoBound_getInterval">getInterval</A></DT>
	<DD>This parameter gives the number of iterations between
	HTTP GET operations.  The value should be a
	decimal integer without commas; default is 3,000.</DD>

	<DT><A name="CpuAndEchoBound_zk">zk</A> ("zero key")</DT>
	<DD>There are two choices available for the phase of the calls
	on <code>Thread.yield()</code> and
	HTTP GET.  One choice is to invoke
	whenever the iteration count is equal to 0 modulo the relevant
	<var>interval</var> above; the other choice is when the
	iteration count is equal to half of the interval, modulo the
	interval.  For example, using the first choice, with an
	interval that is at least as large as the actual number of
	iterations, will result in exactly one invocation (the
	counting starts at 0).  For another example, using the second
	choice, with an interval that is at least twice as large as
	the number of iterations, will cause no invocations.  The
	value should be either <code>true</code> or
	<code>false</code>, which code for the first and second
	choices above, respectively; default is
	<code>true</code>.</DD>

	<DT><A
	name="CpuAndEchoBound_sleepLength">sleepLength</A></DT>
	<DD>This parameter gives the number of milliseconds
	<code>ms</code> used in <code>Thread.sleep(ms)</code>.
	A negative number indicates Thread.sleep() is not called, this results in no waiting. The default is "5".
	Remember that <code>Thread.sleep</code> may actually pause
	longer than the requested amount of time --- and on Linux has
	been observed to always sleep for 11 to 20 ms longer than
	requested when invoked under light CPU load. This value is only used if the echo server is <code>com.ibm.wsmm.services.waiter.WaitServer.</code></DD>

	<DT><A
	name="CpuAndEchoBound_target">target</A></DT>
	<DD>A list of echo or wait server endpoints.  The syntax is:
	<code>
	count "," host [ ":" port ] [ "," host [ ":" port ] ]*
	</code>
	Where:
	<dl>
	<dt>count</dt>
	<dd>The number of enpoint sets to create.</dd>
	<dt>host</dt>
	<dd>A host or IP address.</dd>
	<dt>port</dt>
	<dd>a port number.</dd>
	</dl>
	Example:
	<code>
	5,xyz.example.com:5867,abc.example.com:5867
	</code>
	Will create 10 connections, five to xyz, and five to abc.
	</DD>

	<DT><A name="CpuAndEchoBound_debConc">debConc</A> ("debug
	concurrency")</DT> <DD>This servlet has some concurrency
	instrumentation built in; this parameter can disable it.  The
	value should be either <code>true</code> or
	<code>false</code>; default is <code>true</code>.</DD>

</DL>


<H2>CPUBound</H2>

<P><A name="CPUBound"> This servlet is a restricted version of 
<code>CpuAndSleepBound</code> that takes a single optional
parameter.  
</P>
<DL>
	<DT><A name="CPUBound_count">count</A></DT>
	<DD>This parameter is used as <code>countMean</code> for 
	<code>CpuAndSleepBound</code>. (Defaults are used for the
	remaining parameters.) The default value is 0.</DD>
</DL>

<H2>sleepBound</H2>
<P><A name="sleepBound"> This servlet executes a combination of
<code>Thread.sleep(ms)</code> and <code>Thread.yield()</code>operations.  
It takes the following optional parameters.
</P>
<DL>
	<DT><A
	name="sleepBound_deterministic">deterministic</A></DT>
	<DD>The sleep time can be either deterministic or
	chosen randomly from a negative exponential distribution; this 
	parameter indicates which it will be.  The
	value should be either <code>true</code> or
	<code>false</code>.  If it is true, the sleep time is taken
	from the <code>ms</code> parameter. Default is <code>true</code>.</DD>

	<DT><A name="sleepBound_ms">ms</A></DT>
	<DD>Sleep time in milleseconds. The default is 1000.</DD>

	<DT><A name="sleepBound_precise">precise</A></DT>
	<DD>This parameter controls whether the servlet attempts
	to account for inaccuracies in <code>Thread.sleep</code>
	(see remark under the sleepLength parameter of 
	<code>CpuAndSleepBound</code>).
	The default is <code>false</code>.</DD>
</DL>

<H2>IOBound</H2>
<P><A name="IOBound"> This servlet simulates IO activity by
writing strings to a file. 
It takes the following optional parameter.
</P>
<DL>
	<DT><A name="IOBound_nOfBytes">nOfBytes</A></DT>
	<DD>Number of bytes to write.  The default is 1000.</DD>
</DL>

<H2>memBound</H2>
<P><A name="memBound"></A>Click <A
href="memBound?chunkSize=3&m=4">here</A>
for an example.  This servlet simulates memory activity by iteratively
allocating blocks of memory, performing arithmetic operations over integer 
values striped across the blocks, freeing a block and allocating a new one, 
and then sleeping.
</P>
<P>This servlet takes several parameters, in the usual HTTP ways
(e.g., an HTTP query string).  All are optional.  Here is an example invocation:
<BLOCKQUOTE>
<code>http://host/root/memBound?chunkSize=3&m=4</code>
</BLOCKQUOTE>The actual values used are echoed in the output.
</P>
<P>It takes the following optional parameters.
</P>
<DL>
	<DT><A name="memBound_chunkSize">chunkSize</A></DT>
	<DD>Size of memory blocks allocated, in number of ints.
	The default is 2.
	</DD>

	<DT><A name="memBound_m">m</A></DT>
	<DD>Number of blocks processed concurrently during arithmetic operation.
	The default is 2.
	</DD>

	<DT><A name="memBound_nInner">nInner</A></DT>
	<DD>Controls the arithmetic loop, so that the servlet twiddles
	<code>m*nInner*(chunkSize/100)</code> ints striped across the blocks.
	The default is 2.
	</DD>

	<DT><A name="memBound_sleepMs">sleepMs</A></DT>
	<DD>Length of the sleep interval in milleseconds.
	The default is 2.
	</DD>

	<DT><A name="memBound_nOuter">nOuter</A></DT>
	<DD>Number of iterations of the arithmetic loop, 
	memory allocation and deallocation, and sleep activities.
	The default is 2.
	</DD>
</DL>

<H2>memBoundPerSession</H2>
<P>This servlet simulates memory activity within a HTTP session.  At the 
initiation of a HTTP session, it allocate memory with the size of 
chunkSize*m ints. The newly allocating memory is attached to the HTTP session. 
This memory won't be free until a session invalidation request is received 
or a session time out occured. <A name="memBoundPerSession">
</A>Click <A
href="memBoundPerSession?login=true&chunkSize=3&m=4">login</A>
for an session initiation example. <A name="memBoundPerSession"></A>Click <A
href="memBoundPerSession?logout=true">logout</A>
for an session invalidation example. 
</P>
<P>This servlet takes several parameters, in the usual HTTP ways
(e.g., an HTTP query string).  All are optional.  Here is an example invocation:
<BLOCKQUOTE>
<code>http://host/root/memBoundPerSession?login=true&chunkSize=3&m=4</code>
</BLOCKQUOTE>The actual values used are echoed in the output.
</P>
<P>It takes the following optional parameters.
</P>
<DL>
	<DT><A name="memBoundPerSession_login">login</A></DT>
	<DD>If true, this is a HTTP session initiation request. 
	The default is false.
	</DD>
	
	<DT><A name="memBoundPerSession_logout">logout</A></DT>
	<DD>If true, this is a HTTP session invalidation request. 
	The default is false.
	</DD>
	
	<DT><A name="memBoundPerSession_chunkSize">chunkSize</A></DT>
	<DD>Size of memory blocks allocated, in number of ints.
	The default is 2.
	</DD>

	<DT><A name="memBoundPerSession_m">m</A></DT>
	<DD>Number of blocks allocated.
	The default is 2.
	</DD>
</DL>

<H2>Additional parameters for HTTP Session behavior</H2>
<P>The preceding servlets take the following additional parameters to
simulate three types of HTTP session behavior: creation,
continued use, and termination.
They are all optional, and do not occur by default.
</P>

<DL>
	<DT><A name="user">user</A></DT>
	<DD>This is not connected to HTTP authentication;
	rather, this just provides a value to put in the HTTP session. 
	</DD>
	 
	<DT><A name="login">login</A></DT>
	<DD>Indicates whether a session should be created if not already
	extant.
	</DD>
	
	<DT><A name="logout">logout</A></DT> 
	<DD>
	Indicates whether the extant session, if any, should be terminated.
	</DD>
	
	<DT><A name="sessChunks">sessChunks</A> and <A name="sessChunkSize">sessChunkSize</A></DT> 
	<DD>
	These control an amount of memory held during the lifetime of the session.
	If both are given, the memory held is set to <code>sessChunks</code>
	arrays of the Java primitive type <code>int</code>, each array is of
	length <code>sessChunkSize</code>.  If either is elided (or not positive),
	the memory previously held, if any, is released.
	</DD>
	
</DL>

<H2>Additional parameters for failure behavior</H2>
<P>The preceding servlets take the following additional parameters to
simulate three types of failure behavior: internal server failures, 
memory leaks, and deadlocks.
They are all optional, and do not occur by default. Obviously not all 
combinations of the behaviors are possible on a single request. 
The order in which they are checked is: internal failure, servlet processing, 
memory leak, deadlock.  
</P>

<P>
For example, to simulate a memory leak, 
append values for the <code>leakp</code> and <code>amount</code> 
parameters to the query string.  
The following query string would produce a 1000 byte increase 
in memory usage on every request.
<BLOCKQUOTE>
<code>http://host/root/CpuAndSleepBound?deterministic=true&amp;sleepLength=100&amp;leakp=100&amp;amount=1000</code>
</BLOCKQUOTE>The actual values used are echoed in the output.
</P>

<P>The parameters whose name ends in "p" affect only the request
on which they appear, while those whose name ends in "All" affect
that request and all subsequent requests served by the same
J2EE module instance.
</P>

<DL>
	<DT><A name="leakp">leakp</A></DT>
	<DD>The probability with which the request will allocate additional memory,
	expressed as a number between 0 and 100.   
	This is intended to simulate a memory leak.  The default value is 0. 
	</DD>
	 
	<DT><A name="amount">amount</A></DT>
	<DD>The amount of memory leaked, in bytes, if a leak occurs.  
	The default value is 0.
	</DD>
	
	<DT><A name="deadp">deadp</A></DT> 
	<DD>
	The probability with which the request is suspended, expressed as a number
	between 0 and 100. 
	This is intended to simulate a deadlock by issuing a sleep for 10 minutes.  
	The default value is 0.
	</DD>
	
	<DT><A name="deadTime">deadTime</A></DT> 
	<DD>
	The number of seconds for which this request is suspended due to
	<A href="#deadp">deadp</A>.  
	The default value is 600 (i.e., 10 minutes).
	</DD>
	
	<DT><A name="failp">failp</A></DT> 
	<DD>
	The probability with which the request is failed, expressed as a number
	between 0 and 100.
	A failed request returns an internal server error (error code 500)
	immediately - no servlet processing or other failure behaviors occur. 
	The default value is 0. 
	</DD>
	
	<DT><A name="failAll">failAll</A></DT>
	<DD>
	If set to <code>true</code>, creates a persistent failure
	until explicitly cleared.  This is useful as a "poison pill" which can be
	sent to a subset of members of a cluster.  When used in combination with
	<code>failp</code>, the request fails if either a persistent failure 
	or a request failure is indicated.
	If set to <code>false</code>, clears the persistent failure condition.
	The default value is to make no change in the persistent failure condition.
	</DD>

	<DT><A name="deadTimeAll">deadTimeAll</A></DT>
	<DD>
	The value, if given, should be an integer; it is a number of seconds.
	If set to a positive value, creates a persistent deadlock
	until explicitly cleared --- but this request
	does not itself hang due to this condition.
	This is useful as a "poison pill" which can be
	sent to a subset of members of a cluster.  When used in combination with
	<code>deadp</code>, the request deadlocks if either a persistent deadlock 
	or a request deadlock is indicated; if both are, the length of the hang
	is specified by <code>deadTimeAll</code>.
	If set to <code>0</code>, clears the persistent deadlock condition without
	deadlocking due to it.
	The default value is to make no change in the persistent deadlock condition.
	</DD>

</DL>

<H2>simpleSleep</H2>

<P><A name="simpleSleep"></A><A href="simpleSleep">This</A>
is a very simple servlet that just tries to sleep
for 100 milliseconds.  It has none of the fancy
features of the servlets listed above.
</P>

<H2>GC</H2>

<P><A name="GC"></A><A href="GC">This</A>
is a very simple servlet that just invokes a full garbage collection.
</P>

<H2>bbread.jsp</H2>

<P><A name="bbread"></A>Click <A href="bbread.jsp">here</A>
to see it.  This JSP helps inspect Bulletin Board contents.
Give it the name of a Bulletin Board and a subject,
and it will read the current contents.
</P>

<H2>coregroup.jsp</H2>

<P><A name="coregroup"></A>Click <A href="coregroup.jsp">here</A>
for an example.  This JSP helps debug DCS core group problems.
It is best run on the dmgr; running it on another server
causes it to reach only the HAManager MBean on that server
(Brian is working on a better version that does not have this limitation).</P>

<P>This JSP
lists all the HAManager MBeans and core group views.
The output consists of one table containing all the HAManager MBeans,
followed by a table per MBean listing its view of the core group.
Such a view table has a left half that identifies the MBean,
and a right half holding the view members.</P>

<P>Following is
an example of good output.  It is good because for every WAS process in the cell:
(1) there is a row in the first table, which lists all the HAManager MBeans;
(2) there is a table after the first, in which the process is identified in the left half; and
(3) each of those tables lists all the WAS processes in the right half.
</P>

<table border="3">
<TR><TD>

<table border="1">
<tr><td>WebSphere:cell=eutil19Network,coregroup=DefaultCoreGroup,name=HAManager,mbeanIdentifier=HAManager,type=HAManager,node=eutil14,process=nodeagent</td></tr>
<tr><td>WebSphere:cell=eutil19Network,coregroup=DefaultCoreGroup,name=HAManager,mbeanIdentifier=HAManager,type=HAManager,node=eutil16,process=TestClusterA_eutil16</td></tr>
<tr><td>WebSphere:cell=eutil19Network,coregroup=DefaultCoreGroup,name=HAManager,mbeanIdentifier=HAManager,type=HAManager,node=eutil13,process=nodeagent</td></tr>
<tr><td>WebSphere:cell=eutil19Network,coregroup=DefaultCoreGroup,name=HAManager,mbeanIdentifier=HAManager,type=HAManager,node=eutil19Manager,process=dmgr</td></tr>
<tr><td>WebSphere:cell=eutil19Network,coregroup=DefaultCoreGroup,name=HAManager,mbeanIdentifier=HAManager,type=HAManager,node=eutil11,process=TestClusterA_eutil11</td></tr>
<tr><td>WebSphere:cell=eutil19Network,coregroup=DefaultCoreGroup,name=HAManager,mbeanIdentifier=HAManager,type=HAManager,node=eutil11,process=nodeagent</td></tr>
<tr><td>WebSphere:cell=eutil19Network,coregroup=DefaultCoreGroup,name=HAManager,mbeanIdentifier=HAManager,type=HAManager,node=eutil18,process=nodeagent</td></tr>
<tr><td>WebSphere:cell=eutil19Network,coregroup=DefaultCoreGroup,name=HAManager,mbeanIdentifier=HAManager,type=HAManager,node=eutil17,process=odr</td></tr>
<tr><td>WebSphere:cell=eutil19Network,coregroup=DefaultCoreGroup,name=HAManager,mbeanIdentifier=HAManager,type=HAManager,node=eutil17,process=nodeagent</td></tr>
<tr><td>WebSphere:cell=eutil19Network,coregroup=DefaultCoreGroup,name=HAManager,mbeanIdentifier=HAManager,type=HAManager,node=eutil16,process=nodeagent</td></tr>
</table>
<br>
<table border="1"
><tr><td>eutil14/nodeagent</td><td><table>
<tr><td>eutil19Network\eutil11\TestClusterA_eutil11</td></tr>
<tr><td>eutil19Network\eutil11\nodeagent</td></tr>
<tr><td>eutil19Network\eutil13\nodeagent</td></tr>
<tr><td>eutil19Network\eutil14\nodeagent</td></tr>
<tr><td>eutil19Network\eutil16\TestClusterA_eutil16</td></tr>
<tr><td>eutil19Network\eutil16\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\odr</td></tr>
<tr><td>eutil19Network\eutil18\nodeagent</td></tr>
<tr><td>eutil19Network\eutil19Manager\dmgr</td></tr>
</table></td></tr>
<br>
<table border="1"
><tr><td>eutil16/TestClusterA_eutil16</td><td><table>
<tr><td>eutil19Network\eutil11\TestClusterA_eutil11</td></tr>
<tr><td>eutil19Network\eutil11\nodeagent</td></tr>
<tr><td>eutil19Network\eutil13\nodeagent</td></tr>
<tr><td>eutil19Network\eutil14\nodeagent</td></tr>
<tr><td>eutil19Network\eutil16\TestClusterA_eutil16</td></tr>
<tr><td>eutil19Network\eutil16\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\odr</td></tr>
<tr><td>eutil19Network\eutil18\nodeagent</td></tr>
<tr><td>eutil19Network\eutil19Manager\dmgr</td></tr>
</table></td></tr>
<br>
<table border="1"
><tr><td>eutil13/nodeagent</td><td><table>
<tr><td>eutil19Network\eutil11\TestClusterA_eutil11</td></tr>
<tr><td>eutil19Network\eutil11\nodeagent</td></tr>
<tr><td>eutil19Network\eutil13\nodeagent</td></tr>
<tr><td>eutil19Network\eutil14\nodeagent</td></tr>
<tr><td>eutil19Network\eutil16\TestClusterA_eutil16</td></tr>
<tr><td>eutil19Network\eutil16\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\odr</td></tr>
<tr><td>eutil19Network\eutil18\nodeagent</td></tr>
<tr><td>eutil19Network\eutil19Manager\dmgr</td></tr>
</table></td></tr>
<br>
<table border="1"
><tr><td>eutil19Manager/dmgr</td><td><table>
<tr><td>eutil19Network\eutil11\TestClusterA_eutil11</td></tr>
<tr><td>eutil19Network\eutil11\nodeagent</td></tr>
<tr><td>eutil19Network\eutil13\nodeagent</td></tr>
<tr><td>eutil19Network\eutil14\nodeagent</td></tr>
<tr><td>eutil19Network\eutil16\TestClusterA_eutil16</td></tr>
<tr><td>eutil19Network\eutil16\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\odr</td></tr>
<tr><td>eutil19Network\eutil18\nodeagent</td></tr>
<tr><td>eutil19Network\eutil19Manager\dmgr</td></tr>
</table></td></tr>
<br>
<table border="1"
><tr><td>eutil11/TestClusterA_eutil11</td><td><table>
<tr><td>eutil19Network\eutil11\TestClusterA_eutil11</td></tr>
<tr><td>eutil19Network\eutil11\nodeagent</td></tr>
<tr><td>eutil19Network\eutil13\nodeagent</td></tr>
<tr><td>eutil19Network\eutil14\nodeagent</td></tr>
<tr><td>eutil19Network\eutil16\TestClusterA_eutil16</td></tr>
<tr><td>eutil19Network\eutil16\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\odr</td></tr>
<tr><td>eutil19Network\eutil18\nodeagent</td></tr>
<tr><td>eutil19Network\eutil19Manager\dmgr</td></tr>
</table></td></tr>
<br>
<table border="1"
><tr><td>eutil11/nodeagent</td><td><table>
<tr><td>eutil19Network\eutil11\TestClusterA_eutil11</td></tr>
<tr><td>eutil19Network\eutil11\nodeagent</td></tr>
<tr><td>eutil19Network\eutil13\nodeagent</td></tr>
<tr><td>eutil19Network\eutil14\nodeagent</td></tr>
<tr><td>eutil19Network\eutil16\TestClusterA_eutil16</td></tr>
<tr><td>eutil19Network\eutil16\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\odr</td></tr>
<tr><td>eutil19Network\eutil18\nodeagent</td></tr>
<tr><td>eutil19Network\eutil19Manager\dmgr</td></tr>
</table></td></tr>
<br>
<table border="1"
><tr><td>eutil18/nodeagent</td><td><table>
<tr><td>eutil19Network\eutil11\TestClusterA_eutil11</td></tr>
<tr><td>eutil19Network\eutil11\nodeagent</td></tr>
<tr><td>eutil19Network\eutil13\nodeagent</td></tr>
<tr><td>eutil19Network\eutil14\nodeagent</td></tr>
<tr><td>eutil19Network\eutil16\TestClusterA_eutil16</td></tr>
<tr><td>eutil19Network\eutil16\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\odr</td></tr>
<tr><td>eutil19Network\eutil18\nodeagent</td></tr>
<tr><td>eutil19Network\eutil19Manager\dmgr</td></tr>
</table></td></tr>
<br>
<table border="1"
><tr><td>eutil17/odr</td><td><table>
<tr><td>eutil19Network\eutil11\TestClusterA_eutil11</td></tr>
<tr><td>eutil19Network\eutil11\nodeagent</td></tr>
<tr><td>eutil19Network\eutil13\nodeagent</td></tr>
<tr><td>eutil19Network\eutil14\nodeagent</td></tr>
<tr><td>eutil19Network\eutil16\TestClusterA_eutil16</td></tr>
<tr><td>eutil19Network\eutil16\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\odr</td></tr>
<tr><td>eutil19Network\eutil18\nodeagent</td></tr>
<tr><td>eutil19Network\eutil19Manager\dmgr</td></tr>
</table></td></tr>
<br>
<table border="1"
><tr><td>eutil17/nodeagent</td><td><table>
<tr><td>eutil19Network\eutil11\TestClusterA_eutil11</td></tr>
<tr><td>eutil19Network\eutil11\nodeagent</td></tr>
<tr><td>eutil19Network\eutil13\nodeagent</td></tr>
<tr><td>eutil19Network\eutil14\nodeagent</td></tr>
<tr><td>eutil19Network\eutil16\TestClusterA_eutil16</td></tr>
<tr><td>eutil19Network\eutil16\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\odr</td></tr>
<tr><td>eutil19Network\eutil18\nodeagent</td></tr>
<tr><td>eutil19Network\eutil19Manager\dmgr</td></tr>
</table></td></tr>
<br>
<table border="1"
><tr><td>eutil16/nodeagent</td><td><table>
<tr><td>eutil19Network\eutil11\TestClusterA_eutil11</td></tr>
<tr><td>eutil19Network\eutil11\nodeagent</td></tr>
<tr><td>eutil19Network\eutil13\nodeagent</td></tr>
<tr><td>eutil19Network\eutil14\nodeagent</td></tr>
<tr><td>eutil19Network\eutil16\TestClusterA_eutil16</td></tr>
<tr><td>eutil19Network\eutil16\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\nodeagent</td></tr>
<tr><td>eutil19Network\eutil17\odr</td></tr>
<tr><td>eutil19Network\eutil18\nodeagent</td></tr>
<tr><td>eutil19Network\eutil19Manager\dmgr</td></tr>
</table></td></tr>
</table>

</TD></TR>
</table>

</BODY>
</HTML>
