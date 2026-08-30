@echo off
setlocal

:: التحقق من صلاحيات Administrator
net session >nul 2>&1
if %errorlevel% neq 0 (
    echo Requesting Administrator privileges...
    powershell -NoProfile -Command "Start-Process -FilePath '%~f0' -Verb RunAs"
    exit /b
)

:: الانتقال إلى مجلد ملف BAT
cd /d "%~dp0"

:: التحقق من وجود ملفات التثبيت
if not exist "setup.exe" (
    echo.
    echo ERROR: setup.exe was not found.
    echo.
    pause
    exit /b 1
)

if not exist "configuration.xml" (
    echo.
    echo ERROR: configuration.xml was not found.
    echo.
    pause
    exit /b 1
)

echo.
echo ========================================
echo        Office Installation
echo ========================================
echo.
echo Installing Office...
echo.

setup /configure configuration.xml

echo.
echo ========================================
echo Installation command finished.
echo ========================================
echo.

pause
