//====================================================================================
// Open Computer and Software Inventory Next Generation
// Copyright (C) 2010 OCS Inventory NG Team. All rights reserved.
// Web: http://www.ocsinventory-ng.org

// This code is open source and may be copied and modified as long as the source
// code is always made freely available.
// Please refer to the General Public Licence V2 http://www.gnu.org/ or Licence.txt

// THIS SOFTWARE IS PROVIDED ``AS IS'' AND ANY EXPRESS OR IMPLIED WARRANTIES,
// INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND
// FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED.
// IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
// SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
// PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
// OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
// WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
// OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED
// OF THE POSSIBILITY OF SUCH DAMAGE.
//====================================================================================


REQUIREMENTS
============

- Microsoft Visual C++ 2013 SP1 or higher
- Perl 5.8 or newer for building dependencies (you can use XAMPP perl addon)
- Source code exported from GitHub.
  git clone https://github.com/OCSInventory-NG/WindowsAgent.git


BUILDING DEPENDENCIES
=====================

OCS Inventory NG Agent for Windows needs following libraries:

- zlib 1.2.8 or newer (www.zlib.net)
- openssl 1.0.0n or newer (www.openssl.org)
- curl 7.37.1 or newer (http://curl.haxx.se/)
- tinyXML 2.6.2 or newer (http://www.sourceforge.net/projects/tinyxml/)
- net-snmp 5.7 or newer (http://www.net-snmp.org/)
- ZipArchive GPL Edition 4.0.1 or newer (http://www.artpol-software.com)

Uncompress sources of these libraries into directory "External_Deps" to create
the following directory structures.
- External_Deps\Zlib-X.X.X
- External_Deps\openssl-X.X.X
- External_Deps\curl-X.X.X
- External_Deps\tinyxml
- External_Deps\net-snmp-X.X
- External_Deps\ZipArchive

Open "ZipArchive.sln" Visual C++ 2013 solution in folder
"External_Deps\ZipArchive", select configuration "Release Unicode STL MD DLL"
for platform Win32, and edit project properties. Add
_BIND_TO_CURRENT_VCLIBS_VERSION preprocessor define to "Configuration
properties / C/C++ / Preprocessor" section to automatically bind DLL to Visual
C++ 2008 SP1 CRT and MFC versions (for more explanation, see Jochen Kalmbach's Blog
http://blog.kalmbach-software.de/2009/05/27/deployment-of-vc2008-apps-without-installing-anything/)
Save and build to create unicode DLL for ZipArchive Library.

Script for building dependency automatically fixes cURL and net-snmp Makefiles for Visual C++ 2013,
by adding "/D_BIND_TO_CURRENT_VCLIBS_VERSION" to the CFLAGS. As is, libcurl and net-snmp
DLL will be bound to latest Visual C++ 2008 SP1 CRT versions.

For Zlib, OpenSSL and TinyXML, compiling using _BIND_TO_CURRENT_VCLIBS_VERSION
preprocessor define is done through the call of build file "OCS_Make_Required_Libs.bat".


Edit script "OCS_Make_Required_Libs.bat" to meet your need, especially

- Set path to MS Visual C++ 2013, for example
  set VC_PATH=C:\Program Files (x86)\Microsoft Visual Studio X.X\VC
- Set path to MS Windows SDK, needed to build cURL, for example with VC++ 2013
  set WINDOWS_SDK_PATH="C:\Program Files\Microsoft SDKs\Windows\vX.X"
- Set path to Perl 5.6 or higher binary, for example
  set PERL_PATH=C:\xampp\perl\bin
- Set path to Zlib sources, for example
  set ZLIB_PATH=D:\Developp\OCS Inventory NG\Bazaar\ocsinventory-windows-agent\External_Deps\zlib-1.2.5
- Set path to OpenSSL sources, for example
  set OPENSSL_PATH=D:\Developp\OCS Inventory NG\Bazaar\ocsinventory-windows-agent\External_Deps\openssl-1.0.0
- Set path to cURL sources, for example
  set CURL_PATH=D:\Developp\OCS Inventory NG\Bazaar\ocsinventory-windows-agent\External_Deps\curl-7.20.1
- Set path to tinyXML sources, for example
  set XML_PATH=D:\Developp\OCS Inventory NG\Bazaar\ocsinventory-windows-agent\External_Deps\tinyxml
- Set path to ZipArchive sources, for example
  set ZIP_PATH=D:\Developp\OCS Inventory NG\Bazaar\ocsinventory-windows-agent\External_Deps\ZipArchive

Then, launch script "OCS_Make_Required_Libs.bat" to create all libs and prepare for building OCS agent.


BUILDING AGENT
==============

Open solution "OCSInventory.sln", select project "Agent" and build it !

See Options.txt for agent's command line switches.

We hope it will works for you !

OCS Inventory Team
