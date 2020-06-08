# DockerSonarqube
Docker desktop and Docker toolbox
1. Descargar SonarQube
docker pull sonarqube

2. Ejecutar una instancia de SonarQube 
docker run -d --name sonarqube -p 9000:9000 sonarqube

Nota: para eliminar una instancia previa puede utilizar el comando: docker rm -f sonarqube

3. Ingresar al portal con las credenciales
# Docker desktop  
http://localhost:9999/
# Docker toolbox 
http://192.168.99.100:9000 
user: admin
pass:admin

4. Crear una nueva aplicación con el nombre aplicacionNetCore

5. Generar el token de la nueva aplicación aplicacionNetCore, debera devolver algo similar a 8a15d2a89c8636f15eb32ebee0993b8d16bff94e

6. Decargar Net Core e instalar
https://dotnet.microsoft.com/download/dotnet-core/thank-you/sdk-3.1.300-windows-x64-installer

7. En un terminal ejecutar e instalar sonar-scanner
dotnet tool install --global dotnet-sonarscanner

8. En un terminal, acceder a una ruta donde creara una nueva aplicación
dotnet new sln -o aplicacionNetCore 
cd aplicacionNetCore 
dotnet new console
dotnet sln aplicacionNetCore.sln add aplicacionNetCore.csproj 

9. En el mismo terminal, iniciar la sesión de revisión de sonarqube
# Docker desktop 
dotnet sonarscanner begin /d:sonar.login=admin /d:sonar.host.url="http://192.168.99.100:9000".password=admin /k:”aplicacionNetCore”
# Docker toolbox  
dotnet SonarScanner begin /k:"aplicacionNetCore" /d:sonar.host.url="http://192.168.99.100:9000" /d:sonar.login="fe2c04f332a90a0e90f02c220a66c58f8d1f13ce"

10. Compilar la aplicación
dotnet build

11. Cerramos la sesión
# Docker desktop 
dotnet sonarscanner end /d:sonar.login=admin /d:sonar.password=admin 
# Docker toolbox Docker toolbox  
dotnet SonarScanner end /d:sonar.login="fe2c04f332a90a0e90f02c220a66c58f8d1f13ce"
