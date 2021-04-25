---
layout: single
title: "Hyper-V 가상 컴퓨터의 VHD확인"
description: "PowerShell을 사용하여 Hyper-V의 가상 컴퓨터의 VHD확인"
categories: [Windows]
tags: [Windows, Powershell, Hyper-V]
redirect_from:
  - /2021/04/25/
---
# PowerShell을 사용하여 Hyper-V 가상 컴퓨터의 VHD확인
VM 개수가 많아질 때 어떤 VHD 파일을 쓰는지, 유형은 어떻고 부모 디스크는 무엇인지 확인하고 싶은 경우 이용할 수 있는 명령입니다.

## 명령어
Powershell에서 다음과 같이 입력합니다.
```powershell
Get-VM * -pv VM | %{get-vhd -VMId $_.Id} | Format-Table @{n='Name';e={$VM.Name}}, VhdType, Path, ParentPath -A
```
출력 예:
```powershell
PS D:> Get-VM * -pv VM | %{get-vhd -VMId $_.Id} | Format-Table @{n='Name';e={$VM.Name}}, VhdType, Path

Name                 VhdType Path
----                 ------- ----
WIN10L          Differencing D:\Hyper-V\WIN10L\Virtual Hard Disks\Win10L.vhdx
DHCP01-Client        Dynamic D:\Hyper-V\DHCP01\Virtual Hard Disks\DHCP01.vhdx
K9AD01          Differencing D:\Hyper-V\K9AD01\Virtual Hard Disks\AD19_44DBC95B-5C8C-4ABF-A0F0-43DD432154C3.avhdx
```

## 참고URL
- https://mikefrobbins.com/2013/07/18/use-powershell-to-determine-the-chain-of-vhds-for-a-virtual-machine-on-hyper-v/
- https://rkeithhill.wordpress.com/2013/07/20/powershell-v4-pipelinevariable-common-parameter/
