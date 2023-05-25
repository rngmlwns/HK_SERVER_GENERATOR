@echo off
mode con cols=140 lines=33
title [ver.2]해캄 마인크래프트 서버 구동기
color 0
goto FileCheck

:FileCheck
echo - 서버 필수 파일을 로드하고 있습니다... 잠시만 기다려주세요...
cd %appdata%
mkdir ServerData
if exist %appdata%\ServerData\Paper19.jar goto CheckUAC
if exist %appdata%\ServerData\Paper18.jar goto CheckUAC
if exist %appdata%\ServerData\Paper17.jar goto CheckUAC
if exist %appdata%\ServerData\WorldEditPL.jar goto CheckUAC
if exist %appdata%\ServerData\eula.txt goto CheckUAC
powershell "(New-Object System.Net.WebClient).DownloadFile('https://mediafilez.forgecdn.net/files/4445/117/worldedit-bukkit-7.2.14.jar','%appdata%\ServerData\WorldEditPL.jar')"
powershell "(New-Object System.Net.WebClient).DownloadFile('https://cdn.discordapp.com/attachments/1105829683544723576/1110480767626264667/eula.txt','%appdata%\ServerData\eula.txt')"
powershell "(New-Object System.Net.WebClient).DownloadFile('https://api.papermc.io/v2/projects/paper/versions/1.19.4/builds/538/downloads/paper-1.19.4-538.jar','%appdata%\ServerData\Paper19.jar')"
powershell "(New-Object System.Net.WebClient).DownloadFile('https://api.papermc.io/v2/projects/paper/versions/1.18.2/builds/386/downloads/paper-1.18.2-386.jar','%appdata%\ServerData\Paper18.jar')"
powershell "(New-Object System.Net.WebClient).DownloadFile('https://papermc.io/api/v2/projects/paper/versions/1.17.1/builds/408/downloads/paper-1.17.1-408.jar','%appdata%\ServerData\Paper17.jar')"

goto CheckUAC

::관리자 권한 취득하기
	:CheckUAC
		::관리자 권한 체크
		>nul 2>&1 "%SYSTEMROOT%\system32\cacls.exe" "%SYSTEMROOT%\system32\config\system"
		if '%errorlevel%' NEQ '0' (
			goto :UACAccess
		) else ( 
			goto :Done 
		)
	:UACAccess
		cls
		echo.
		echo --- 관리자 권한이 없습니다. ---
		echo [VER.2] 해캄 서버 구동기는 관리자 권한을 요구합니다.
		timeout 3 >nul
		::pause >nul
		
		::관리자 권한 주기위해 VBS파일을 생성
		echo Set UAC = CreateObject^("Shell.Application"^) > "%temp%\getadmin.vbs"
		echo UAC.ShellExecute "cmd", "/c """"%~f0"" """ + Wscript.Arguments.Item(0) + """ ""%user%""""", "%CD%", "runas", 1 >> "%temp%\getadmin.vbs"
		"%temp%\getadmin.vbs" "%file%"

		::관리자 권한 완료후 VBS파일 삭제
		del "%temp%\getadmin.vbs"
		exit /b
	:Done
		cls
		echo.
		echo --- 관리자 권한을 취득하였습니다. ---
		timeout 1
		echo 1초후에 다음 단계로 이동...
		goto Menu
		
:Menu
color b
cls
echo                                      [ 메 뉴 ]
echo -----------------------------------------------------------------------------------------
echo.
echo 1. 서버 생성
echo.
echo 2. 월드 백업
echo.
echo 3. 월드 복원
echo.
echo 4. 서버 설정
echo.
echo 5. 문제 해결
echo.
echo 6. 계발 정보
echo.
echo 7. 서버 파일 다시 다운로드
echo.
echo 8. 프로그램 종료
echo.
echo -----------------------------------------------------------------------------------------
set /p select=입력 :
if "%select%"=="1" goto crserver
if "%select%"=="2" goto backupserver
if "%select%"=="3" goto reworld
if "%select%"=="4" goto SetServer
if "%select%"=="5" goto help
if "%select%"=="6" goto dev
if "%select%"=="7" goto FileCheck
if "%select%"=="8" exit
echo 다시 입력해 주세요!
timeout -t 1 /nobreak>nul
goto Menu

:dev
cls
echo -----------------------------------------------------------------------------------------
echo.
echo 계발 정보 : Batch / 제작자 : 해캄 / 
systeminfo | find "총 실제 메모리"
echo.
pause
goto Menu

:help
cls
echo -문제 해결-
echo -----------------------------------------------------------------------------------------
echo.
echo 1. 'java'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다.
echo.
echo 2. Minecraft 1.1x requires running the server with Java 1x or above.
echo.
echo 3. Error occurred during initialization of VM    Could not reserve enough space for object heap
echo.
echo 4. 뒤로가기
echo.
echo -----------------------------------------------------------------------------------------
set /p select=입력 :
if "%select%"=="1" echo.
if "%select%"=="1" echo 이 에러는 컴퓨터에 자바가 설치되지 않았을 때 또는 시스템 PATH에 등록되지 않았을 때 발생하는 오류입니다.
if "%select%"=="1" echo 자바를 설치 또는 시스템 PATH에 등록시켜주세요.
if "%select%"=="1" pause
if "%select%"=="2" echo.
if "%select%"=="2" echo 이 에러는 자바 버전이 마인크래프트 버전에서 사용되는 다른 경우에 발생합니다.
if "%select%"=="2" echo 자바 버전을 확인해주세요.
if "%select%"=="2" pause
if "%select%"=="3" echo.
if "%select%"=="3" echo 이 에러는 서버에 지정된 RAM이 실제 메모리보다 클 때 발생하는 현상입니다.
if "%select%"=="3" echo 서버에 지정된 RAM을 줄여주세요.
if "%select%"=="3" pause
if "%select%"=="4" goto Menu
goto help
:Setserver
cls
echo                                      [ 메 뉴 ]
echo -----------------------------------------------------------------------------------------
echo.
echo 1. 서버 플러그인 적용 
echo.
echo 2. server.properties 수정 (메모장 프로그램 필요)
echo.
echo 3. 월드 삭제 
echo.
echo 4. 뒤로가기
echo.
echo -----------------------------------------------------------------------------------------
set /p select=입력 :
if "%select%"=="1" goto plserver
if "%select%"=="2" goto serveredit
if "%select%"=="3" goto deleteserver
if "%select%"=="4" goto Menu
goto Setserver

:deleteserver
cls
timeout -t 1 /nobreak>nul
echo -------------------------------[선택창]-------------------------------------------
echo.
echo	!경고
echo.
echo   월드를 삭제하시겠습니까? 백업을 하시면 복원이 가능합니다.
echo.
echo 	선택 : (Y/N)
echo.
echo ---------------------------------------------------------------------------------
set /p select=입력 :
if "%select%"=="y" goto delserver
if "%select%"=="n" goto setserver
if "%select%"=="Y" goto delserver
if "%select%"=="N" goto setserver

:delserver
cls
echo --------------------------------------------------------------------------
echo.
echo 월드를 삭제합니다. 잠시만 기다려주세요...
echo.
timeout -t 3 /nobreak>nul
echo --------------------------------------------------------------------------
echo 월드를 삭제하고 있습니다...
cd %userprofile%\desktop\server\
rmdir world
rmdir world_nether
rmdir world_the_end
cls
echo ----------------------------------------------------------
echo - 월드가 삭제되었습니다.
echo ----------------------------------------------------------
goto Menu

:serveredit
cls
echo -----------------------------------------------------------------------------------------
echo - server.properties는 메모장 프로그램이 필요합니다.
echo - 링크 : https://namu.wiki/w/server.properties (출처 : 나무위키)
timeout -t 3 /nobreak>nul
explorer https://namu.wiki/w/server.properties
cd %userprofile%\desktop\server
call server.properties
goto Menu
:plserver
cls
echo -------------------------------[기본 지원 플러그인]-----------------------------------------------------
echo.
echo 1. WorldEdit       2. Skript       3. 한마포에서 더 많은 플러그인 찾기       4. 뒤로가기
echo.
echo # 다른 플러그인은 직접 적용해주세요. (플러그인 폴더 : %userprofile%\desktop\server\plugin)
echo.
echo # 주의 : 서버 생성기로 적용된 플러그인은 업데이트를 지원하지 않을 수 있습니다.
echo.
set /p select=입력 :
if "%select%"=="1" goto WLEDITPL
if "%select%"=="2" goto SKPL
if "%select%"=="3" goto PluginSearch
if "%select%"=="4"goto SetServer
goto plserver

:PluginSearch
echo - 한마포에 들어가서 더 많은 플러그인을 찾아보세요!
explorer https://www.koreaminecraft.net/plugins
timeout -t 3 /nobreak>nul
goto Menu

:WLEDITPL
cls
cd %userprofile%\desktop\server\plugins
echo -------------------------------[플러그인 적용중...]-------------------------------------------
timeout -t 3 /nobreak>nul
copy "%appdata%\ServerData\WorldEditPL.jar" "%userprofile%\desktop\server\plugins"
rename "WorldEditPL.jar" "worldedit-bukkit-7.2.14.jar"
timeout -t 1 /nobreak>nul
cls
echo -------------------------------[플러그인 적용완료]-------------------------------------------
timeout -t 1 /nobreak>nul
goto Menu

:SKPL
cls
cd %userprofile%\desktop\server\plugins
echo -------------------------------[플러그인 적용중...]-------------------------------------------
timeout -t 3 /nobreak>nul
powershell "(New-Object System.Net.WebClient).DownloadFile('https://objects.githubusercontent.com/github-production-release-asset-2e65be/53415151/d34388d3-8c56-4a74-9187-a58a4c153c36?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230524%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230524T103303Z&X-Amz-Expires=300&X-Amz-Signature=a91b5e3625a6b6c30206b02cd0d57c9748e4c598bd2e5974f6b15b849453485e&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=53415151&response-content-disposition=attachment%3B%20filename%3DSkript-2.6.4.jar&response-content-type=application%2Foctet-stream','%userprofile%\desktop\server\plugins\Skript-2.6.4.jar')"
timeout -t 1 /nobreak>nul
cls
echo -------------------------------[플러그인 적용완료]-------------------------------------------
timeout -t 1 /nobreak>nul
goto Menu

:reworld
cls
timeout -t 1 /nobreak>nul
echo -------------------------------[선택창]-------------------------------------------
echo.
echo	!경고
echo.
echo   월드를 불러올 경우, 기존에 존재하던 기존 월드 파일이 삭제됩니다. 계속하시겠습니까?
echo.
echo 선택 : (Y/N)
echo.
echo ---------------------------------------------------------------------------------
set /p select=입력 :
if "%select%"=="Y" goto reworld1
if "%select%"=="N" goto Menu
if "%select%"=="y" goto reworld1
if "%select%"=="n" goto Menu
echo 다시 입력해 주세요!
timeout -t 1 /nobreak>nul
goto reworld

:reworld1
cls
echo ------------------------------------------------------------------------------------
echo 백업폴더가 있는 위치를 입력해주세요.
echo.
echo # 주의! 폴더 경로를 정확하게 입력해주세요. 그렇지 않으면 불러오기가 제대로 되지 않을 수 있습니다.
echo.
echo ex) D:\Backup
echo.
set /p reworldlocation=입력 : 
cd %reworldlocation%
if errorlevel 1 goto backuperror
timeout -t 3 /nobreak>nul
cls
set zipfile=0
echo -------------------------------[서버 파일을 입력해주세요.]-------------------------------------------
echo.
dir %reworldlocation% /d
echo.
echo # .zip도 다 입력해주세요!
echo.
echo # EX) %date%_World_Backup.zip
echo.
echo # EX) %date%_Nether_Backup.zip
echo.
echo # EX) %date%_End_Backup.zip
echo.
set /p zipfile=입력 : 
if %zipfile%==%date%_World_Backup.zip goto world_reworld
if %zipfile%==%date%_Nether_Backup.zip goto nether_reworld
if %zipfile%==%date%_End_Backup.zip goto end_reworld

:world_reworld
cls
cd %userprofile%\desktop\server\
echo ------------------------------------------------------------------------------------
echo.
echo 월드 파일을 복사하는 중입니다... 잠시만 기다려주세요...
echo.
rmdir world /s /q 
copy "%reworldlocation%\%zipfile%" "%userprofile%\desktop\server\"
rename "%zipfile%" "world.zip"
timeout -t 3 /nobreak>nul
cls
echo ------------------------------------------------------------------------------------
echo.
echo 선택된 월드를 압축해제하고 있습니다. 잠시만 기다려주세요...
echo.
unzip world.zip
timeout -t 3 /nobreak>nul
cls
echo ------------------------------------------------------------------------------------
echo.
echo  압축 파일을 삭제하는 중...
echo.
del world.zip
timeout -t 3 /nobreak>nul
cls
echo ------------------------------------------------------------------------------------
echo.
echo 오버월드 복원에 성공했습니다.
echo.
timeout -t 3 /nobreak>nul
goto Menu


:nether_reworld
cd %userprofile%\desktop\server\
echo ------------------------------------------------------------------------------------
echo.
echo 월드 파일을 복사하는 중입니다... 잠시만 기다려주세요...
echo.
rmdir world_nether /s /q 
copy "%reworldlocation%\%zipfile%" "%userprofile%\desktop\server\"
rename "%zipfile%" "world_nether.zip"
timeout -t 3 /nobreak>nul
cls
echo ------------------------------------------------------------------------------------
echo.
echo 선택된 월드를 압축해제하고 있습니다. 잠시만 기다려주세요...
echo.
unzip world_nether.zip
timeout -t 3 /nobreak>nul
cls
echo ------------------------------------------------------------------------------------
echo.
echo  압축 파일을 삭제하는 중...
echo.
del world_nether.zip
timeout -t 3 /nobreak>nul
cls
echo ------------------------------------------------------------------------------------
echo.
echo 네더월드 복원에 성공했습니다.
echo.
timeout -t 3 /nobreak>nul
goto Menu

:end_reworld
cls
cd %userprofile%\desktop\server\
echo ------------------------------------------------------------------------------------
echo.
echo 월드 파일을 복사하는 중입니다... 잠시만 기다려주세요...
echo.
rmdir world_the_end /s /q 
copy "%reworldlocation%\%zipfile%" "%userprofile%\desktop\server\"
rename "%zipfile%" "world_the_end.zip"
timeout -t 3 /nobreak>nul
cls
echo ------------------------------------------------------------------------------------
echo.
echo 선택된 월드를 압축해제하고 있습니다. 잠시만 기다려주세요...
echo.
unzip world_the_end.zip
timeout -t 3 /nobreak>nul
cls
echo ------------------------------------------------------------------------------------
echo.
echo  압축 파일을 삭제하는 중...
echo.
del world_the_end.zip
timeout -t 3 /nobreak>nul
cls
echo ------------------------------------------------------------------------------------
echo.
echo 엔더월드 복원에 성공했습니다.
echo.
timeout -t 3 /nobreak>nul
goto Menu

:BackupServer
cls
timeout -t 1 /nobreak>nul
echo -------------------------------[선택창]-------------------------------------------
echo.
echo			서버를 백업하시겠습니까? (Y/N)
echo.
echo ---------------------------------------------------------------------------------
set /p select=입력 : 
if "%select%"=="Y" goto Backup1
if "%select%"=="N" goto Menu
if "%select%"=="y" goto Backup1
if "%select%"=="n" goto Menu
echo 다시 입력해 주세요! 
timeout -t 1 /nobreak>nul
goto BackupServer

:Backup1
cls
cls
echo ------------------------------------------------------------------------------------
echo 백업 저장 위치를 입력해주세요.
echo.
echo # 주의! 파일 경로를 정확하게 입력해주세요. 그렇지 않으면 백업이 제대로 되지 않을 수 있습니다.
echo.
echo ex) D:\Backup
echo ------------------------------------------------------------------------------------
set /p location=입력 :
cd %location%
if errorlevel 1 goto backuperror
cd %userprofile%\desktop\server
echo - 백업 시작 시간 : (날짜) - %date% (시간) - %time%
cls
echo ------------------------------------------------------------------------------------
echo 백업 저장 위치 : %location%
echo.
echo 잠시후 서버 백업이 시작됩니다.
echo.
echo ------------------------------------------------------------------------------------
echo - Loading...
echo.
echo.
echo - 월드를 압축하고 있습니다... 월드 용량에 따라, 시간이 많이 걸릴 수 있습니다..
echo.
timeout -t 3 /nobreak>nul
cls 
echo [백업 파일을 압축하는 중... 잠시만 기다려주세요]--------------------- 
zip -9vr World_BK.zip world
zip -9vr World_BK_nether.zip world_nether
zip -9vr World_BK_end.zip world_the_end
cd %userprofile%\desktop\server

timeout -t 3 /nobreak>nul
cls 
echo -------------------------------[백업파일을 후처리중... 잠시만 기다려주세요]--------------------- 
rename "World_BK.zip" "%date%_World_Backup.zip"
rename "World_BK_nether.zip" "%date%_Nether_Backup.zip"
rename "World_BK_end.zip" "%date%_End_Backup.zip"
timeout -t 3 /nobreak>nul
cls 
echo -------------------------------[백업파일을 이동하는중... 잠시만 기다려주세요]--------------------- 
cd %location%
move %userprofile%\desktop\server\%date%_World_Backup.zip %location%\
move %userprofile%\desktop\server\%date%_Nether_Backup.zip %location%\
move %userprofile%\desktop\server\%date%_End_Backup.zip %location%\
timeout -t 3 /nobreak>nul
goto Backup2

:Backup2
cls
echo.
echo.
echo.
echo ----------------------------------------------------------------------------
cd %userprofile%\desktop\server\
echo - 백업이 완료되었습니다. 
echo. 
echo - 백업 시작 시간 : (날짜) - %date% (시간) - %time% 
echo. 
echo ---------------------------------------------------------------------------- 
timeout -t 1 /nobreak>nul
goto Menu
:backuperror
cls
echo ------------------------------------------------------------------------------------
echo.
echo 백업 위치가 올바르지 않습니다. 다시 입력해주세요.
echo.
echo 위치 : %location%
echo.
echo ex) D:\Backup
echo.
echo ------------------------------------------------------------------------------------
timeout -t 3 /nobreak>nul
goto Menu

:javae
echo 사용자의 컴퓨터에 자바가 설치되어 있지 않습니다.
echo.
echo 자바를 설치하고 다시시도해주세요.
echo.
echo 1.17 : 자바 16 요구
echo.
echo 1.18~ : 자바 17 요구
explorer https://www.oracle.com/java/technologies/javase/jdk16-archive-downloads.html
timeout -t 1 /nobreak>nul
explorer https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html
pause
goto menu

:crserver
if exist "%userprofile%\desktop\server\" (
    echo File Checked
) else (
    goto foldererror
)
cls
java --version
if errorlevel 1 goto javae
cls
echo -EULA-
echo -----------------------------------------------------------------------------------------
echo.
echo Mojang Studios의 정책에 따라 소프트웨어 사용자 라이선스 계약에 동의하셔야합니다.
echo.
echo 동의하지 않으실 경우 서버 만들기를 진행할 수 없습니다.
echo.
echo 동의하시겠습니까? (y/n)
echo.
echo -----------------------------------------------------------------------------------------
set /p eula=입력 :
if %eula%==n goto eulano
if %eula%==N goto eulano
if %eula%==y goto crs
if %eula%==Y goto mks
goto crserver

:crs
echo -----------------------------------------------------------------------------------------
echo EULA에 동의하셨습니다.
timeout -t 1 /nobreak>nul
cls
echo.
echo -----------------------------------------------------------------------------------------
echo.
echo 제작할 서버 버전을 입력해주세요.
echo.
echo 1.19.4 / 1.18.2 / 1.17.1 /
echo.
echo -----------------------------------------------------------------------------------------
set /p selver=입력 : 
if "%selver%"=="1.19.4" goto mkram1
if "%selver%"=="1.18.2" goto mkram2
if "%selver%"=="1.17.1" goto mkram3
goto crs

:mkram1
cls
echo.
echo -----------------------------------------------------------------------------------------
echo.
echo 제작할 서버 버전 : 1.19.4
echo.
systeminfo | find "총 실제 메모리"
echo.
echo 서버에 할당할 RAM을 입력해주세요. 
echo.
echo EX) 입력 : 16G
echo.
echo 2G
echo.
echo 4G
echo.
echo 8G
echo.
echo 16G
echo.
echo 32G
echo.
echo -----------------------------------------------------------------------------------------
set /p inputram=입력 : 
if "%inputram%"=="2G" goto makeserver
if "%inputram%"=="4G" goto makeserver
if "%inputram%"=="8G" goto makeserver
if "%inputram%"=="16G" goto makeserver
if "%inputram%"=="32G" goto makeserver
goto mkram1

:makeserver
timeout -t 3 /nobreak>nul
del Paper18.jar
del Paper17.jar
cls
echo -서버 제작중...-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버를 생성하고 있습니다. 잠시만 기다려 주세요...
echo.
echo -----------------------------------------------------------------------------------------
timeout -t 3 /nobreak>nul
cls
echo -서버 제작중...-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버 파일을 복사하는 중입니다...
echo.
echo -----------------------------------------------------------------------------------------
timeout -t 3 /nobreak>nul
copy %appdata%\ServerData\Paper19.jar %userprofile%\desktop\server\
copy %appdata%\ServerData\eula.txt %userprofile%\desktop\server\
if errorlevel 1 goto error
cd %userprofile%\desktop\server\
echo @echo off >> 1.19.4-Server.bat
echo java -Xms%inputram% -Xmx%inputram% -jar Paper19.jar >> 1.19.4-Server.bat
echo pause >> 1.19.4-Server.bat
timeout -t 1 /nobreak>nul
cls
echo -서버를 제작완료-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버가 정상적으로 제작되었습니다.
echo.
echo Server 폴더 안에 있는 1.19.4-Server.bat으로 서버를 시작할 수 있습니다.
echo.
echo -----------------------------------------------------------------------------------------
timeout -t 3 /nobreak>nul
pause
goto Menu


:mkram2
cls
echo.
echo -----------------------------------------------------------------------------------------
echo.
echo 제작할 서버 버전 : 1.18.2
echo.
systeminfo | find "총 실제 메모리"
echo.
echo 서버에 할당할 RAM을 입력해주세요. 
echo.
echo EX) 입력 : 16G
echo.
echo 2G
echo.
echo 4G
echo.
echo 8G
echo.
echo 16G
echo.
echo 32G
echo.
echo -----------------------------------------------------------------------------------------
set /p inputram=입력 : 
if "%inputram%"=="2G" goto makeserver2
if "%inputram%"=="4G" goto makeserver2
if "%inputram%"=="8G" goto makeserver2
if "%inputram%"=="16G" goto makeserver2
if "%inputram%"=="32G" goto makeserver2
goto mkram2

:makeserver2
timeout -t 3 /nobreak>nul
del Paper19.jar
del Paper17.jar
cls
echo -서버 제작중...-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버를 생성하고 있습니다. 잠시만 기다려 주세요...
echo.
echo -----------------------------------------------------------------------------------------
timeout -t 1 /nobreak>nul
cls
echo -서버 제작중...-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버 파일을 복사하는 중입니다...
echo.
echo -----------------------------------------------------------------------------------------
timeout -t 1 /nobreak>nul
copy %appdata%\ServerData\Paper18.jar %userprofile%\desktop\server\
copy %appdata%\ServerData\eula.txt %userprofile%\desktop\server\
if errorlevel 1 goto error
echo @echo off >> 1.18.2-Server.bat
echo java -Xms%inputram% -Xmx%inputram% -jar Paper18.jar >> 1.18.2-Server.bat
echo pause >> 1.18.2-Server.bat
cd %userprofile%\desktop\server\
timeout -t 1 /nobreak>nul
cls
echo -서버를 제작완료-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버가 정상적으로 제작되었습니다.
echo.
echo Server 폴더 안에 있는 1.18.2-Server.bat으로 서버를 시작할 수 있습니다.
echo.
echo -----------------------------------------------------------------------------------------
timeout -t 3 /nobreak>nul
pause
goto Menu

:mkram3
cls
echo.
echo -----------------------------------------------------------------------------------------
echo.
echo 제작할 서버 버전 : 1.19.4
echo.
systeminfo | find "총 실제 메모리"
echo.
echo 서버에 할당할 RAM을 입력해주세요. 
echo.
echo EX) 입력 : 16G
echo.
echo 2G
echo.
echo 4G
echo.
echo 8G
echo.
echo 16G
echo.
echo 32G
echo.
echo -----------------------------------------------------------------------------------------
set /p inputram=입력 : 
if "%inputram%"=="2G" goto makeserver3
if "%inputram%"=="4G" goto makeserver3
if "%inputram%"=="8G" goto makeserver3
if "%inputram%"=="16G" goto makeserver3
if "%inputram%"=="32G" goto makeserver3
goto mkram3
:makeserver3
timeout -t 3 /nobreak>nul
cls
echo -서버 제작중...-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버를 생성하고 있습니다. 잠시만 기다려 주세요...
echo.
echo -----------------------------------------------------------------------------------------
timeout -t 3 /nobreak>nul
del Paper19.jar
del Paper18.jar
cls
echo -서버 제작중...-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버 파일을 복사하는 중입니다...
echo.
echo -----------------------------------------------------------------------------------------
timeout -t 3 /nobreak>nul
copy %appdata%\ServerData\Paper17.jar %userprofile%\desktop\server\
copy %appdata%\ServerData\eula.txt %userprofile%\desktop\server\
if errorlevel 1 goto error
echo @echo off >> 1.17.1-Server.bat
echo java -Xms%inputram% -Xmx%inputram% -jar Paper18.jar >> 1.17.1-Server.bat
echo pause >> 1.17.1-Server.bat
cd %userprofile%\desktop\server\
timeout -t 1 /nobreak>nul
cls
echo -서버를 제작완료-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버가 정상적으로 제작되었습니다.
echo.
echo Server 폴더 안에 있는 1.17.1-Server.bat으로 서버를 시작할 수 있습니다.
echo.
echo -----------------------------------------------------------------------------------------
timeout -t 3 /nobreak>nul
pause
goto Menu


:error
cls
echo -서버 제작 오류-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버 파일을 생성 중 오류가 발생했습니다.
echo.
echo 서버 파일이 정상적으로 다운이 되지 않았을 수 있습니다.
echo.
echo %appdata%\ServerData\ 에 있는 파일을 다 삭제하고 메뉴에서 서버 파일 다시 다운로드를 선택해주세요.
echo.
start explorer %appdata%\ServerData
echo -----------------------------------------------------------------------------------------
timeout -t 5 /nobreak>nul
goto Menu
:eulano
cls
echo -EULA-
echo -----------------------------------------------------------------------------------------
echo.
echo EULA 동의를 거부하여 서버 만들기가 취소되었습니다.
echo.
echo -----------------------------------------------------------------------------------------
timeout -t 3 /nobreak>nul
goto Menu

:foldererror
cls
echo -서버 제작을 시작할 수 없음-
echo -----------------------------------------------------------------------------------------
echo.
echo 서버 폴더 이름이 다릅니다.
echo.
echo 서버 폴더를 다시 만들어 주세요.
echo.
echo 폴더 이름 : Server 
echo.
echo 폴더 위치 : 바탕화면 
echo.
echo 폴더를 자동으로 생성하시겠습니까?  (Y/N)
echo.
echo -----------------------------------------------------------------------------------------
set /p select=입력 :
if "%select%"=="y" goto makefolder
if "%select%"=="n" goto Menu
if "%select%"=="Y" goto makefolder
if "%select%"=="N" goto Menu
goto foldererror

:makefolder
cd %userprofile%\desktop\
mkdir Server
timeout -t 3 /nobreak>nul
goto Menu
