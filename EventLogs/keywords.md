 - **PowerShell script** to list all event log *'keywords'* 

        try{$v = @((Get-WinEvent -Listprovider *  -ErrorAction SilentlyContinue ).events.keywords) }
        catch{$v=$null}
        write-host "found $($v.count) entries"

        $val = @(foreach($i in $v) {
             if($i -ne $null){           
            [PSCustomObject]@{
                name = $i.name
                value_hex = "0x"+'{0:x16}'-f $i.value
                value_decimal= $i.value
                displayname = $i.displayname
            }
          }
        })|sort-object -Property value_decimal -unique  

        # write output to text file
        # otherwise just replace the next 2 lines with $val

        $out = foreach ($x in $val){"|$($x.name) | $($x.value_hex) | $($x.value_decimal) | $($x.displayname)"} 
        $out|out-file D:\keywall.txt -append


  - **Output:**
  
    | **Name** | **Hex Value** | **Decimal Value** | **Display Name**
    | -----: | :-----: | -----: | :----- 
    |Base | 0x0000000000000001 | 1 |  
    |Performance | 0x0000000000000002 | 2 | Performance 
    |Tasks | 0x0000000000000004 | 4 |  
    |Trigger | 0x0000000000000008 | 8 |  
    |ETW_KEYWORD_SESSION | 0x0000000000000010 | 16 | Session 
    |Warning | 0x0000000000000020 | 32 | Warning 
    |WFTracking | 0x0000000000000040 | 64 | WF Tracking 
    |ut:TcpipDiagnosis | 0x0000000000000080 | 128 |  
    |USER_LOADER_KEYWORD COMPONENT_ON_DEMAND | 0x0000000000000100 | 256 | Windows component on demand. 
    |DxgKrnl_Power | 0x0000000000000200 | 512 |  
    |RotationManager | 0x0000000000000400 | 1024 | CUI RotationManager 
    |StationId | 0x0000000000000800 | 2048 | StationId 
    |Rendering | 0x0000000000001000 | 4096 |  
    |HWVerifyHub | 0x0000000000002000 | 8192 |  
    |PLM | 0x0000000000004000 | 16384 | Lifetime Manager 
    |RoutingServices | 0x0000000000008000 | 32768 | Routing Services 
    |Shell | 0x0000000000010000 | 65536 |  
    |CSM | 0x0000000000020000 | 131072 | Crawl Scope Manager 
    |Streaming | 0x0000000000040000 | 262144 | Streaming 
    |APPXDEPLOYMENTSERVER PERF_KEYWORD | 0x0000000000080000 | 524288 | AppXDeploymentServerPerf Keyword 
    |ExecSelfHostCritical | 0x0000000000100000 | 1048576 | SelfHost Critical 
    |ExecDevPlatCircular | 0x0000000000200000 | 2097152 | DevPlat Circular 
    |Write | 0x0000000000400000 | 4194304 | Write request 
    |tabhydration | 0x0000000000800000 | 8388608 |  
    |WFRuntime | 0x0000000001000000 | 16777216 | Workflow Runtime 
    |LowMemoryRead | 0x0000000002000000 | 33554432 | Low memory Read request 
    |StartupPerf | 0x0000000004000000 | 67108864 |  
    |StructuredQuery | 0x0000000008000000 | 134217728 |  
    |ViewManager | 0x0000000010000000 | 268435456 | OneCore CUI ViewManager 
    |animation | 0x0000000020000000 | 536870912 |  
    |IOCTL | 0x0000000040000000 | 1073741824 | Device I/O control request 
    |composition_verbose | 0x0000000080000000 | 2147483648 |  
    |MessagingPerformance | 0x0000000100000000 | 4294967296 | CoreMessaging MessagingPerformance 
    |Keyword.RECEIVE | 0x0000000200000000 | 8589934592 | RECEIVE 
    |debug | 0x0000000400000000 | 17179869184 | Debug events 
    |DCompDetails | 0x0000000800000000 | 34359738368 |  
    |CommsService | 0x0000001000000000 | 68719476736 | CommsService 
    |ut:Authentication | 0x0000002000000000 | 137438953472 |  
    |Warning | 0x0000004000000000 | 274877906944 |  
    |StateTransition | 0x0000008000000000 | 549755813888 |  
    |ut:Dropped | 0x0000010000000000 | 1099511627776 |  
    |ut:PiiPresent | 0x0000020000000000 | 2199023255552 |  
    |WININET_KEYWORD_PACKET | 0x0000040000000000 | 4398046511104 | Flagged on all WinINet events dealing with packet capture 
    |SelfHostError | 0x0000080000000000 | 8796093022208 | CoreMessaging SelfHostError 
    |Messages | 0x0000100000000000 | 17592186044416 |  
    |ut:StateTransition | 0x0000200000000000 | 35184372088832 |  
    |ms:Measures | 0x0000400000000000 | 70368744177664 |  
    |WinRTCaptureEngine | 0x0000800000000000 | 140737488355328 |  
    |win:ResponseTime | 0x0001000000000000 | 281474976710656 | Response Time 
    |win:ReservedKeyword49 | 0x0002000000000000 | 562949953421312 |  
    |win:WDIDiag | 0x0004000000000000 | 1125899906842624 | WDI Diag 
    |win:SQM | 0x0008000000000000 | 2251799813685248 | SQM 
    |win:AuditFailure | 0x0010000000000000 | 4503599627370496 | Audit Failure 
    |win:AuditSuccess | 0x0020000000000000 | 9007199254740992 | Audit Success 
    |win:EventlogClassic | 0x0080000000000000 | 36028797018963968 | Classic 
    | | 0x0100000000000000 | 72057594037927936 |  
    | | 0x0200000000000000 | 144115188075855872 |  
    | | 0x0400000000000000 | 288230376151711744 |  
    | | 0x0800000000000000 | 576460752303423488 |  
    | | 0x1000000000000000 | 1152921504606846976 |  
    | | 0x2000000000000000 | 2305843009213693952 |  
    | | 0x4000000000000000 | 4611686018427387904 |  
    | | 0x8000000000000000 | -9223372036854775808 |      

     
  - Known keywords ( [source](https://www.geoffchappell.com/notes/windows/shell/events/core.htm))
   
    | **Name** | **Hex Value** | **Decimal Value** | **Display Name**
    |  -----: | :-----: | -----: | :-----    
    |  | 0x0000000000010000 | | Shell 
    |  | 0x0000000000020000 | |  Properties 
    |  | 0x0000000000040000 | |  FileClassStoreAndIconCache 
    |  | 0x0000000000080000 | |  Controls 
    |  | 0x0000000000100000 | |  APICalls'
    |  | 0x0000000000200000 | |  InternetExplorer
    |  | 0x0000000000400000 | |  ShutdownUX 
    |  | 0x0000000000800000 | |  CopyEngine 
    |  | 0x0000000001000000 | |  Tasks
    |  | 0x0000000002000000 | |  WDI 
    |  | 0x0000000004000000 | |  StartupPerf 
    |  | 0x0000000008000000 | |  StructuredQuery 
    |  | 0x0008000000000000 | |  win:SQM 
    |  | 0x8000000000000000 | |  Microsoft-Windows-Shell-Core/Diagnostic 
