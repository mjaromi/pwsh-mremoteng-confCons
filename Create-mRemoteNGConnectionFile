function Create-mRemoteNGConnectionFile {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory)][string] $consulUri,
        [Parameter(Mandatory)][string] $connectionFile,
        [Parameter(Mandatory)][string] $sshUsername
    )

    $CONFIG = 'Descr="" Icon="" Panel="General" Id="GUID" Username="sshUsername" Domain="" Password="" Hostname="IP_ADDRESS" Protocol="SSH2" PuttySession="Default Settings" Port="22" ConnectToConsole="false" UseCredSsp="true" RenderingEngine="IE" ICAEncryptionStrength="EncrBasic" RDPAuthenticationLevel="NoAuth" RDPMinutesToIdleTimeout="0" RDPAlertIdleTimeout="false" LoadBalanceInfo="" Colors="Colors16Bit" Resolution="FitToWindow" AutomaticResize="true" DisplayWallpaper="false" DisplayThemes="false" EnableFontSmoothing="false" EnableDesktopComposition="false" CacheBitmaps="false" RedirectDiskDrives="false" RedirectPorts="false" RedirectPrinters="false" RedirectSmartCards="false" RedirectSound="DoNotPlay" SoundQuality="Dynamic" RedirectKeys="false" Connected="false" PreExtApp="" PostExtApp="" MacAddress="" UserField="" ExtApp="" VNCCompression="CompNone" VNCEncoding="EncHextile" VNCAuthMode="AuthVNC" VNCProxyType="ProxyNone" VNCProxyIP="" VNCProxyPort="0" VNCProxyUsername="mjaromi" VNCProxyPassword="" VNCColors="ColNormal" VNCSmartSizeMode="SmartSAspect" VNCViewOnly="false" RDGatewayUsageMethod="Never" RDGatewayHostname="" RDGatewayUseConnectionCredentials="Yes" RDGatewayUsername="mjaromi" RDGatewayPassword="" RDGatewayDomain="" InheritCacheBitmaps="false" InheritColors="false" InheritDescription="false" InheritDisplayThemes="false" InheritDisplayWallpaper="false" InheritEnableFontSmoothing="false" InheritEnableDesktopComposition="false" InheritDomain="false" InheritIcon="false" InheritPanel="false" InheritPassword="false" InheritPort="false" InheritProtocol="false" InheritPuttySession="false" InheritRedirectDiskDrives="false" InheritRedirectKeys="false" InheritRedirectPorts="false" InheritRedirectPrinters="false" InheritRedirectSmartCards="false" InheritRedirectSound="false" InheritSoundQuality="false" InheritResolution="false" InheritAutomaticResize="false" InheritUseConsoleSession="false" InheritUseCredSsp="false" InheritRenderingEngine="false" InheritUsername="false" InheritICAEncryptionStrength="false" InheritRDPAuthenticationLevel="false" InheritRDPMinutesToIdleTimeout="false" InheritRDPAlertIdleTimeout="false" InheritLoadBalanceInfo="false" InheritPreExtApp="false" InheritPostExtApp="false" InheritMacAddress="false" InheritUserField="false" InheritExtApp="false" InheritVNCCompression="false" InheritVNCEncoding="false" InheritVNCAuthMode="false" InheritVNCProxyType="false" InheritVNCProxyIP="false" InheritVNCProxyPort="false" InheritVNCProxyUsername="false" InheritVNCProxyPassword="false" InheritVNCColors="false" InheritVNCSmartSizeMode="false" InheritVNCViewOnly="false" InheritRDGatewayUsageMethod="false" InheritRDGatewayHostname="false" InheritRDGatewayUseConnectionCredentials="false" InheritRDGatewayUsername="false" InheritRDGatewayPassword="false" InheritRDGatewayDomain="false"'

    $start = '<?xml version="1.0" encoding="utf-8"?><mrng:Connections xmlns:mrng="http://mremoteng.org" Name="Connections" Export="false" EncryptionEngine="AES" BlockCipherMode="GCM" KdfIterations="1000" FullFileEncryption="false" Protected="1+IGXSEHZGQsAp1byi+ufcR9a0xVt+Wmb4VeLZsjgVuwS9K5rEAfQu1AzQwxYfFCNCNI5xW75KcSJPSEO4G7HeR+" ConfVersion="2.6">'
    $nodes = '    <Node Name="NODE_NAME - IP_ADDRESS" Type="Connection" CONFIG/>'
    $end = '</mrng:Connections>'

    # create mRemoteNG Connection File
    $start | Out-File -FilePath $connectionFile

    $consulNodes=(Invoke-WebRequest -Uri $consulUri -UseBasicParsing).Content
    foreach ($node in ($consulNodes | ConvertFrom-Json)) {
        if ($node.Address -match '\d.\d.\d.\d') {
            $nodes `
            -replace 'CONFIG',$CONFIG `
            -replace 'sshUsername',$sshUsername `
            -replace 'NODE_NAME',$node.Node `
            -replace 'IP_ADDRESS',$node.Address `
            -replace 'GUID',(New-Guid).Guid `
            | Out-File -FilePath $connectionFile -Append
        }
    }

    $end | Out-File -FilePath $connectionFile -Append
}
