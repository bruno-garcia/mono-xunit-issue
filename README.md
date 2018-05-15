Mono 5.12 running tests targeting .NET 4.7.2 fail with:

```shell
$ uname -a
Linux Tampere 4.4.0-17134-Microsoft #48-Microsoft Fri Apr 27 18:06:00 PST 2018 x86_64 x86_64 x86_64 GNU/Linux

$ mono --version
Mono JIT compiler version 5.12.0.226 (tarball Thu May  3 09:48:32 UTC 2018)
Copyright (C) 2002-2014 Novell, Inc, Xamarin Inc and Contributors. www.mono-project.com
        TLS:           __thread
        SIGSEGV:       altstack
        Notifications: epoll
        Architecture:  amd64
        Disabled:      none
        Misc:          softdebug
        Interpreter:   yes
        LLVM:          supported, not enabled.
        GC:            sgen (concurrent by default)

$ dotnet test
Build started, please wait...
Build completed.

Test run for /mnt/c/Users/bruno/git/mono-xunit-issue/bin/Debug/net47/mono-xunit-issue.dll(.NETFramework,Version=v4.7)
Microsoft (R) Test Execution Command Line Tool Version 15.7.0-preview-20180221-13
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
[xUnit.net 00:00:01.8591040] mono-xunit-issue: Catastrophic failure: System.NullReferenceException: Object reference not set to an instance of an object


Server stack trace:
  at System.Runtime.Remoting.ClientIdentity.get_ClientProxy () [0x00000] in <71d8ad678db34313b7f718a414dfcb25>:0
  at System.Runtime.Remoting.RemotingServices.GetOrCreateClientIdentity (System.Runtime.Remoting.ObjRef objRef, System.Type proxyType, System.Object& clientProxy) [0x00068] in <71d8ad678db34313b7f718a414dfcb25>:0
  at System.Runtime.Remoting.RemotingServices.GetRemoteObject (System.Runtime.Remoting.ObjRef objRef, System.Type proxyType) [0x00000] in <71d8ad678db34313b7f718a414dfcb25>:0
  at System.Runtime.Remoting.RemotingServices.GetProxyForRemoteObject (System.Runtime.Remoting.ObjRef objref, System.Type classToProxy) [0x0001b] in <71d8ad678db34313b7f718a414dfcb25>:0
  at System.Runtime.Remoting.RemotingServices.Unmarshal (System.Runtime.Remoting.ObjRef objectRef, System.Boolean fRefine) [0x0007a] in <71d8ad678db34313b7f718a414dfcb25>:0
  at System.Runtime.Remoting.RemotingServices.Unmarshal (System.Runtime.Remoting.ObjRef objectRef) [0x00000] in <71d8ad678db34313b7f718a414dfcb25>:0
  at System.Runtime.Remoting.Messaging.CADMessageBase.UnmarshalArgument (System.Object arg, System.Collections.ArrayList args) [0x0003d] in <71d8ad678db34313b7f718a414dfcb25>:0
  at System.Runtime.Remoting.Messaging.CADMessageBase.UnmarshalArguments (System.Object[] arguments, System.Collections.ArrayList args) [0x00011] in <71d8ad678db34313b7f718a414dfcb25>:0
  at System.Runtime.Remoting.Messaging.CADMethodCallMessage.GetArgs (System.Collections.ArrayList args) [0x00000] in <71d8ad678db34313b7f718a414dfcb25>:0
  at System.Runtime.Remoting.Messaging.MethodCall..ctor (System.Runtime.Remoting.Messaging.CADMethodCallMessage msg) [0x0001e] in <71d8ad678db34313b7f718a414dfcb25>:0
  at System.AppDomain.ProcessMessageInDomain (System.Byte[] arrRequest, System.Runtime.Remoting.Messaging.CADMethodCallMessage cadMsg, System.Byte[]& arrResponse, System.Runtime.Remoting.Messaging.CADMethodReturnMessage& cadMrm) [0x00012] in <71d8ad678db34313b7f718a414dfcb25>:0
  at (wrapper remoting-invoke-with-check) System.AppDomain.ProcessMessageInDomain(byte[],System.Runtime.Remoting.Messaging.CADMethodCallMessage,byte[]&,System.Runtime.Remoting.Messaging.CADMethodReturnMessage&)
  at System.Runtime.Remoting.Channels.CrossAppDomainSink.ProcessMessageInDomain (System.Byte[] arrRequest, System.Runtime.Remoting.Messaging.CADMethodCallMessage cadMsg) [0x0000d] in <71d8ad678db34313b7f718a414dfcb25>:0

Exception rethrown at [0]:
  at (wrapper managed-to-native) System.Object.__icall_wrapper_mono_remoting_wrapper(intptr,intptr)
  at (wrapper remoting-invoke) Xunit.Sdk.TestFrameworkExecutor`1[Xunit.Sdk.IXunitTestCase].RunTests(System.Collections.Generic.IEnumerable`1<Xunit.Abstractions.ITestCase>,Xunit.Abstractions.IMessageSink,Xunit.Abstractions.ITestFrameworkExecutionOptions)
  at (wrapper xdomain-invoke) Xunit.Sdk.TestFrameworkExecutor`1[Xunit.Sdk.IXunitTestCase].RunTests(System.Collections.Generic.IEnumerable`1<Xunit.Abstractions.ITestCase>,Xunit.Abstractions.IMessageSink,Xunit.Abstractions.ITestFrameworkExecutionOptions)
  at Xunit.Xunit2.RunTests (System.Collections.Generic.IEnumerable`1[T] testCases, Xunit.Abstractions.IMessageSink messageSink, Xunit.Abstractions.ITestFrameworkExecutionOptions executionOptions) [0x0000e] in <76951d54e5564f89923967e66e39e57a>:0
  at Xunit.XunitFrontController.RunTests (System.Collections.Generic.IEnumerable`1[T] testMethods, Xunit.Abstractions.IMessageSink messageSink, Xunit.Abstractions.ITestFrameworkExecutionOptions executionOptions) [0x00006] in <76951d54e5564f89923967e66e39e57a>:0
  at TestFrameworkExtensions.RunTests (Xunit.Abstractions.ITestFrameworkExecutor executor, System.Collections.Generic.IEnumerable`1[T] testCases, Xunit.IMessageSinkWithTypes executionMessageSink, Xunit.Abstractions.ITestFrameworkExecutionOptions executionOptions) [0x00008] in <76951d54e5564f89923967e66e39e57a>:0
  at Xunit.Runner.VisualStudio.VsTestRunner.RunTestsInAssembly (Microsoft.VisualStudio.TestPlatform.ObjectModel.Adapter.IRunContext runContext, Microsoft.VisualStudio.TestPlatform.ObjectModel.Adapter.IFrameworkHandle frameworkHandle, LoggerHelper logger, Xunit.Runner.VisualStudio.TestPlatformContext testPlatformContext, Xunit.IMessageSinkWithTypes reporterMessageHandler, Xunit.Runner.VisualStudio.AssemblyRunInfo runInfo) [0x00505] in <587845cbc5794887a177d25dc93c0b6a>:0

Test Run Failed.
```