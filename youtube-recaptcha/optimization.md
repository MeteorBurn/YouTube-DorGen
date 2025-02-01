---
order: 4.5
title: ♾️Оптимизация
---

#### 3️⃣ Тюнинг TCP-стека для оптимизации и работы шаблона **YouTube-ReCaptcha на выделенных физических серверах под управлением Windows Server.**

#### Базовая настройка TCP **–** `tcp_general`

Эта конфигурация **ускоряет работу сети**, увеличивая количество доступных соединений, уменьшая задержки и улучшая передачу данных. Windows начинает **быстрее устанавливать и поддерживать соединения**, что полезно для активного сетевого использования.

```PowerShell
Windows Registry Editor Version 5.00
; General TCP/IP optimization settings
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters]
"MaxUserPort"=dword:65534         ; Increases the available port range
"TcpNumConnections"=dword:16777214 ; Allows maximum number of TCP connections
"TcpTimedWaitDelay"=dword:30       ; Reduces time for closing connections (30 seconds instead of 240)
"TcpMaxDataRetransmissions"=dword:3  ; Reduces TCP retransmissions
; TCP window size optimization
"TcpWindowSize"=dword:1048576      ; Increases TCP window size to 1MB
"DefaultSendWindow"=dword:1048576  ; Increases send window size
; ACK and Keep-Alive settings
"TcpNoDelay"=dword:1               ; Disables Nagle Algorithm (improves responsiveness for small packets)
"TcpAckFrequency"=dword:1          ; Sends ACK for every received packet (reduces latency)
"TcpDelAckTicks"=dword:1           ; Reduces delay for sending ACKs
"KeepAliveTime"=dword:30000        ; Reduces Keep-Alive timeout to 30 seconds
"KeepAliveInterval"=dword:1000     ; Sets Keep-Alive interval to 1 second
```

#### **Оптимизация сетевой карты –** `tcp_network_adapter`

Настройка сетевого адаптера для **максимальной скорости и стабильности**. Эта конфигурация увеличивает размер пакетов, снижает задержки, улучшает буферизацию данных. Требуется вручную указать **GUID сетевого адаптера**, чтобы настройки применились к нужному устройству.

Чтобы узнать GUID активного сетевого адаптера в Powershell  необходимо выполнить команду:

```PowerShell
Get-NetAdapter | Where-Object { $_.Status -eq 'Up' } | Select-Object Name, InterfaceGuid
```

И затем заменить `{YOUR_ADAPTER_GUID}`на полученный **GUID.**

```PowerShell
Windows Registry Editor Version 5.00
; Network adapter optimization settings
; Replace {YOUR_ADAPTER_GUID} with the actual GUID of your network adapter.
; The format should be: {D4F58A9E-6A57-4B12-A2B3-5CDA98B6F9E1}
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\{YOUR_ADAPTER_GUID}]
"MTU"=dword:1500                  ; Sets maximum packet size (MTU)
"TcpAckFrequency"=dword:1          ; Reduces latency by acknowledging packets faster
; Memory management optimizations
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management]
"LargeSystemCache"=dword:1
"IOPageLockLimit"=dword:262144      ; Increases memory page lock limit to 256KB
```

#### **Отключение ограничений Windows –** `tcp_security`  

Windows ограничивает скорость соединений – эта конфигурация **убирает эти ограничения**. Это позволяет **создавать больше подключений одновременно** и быстрее передавать данные. Особенно важно для серверов, где используются программы, которые отправлюят и принимают множество HTTP-запросов.

```PowerShell
Windows Registry Editor Version 5.00
; Removing Windows network restrictions
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters]
"EnableConnectionRateLimiting"=dword:0  ; Disables connection rate limiting
"SynAttackProtect"=dword:0         ; Disables SYN attack protection (useful for high outgoing connections)
"EnableDynamicBacklog"=dword:1     ; Enables automatic scaling of connection backlog
"MinimumDynamicBacklog"=dword:20   ; Sets minimum number of pending connections
"MaximumDynamicBacklog"=dword:20000 ; Sets maximum number of pending connections
"DynamicBacklogGrowthDelta"=dword:100 ; Defines the rate at which backlog grows
```

#### **Продвинутая настройка сети –** `tcp_advanced` 

Эти команды вносят изменения через `netsh` и `PowerShell`, отключая функции, которые **мешают быстродействию сети**. Отключает задержки обработки пакетов, экономию энергии на сетевой карте и включает авто-настройку TCP для лучшей пропускной способности.

```PowerShell
netsh int tcp set heuristics wsh=disabled forcews=enabled; if ($LASTEXITCODE -ne 0) { Write-Host "Error: Heuristics" -ForegroundColor Red }

netsh int tcp set global autotuninglevel=normal; if ($LASTEXITCODE -ne 0) { Write-Host "Error: Auto-Tuning" -ForegroundColor Red }

netsh int tcp set global rsc=disabled; if ($LASTEXITCODE -ne 0) { Write-Host "Error: RSC" -ForegroundColor Red }

Get-NetAdapter | Where-Object { $_.Status -eq 'Up' -and $_.PhysicalMediaType -ne '802.3' -and $_.InterfaceDescription -notmatch 'VPN|Virtual' } | Disable-NetAdapterBinding -ComponentID ms_tcpip

Get-NetAdapter | Where-Object { $_.Status -eq 'Up' -and $_.PhysicalMediaType -ne '802.3' -and $_.InterfaceDescription -notmatch 'VPN|Virtual' } | Set-NetAdapterAdvancedProperty -RegistryKeyword '*InterruptModeration' -RegistryValue 0

Get-NetAdapter | Where-Object { $_.Status -eq 'Up' -and $_.PhysicalMediaType -ne '802.3' -and $_.InterfaceDescription -notmatch 'VPN|Virtual' } | Set-NetAdapterAdvancedProperty -RegistryKeyword '*EEE' -RegistryValue 0
```