Set IIS gzip and deflate

cd C:\Inetpub\AdminScripts\

cscript adsutil.vbs SET W3SVC/Filters/Compression/Deflate/HcFileExtensions "htm html txt css js"

cscript adsutil.vbs SET W3SVC/Filters/Compression/gzip/HcFileExtensions "htm html txt css js"

separate items:

adsutil.vbs SET w3svc/Filters/Compression/Deflate/HcFileExtensions "htm" "html" "txt" "css" "js"

adsutil.vbs SET w3svc/Filters/Compression/gzip/HcFileExtensions "htm" "html" "txt" "css" "js"

adsutil.vbs GET w3svc/Filters/Compression/Deflate/HcFileExtensions

adsutil.vbs GET w3svc/Filters/Compression/gzip/HcFileExtensions

Restart IIS gracefully:

iisreset /noforce


Restart w3svc after making the above changes:

net stop w3svc
net stop iisadmin
net start iisadmin
net start w3svc


Include the following web config file:

<!-- Web.Config Configuration File -->

<configuration>
  <system.web>
       <customErrors mode="Off"/>
       <webServices>
           <protocols>
               <add name="HttpGet"/>
               <add name="HttpPost"/>
           </protocols>
       </webServices>
  </system.web>
  <system.webServer>
    <staticContent>
        <mimeMap fileExtension=".m4v" mimeType="video/m4v" />
        <mimeMap fileExtension=".m4a" mimeType="audio/mp4" />
        <mimeMap fileExtension=".mp4" mimeType="audio/mp4" />
        <mimeMap fileExtension=".ogg" mimeType="audio/ogg" />
        <mimeMap fileExtension=".oga" mimeType="audio/ogg" />
        <mimeMap fileExtension=".ogv" mimeType="video/ogg" />
        <mimeMap fileExtension=".webm" mimeType="video/webm"/>
        <clientCache httpExpires="Sun, 29 Mar 2020 00:00:00 GMT" cacheControlMode="UseExpires" />
    </staticContent>
    
    <httpCompression directory="%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files">
      <scheme name="gzip" dll="%Windir%\system32\inetsrv\gzip.dll"/>
      <dynamicTypes>
        <add mimeType="text/*" enabled="true"/>
        <add mimeType="message/*" enabled="true"/>
        <add mimeType="application/javascript" enabled="true"/>
        <add mimeType="text/css" enabled="true"/>
        <add mimeType="*/*" enabled="false"/>
      </dynamicTypes>
      <staticTypes>
        <add mimeType="text/*" enabled="true"/>
        <add mimeType="message/*" enabled="true"/>
        <add mimeType="application/javascript" enabled="true"/>
        <add mimeType="text/css" enabled="true"/>
        <add mimeType="*/*" enabled="false"/>
      </staticTypes>
    </httpCompression>
    <urlCompression doStaticCompression="true" doDynamicCompression="true"/>
  </system.webServer>

</configuration>
