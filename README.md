# Internet Status Indicator Startup Script

[![Platform](https://img.shields.io/badge/platform-Windows-blue.svg)](https://www.microsoft.com/en-us/windows)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-brightgreen.svg)](https://github.com/almas-cp/internet-status-indicator/graphs/commit-activity)

This repository hosts a PowerShell one-liner script that automates the setup and execution of the Internet Status Indicator during Windows startup.

## Overview

When executed, the script performs the following tasks:
- **Administrator Privilege Check:**  
  It verifies if the script is running with administrator privileges and, if not, re-launches itself in an elevated window.
- **Console Configuration:**  
  Uses the legacy `mode con:` command to set the console dimensions to 120 columns and 50 lines.
- **Startup Folder Navigation:**  
  Changes the working directory to `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup` so the script integrates with Windows startup.
- **Display of ASCII Art:**  
  Shows an ASCII art banner crediting the author.
- **Downloading and Executing the Application:**  
  Downloads the Internet Status Indicator executable from GitHub and runs it.
- **User Guidance:**  
  Instructs the user to check the Windows system tray for the indicator icon and to reposition it if needed.
- **Script Termination:**  
  Waits for a key press before exiting to ensure the user has read all information.

## Prerequisites

- **Operating System:** Windows 10 or later.
- **PowerShell:** Must be executed in an elevated (Administrator) mode.
- **Internet Connection:** Required to download the executable from GitHub.
- **User Permissions:** The script automatically relaunches itself with administrator rights if not already elevated.

## Usage

1. **Copy and Execute:**  
   Copy the one-liner command below and paste it into an elevated PowerShell console, or save it as a `.ps1` file and execute it.

2. **One-Liner Command:**

   ```powershell
   if (-NOT ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole]"Administrator")) {Start-Process powershell "-NoProfile -ExecutionPolicy Bypass -Command `"$($MyInvocation.MyCommand.Definition)`"" -Verb RunAs -WindowStyle Maximized; exit}; mode con: cols=120 lines=50; Set-Location "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup"; try {Clear-Host; Write-Host "██╗███╗░░██╗████████╗███████╗██████╗░███╗░░██╗███████╗████████╗  ░██████╗████████╗░█████╗░████████╗██╗░░░██╗░██████╗" -ForegroundColor Cyan; Write-Host "██║████╗░██║╚══██╔══╝██╔════╝██╔══██╗████╗░██║██╔════╝╚══██╔══╝  ██╔════╝╚══██╔══╝██╔══██╗╚══██╔══╝██║░░░██║██╔════╝" -ForegroundColor Cyan; Write-Host "██║██╔██╗██║░░░██║░░░█████╗░░██████╔╝██╔██╗██║█████╗░░░░░██║░░░  ╚█████╗░░░░██║░░░███████║░░░██║░░░██║░░░██║╚█████╗░" -ForegroundColor Cyan; Write-Host "██║██║╚████║░░░██║░░░██╔══╝░░██╔══██╗██║╚████║██╔══╝░░░░░██║░░░  ░╚═══██╗░░░██║░░░██╔══██║░░░██║░░░██║░░░██║░╚═══██╗" -ForegroundColor Cyan; Write-Host "██║██║░╚███║░░░██║░░░███████╗██║░░██║██║░╚███║███████╗░░░██║░░░  ██████╔╝░░░██║░░░██║░░██║░░░██║░░░╚██████╔╝██████╔╝" -ForegroundColor Cyan; Write-Host "╚═╝╚═╝░░╚══╝░░░╚═╝░░░╚══════╝╚═╝░░╚═╝╚═╝░░╚══╝╚══════╝░░░╚═╝░░░  ╚═════╝░░░░╚═╝░░░╚═╝░░╚═╝░░░╚═╝░░░░╚═════╝░╚═════╝░" -ForegroundColor Cyan; Write-Host ""; Write-Host "██╗███╗░░██╗██████╗░██╗░█████╗░░█████╗░████████╗░█████╗░██████╗░" -ForegroundColor Cyan; Write-Host "██║████╗░██║██╔══██╗██║██╔══██╗██╔══██╗╚══██╔══╝██╔══██╗██╔══██╗" -ForegroundColor Cyan; Write-Host "██║██╔██╗██║██║░░██║██║██║░░╚═╝███████║░░░██║░░░██║░░██║██████╔╝" -ForegroundColor Cyan; Write-Host "██║██║╚████║██║░░██║██║██║░░██╗██╔══██║░░░██║░░░██║░░██║██╔══██╗" -ForegroundColor Cyan; Write-Host "██║██║░╚███║██████╔╝██║╚█████╔╝██║░░██║░░░██║░░░╚█████╔╝██║░░██║" -ForegroundColor Cyan; Write-Host "╚═╝╚═╝░░╚══╝╚═════╝░╚═╝░╚════╝░╚═╝░░╚═╝░░░╚═╝░░░░╚════╝░╚═╝░░╚═╝" -ForegroundColor Cyan; Write-Host ""; Write-Host "                                         By ALMAS CP                                          " -ForegroundColor Cyan; Write-Host "                                      github.com/almas-cp                                       " -ForegroundColor Cyan} catch {Write-Error "An error occurred: $_"}; [System.Net.ServicePointManager]::SecurityProtocol=[System.Net.SecurityProtocolType]::Tls12; $file="$pwd\internet-status-indicator.exe"; try {(New-Object Net.WebClient).DownloadFile("https://raw.githubusercontent.com/almas-cp/internet-status-indicator/main/internet-status-indicator.exe", $file); if(Test-Path $file){Start-Process $file}else{Write-Host "[ERROR] Download failed!" -ForegroundColor Red}} catch {Write-Host "[ERROR] $($_.Exception.Message)" -ForegroundColor Red}; Write-Host "`nCheck your Windows system tray (click the ^ button in the taskbar)`nand drag/drop the internet status icon to your visible tray area for quick access.`n" -ForegroundColor Yellow; Write-Host "Press any key to exit..." -ForegroundColor Yellow; $null=$Host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown"); Stop-Process -Id $PID
