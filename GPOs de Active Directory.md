# Diferentes gpos de active directory


    Denegar la posibilidad de cambiar el fondo de pantalla 
```Powershell
New-GPO -Name "CambioFondoDenegado" -Comment "Impide a los usuarios cambiar el fondo de pantalla de los ordenadores"
Set-GPRegistryValue -Name "CambioFondoDenegado" -Key "HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer" -ValueName NoThemesTab -Type DWORD  -Value 00000001
New-GPLink -Name "CambioFondoDenegado" -Target "ou=recursoshumanos,dc=andel,dc=local"
```

    No mostrar a los usuarios el icono de red(SOLO ACCESO LOCAL)
```Powershell
New-GPO -Name "Icono acceso red local denegado" -Comment "No muestra a los usuarios el icono de red(SOLO ACCESO LOCAL)"
Set-GPRegistryValue -Name "Icono acceso red local denegado" -Key "HKCU\Software\Policies\Microsoft\Windows\Network Connections" -ValueName NC_DoNotShowLocalOnlyIcon -Type DWORD  -Value 00000001
New-GPLink -Name "Icono acceso red local denegado" -Target "ou=finanzas,dc=andel,dc=local"
```

    Prohibir la conexión y desconexión de una conexión de acceso remoto
```Powershell
New-GPO -Name "Conexiones remotas" -Comment "Prohibir la conexión y desconexión de una conexión de acceso remoto"
Set-GPRegistryValue -Name "Conexiones remotas" -Key "HKCU\Software\Policies\Microsoft\Windows\Network Connections" -ValueName NC_RasConnect -Type DWORD  -Value 00000000
New-GPLink -Name "Conexiones remotas" -Target "ou=contabilidad,dc=andel,dc=local"
```

    Prohíbe la publicación de carpetas compartidas
```Powershell
New-GPO -Name "Bloqueo Carpetas compartidas" -Comment "Denegar la publicación de carpetas compartidas"
Set-GPRegistryValue -Name "Bloqueo Carpetas compartidas" -Key "HKCU\Software\Policies\Microsoft\Windows NT\SharedFolders" -ValueName PublishSharedFolders -Type DWORD  -Value 00000000
New-GPLink -Name "Bloqueo Carpetas compartidas" -Target "ou=marketing,dc=andel,dc=local"
```

   Impedir que se elimine el historial de descarga
```Powershell
New-GPO -Name "NoBorrarHistorialDescargas" -Comment "Impide que se elimine el historial de descarga"
Set-GPRegistryValue -Name "NoBorrarHistorialDescargas" -Key "HKCU\Software\Policies\Microsoft\Internet Explorer\Privacy" -ValueName CleanDownloadHistory -Type DWORD  -Value 00000000
New-GPLink -Name "NoBorrarHistorialDescargas" -Target "ou=compras,ou=marketing,dc=andel,dc=local"
```
    
    Impedir que se elimine el historial de páginas web visitas por el usuario
```Powershell
New-GPO -Name "NoBorrarPáginasVisitadas" -Comment "Impide que se elimine el historial de páginas web visitas por el usuario"
Set-GPRegistryValue -Name "NoBorrarPáginasVisitadas" -Key "HKCU\Software\Policies\Microsoft\Internet Explorer\Privacy" -ValueName CleanHistory -Type DWORD  -Value 00000000
New-GPLink -Name "NoBorrarPáginasVisitadas" -Target "ou=ventas,ou=marketing,dc=andel,dc=local"
```

    Impide el acceso al símbolo del sistema (CMD), sin uso de hash
```Powershell
New-GPO -Name "CMDdenegado" -Comment "Impide el acceso al símbolo del sistema (CMD)"
Set-GPRegistryValue -Name "CMDdenegado" -Key "HKCU\Software\Policies\Microsoft\Windows\System" -ValueName DisableCMD -Type DWORD  -Value 00000002
New-GPLink -Name "CMDdenegado" -Target "ou=marketing,dc=andel,dc=local"
```

    Todas las clases de unidades de almacenamiento extraible quedan denegadas(usar carpetas compartidas)
```Powershell
New-GPO -Name "Almacenamiento extraible" -Comment "Todas las clases de unidades de almacenamiento extraible quedan denegadas(usar carpetas compartidas)"
Set-GPRegistryValue -Name "Almacenamiento extraible" -Key "HKCU\Software\Policies\Microsoft\Windows\RemovableStorageDevices" -ValueName Deny_All -Type DWORD  -Value 00000001
New-GPLink -Name "Almacenamiento extraible" -Target "ou=contabilidad,dc=andel,dc=local"
```
