内存溢出错误：
```
<--- Last few GCs --->

[78352:0x105000000]     8502 ms: Mark-sweep 1394.6 (1401.2) -> 1394.6 (1401.2) MB, 5.9 / 0.0 ms  (average mu = 0.302, current mu = 0.004) last resort GC in old space requested
[78352:0x105000000]     8508 ms: Mark-sweep 1394.6 (1401.2) -> 1394.6 (1401.2) MB, 5.9 / 0.0 ms  (average mu = 0.181, current mu = 0.003) last resort GC in old space requested


<--- JS stacktrace --->

==== JS stack trace =========================================

    0: ExitFrame [pc: 0x261682ecfc7d]
Security context: 0x36ccf8c53d51 <JSObject>
    1: substring [0x36cc6daf6dc1](this=0x36cc6061cca1 <Very long string[6453527]>,0,4413898)
    2: /* anonymous */ [0x36cc2d26ab71] [/Users/zhanglin/svn/PP/BOSPadProject/bundler/bin/vendor/diff_match_patch.js:36] [bytecode=0x36cc6dadafa1 offset=477](this=0x36cc373b1641 <diff_match_patch map = 0x36ccd05c5231>,0x36cc6061cd99 <JSObject>,0x36cc6dadeb39 <JSArray...

FATAL ERROR: CALL_AND_RETRY_LAST Allocation failed - JavaScript heap out of memory

Writing Node.js report to file: report.20190812.160910.78352.001.json
Node.js report completed
 1: 0x10006313d node::Abort() [/Users/zhanglin/.nvm/versions/node/v11.8.0/bin/node]
 2: 0x100063894 node::OnFatalError(char const*, char const*) [/Users/zhanglin/.nvm/versions/node/v11.8.0/bin/node]
 3: 0x1001a5ca7 v8::Utils::ReportOOMFailure(v8::internal::Isolate*, char const*, bool) [/Users/zhanglin/.nvm/versions/node/v11.8.0/bin/node]
 4: 0x1001a5c44 v8::internal::V8::FatalProcessOutOfMemory(v8::internal::Isolate*, char const*, bool) [/Users/zhanglin/.nvm/versions/node/v11.8.0/bin/node]
 5: 0x1005aada2 v8::internal::Heap::FatalProcessOutOfMemory(char const*) [/Users/zhanglin/.nvm/versions/node/v11.8.0/bin/node]
 6: 0x1005b4384 v8::internal::Heap::AllocateRawWithRetryOrFail(int, v8::internal::AllocationSpace, v8::internal::AllocationAlignment) [/Users/zhanglin/.nvm/versions/node/v11.8.0/bin/node]
 7: 0x100585bd5 v8::internal::Factory::NewRawOneByteString(int, v8::internal::PretenureFlag) [/Users/zhanglin/.nvm/versions/node/v11.8.0/bin/node]
 8: 0x1006cd1d0 v8::internal::String::SlowFlatten(v8::internal::Isolate*, v8::internal::Handle<v8::internal::ConsString>, v8::internal::PretenureFlag) [/Users/zhanglin/.nvm/versions/node/v11.8.0/bin/node]
 9: 0x100587eee v8::internal::Factory::NewProperSubString(v8::internal::Handle<v8::internal::String>, int, int) [/Users/zhanglin/.nvm/versions/node/v11.8.0/bin/node]
10: 0x10087e170 v8::internal::Runtime_StringSubstring(int, v8::internal::Object**, v8::internal::Isolate*) [/Users/zhanglin/.nvm/versions/node/v11.8.0/bin/node]
11: 0x261682ecfc7d 
Abort trap: 6
```

解决办法
```
node --max-old-space-size=4096  bundler/bin/index.js diff
```
