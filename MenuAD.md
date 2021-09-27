# MENU PARA CREAR LA ESTRUCTURA DE AD (USUARIOS, OUs, ETC)
```Powershell
function EMPRESA($opciones)
{
       
while($opciones -ne 0)
{       $opciones = read-host  {

     "______________________________________________________________________________________________"
               
               "1   - Crear unidad organizativa(UO)"
               "2   - Crear unidad organizativa(UO) dentro de otra UO"
               "3   - meter grupos dentro de UO de nivel 1"
               "4   - meter grupos dentro de UO de nivel 2"
               "5   - hacer que las contraseñas del dominio no tengan que presentar complegidad"
               "6   - Crear usuarios por teclado"
               "7   - Crear usuarios desde fichero"
               "8   - Mover usuarios a grupos"
               

     "______________________________________________________________________________________________"
     }



      switch($opciones)

        {
        "1"{
                $NombreUO = read-host "Escribe el nombre de la unidad organizativa"
            
                New-ADOrganizationalUnit -Name $NombreUO -Path "dc=andel,dc=local" }

        
        
        "2"{
                 $nombreUOexistente = Read-Host "Nombre de la UO ya existente"
                 $NombreUO = read-host "Escribe el nombre de la unidad organizativa"
            
                 New-ADOrganizationalUnit -Name $NombreUO -Path "ou=$nombreUOexistente,dc=andel,dc=local"}

        
        
        "3"{
                $grupo = Read-Host "Nombre del grupo"
                $OUYACREADA = Read-Host "Nmbre del la unidad organizativa ya existente"
            
                New-ADGroup -Name $grupo -GroupScope DomainLocal -Path "OU=$OUYACREADA,DC=andel,DC=local"}

       
       
        "4"{
                $grupo = Read-Host "Nombre del grupo"
                $OUYACREADA1 = Read-Host "Nombre del la unidad organizativa Nivel 1 ya existente"
                $OUYACREADA2 = Read-Host "Nombre del la unidad organizativa Nivel 2 ya existente"
            
                  
                 New-ADGroup -Name $grupo -GroupScope DomainLocal -Path "OU=$OUYACREADA2,OU=$OUYACREADA1,DC=andel,DC=local"}


        "5"{ 
                Set-ADDefaultDomainPasswordPolicy -ComplexityEnabled $False -Identity andel.local
            }
        
        
        
        "6"{ 
                $nombre = Read-Host "Nombre del usuario"
                $contraseña = Read-Host "Nueva contraseña"

            
                new-aduser -name $nombre  -ChangePasswordAtLogon $false -Enabled $true -accountpassword (convertto-securestring $contraseña -asplaintext -force) -whatif
            }

        "7"{ 
               foreach ($usuarios in gc .\usuarios.txt)
                {
                  new-aduser -name (($usuarios).split(",")[0] ) -ChangePasswordAtLogon $false  -accountpassword (convertto-securestring ($usuarios).split(",")[1] -asplaintext -force) -whatif
                } 
           }


         "8"{
                $nombreusuariomover = read-host "Nombre del usuario que quieres mover"
                $grupo = read-host "Nombre del grupo a donde quieres mover el usuario"

                Add-ADGroupMember $grupo -Members $nombreusuariomover 

            }       
  }     
}
}
EMPRESA ; Write-host "opción a elegir"

```
